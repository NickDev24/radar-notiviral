# 📘 Documentación técnica pública — APIFENIX

Referencia pública de la API de APIFENIX: qué señales resuelve, cómo te
autenticás y qué endpoints existen.

- **API pública**: https://apifenix.mp4-render.site
- **Docs interactivas (Swagger)**: https://apifenix.mp4-render.site/api/docs
- **OpenAPI**: https://apifenix.mp4-render.site/api/openapi.json
- **Radar público**: `/mapa` · `/mural` · `/catalogo`

---

## 1. Arquitectura (vista de alto nivel)

```
  100+ FUENTES (23 provincias)
  ├── RSS directos (editoriales, radios, oficiales)
  ├── Google News RSS (medios sin feed propio)
  └── YouTube feeds oficiales (feeds/videos.xml?channel_id=)
            │  ingesta cada 15 min
            ▼
  MOTOR RADAR v2  ── firma · clusters · primicias · huérfanas · reloj · gaps · agenda
            │
            ▼
  PostgreSQL (datos + señales indexadas)      Redis (rate limit + cuotas)
            │
            ▼
  FastAPI  ──►  API REST  +  Portal web  +  MCP  +  SDKs
```

El motor corre sobre fuentes reales de las 23 provincias argentinas: medios
editoriales, radios, canales oficiales y canales de YouTube. La deduplicación
se hace por hash de URL y la agrupación de la misma nota por **firma** del
título normalizado.

---

## 2. Autenticación

| Mecanismo | Uso |
|---|---|
| `X-API-Key` (header) | API REST (`/api/v1/*`) |
| Cookie de sesión firmada | Portal web (`/portal`, `/mapa`, `/mural`) |
| Google OAuth | `/auth/google` |
| Email + verificación | `/registro` → email → verificar |

- Las API keys se guardan **hasheadas (SHA-256)**; el valor real solo se muestra una vez, al crearla.
- Rate limit por minuto y cuota diaria se cuentan por key. El plan **GRATIS** alcanza 30 req/min y 5.000 req/día.
- Los SDKs (Python y JavaScript) y el servidor MCP se entregan desde el portal, con tu key.

---

## 3. Endpoints del Motor Radar v2

| Endpoint | Qué resuelve |
|---|---|
| `GET /api/v1/items` | Feed de notas con todas las señales y filtros |
| `GET /api/v1/clusters?min_fuentes=3` | **Nota en expansión**: misma nota replicada en N fuentes, con origen, cadena y minutos |
| `GET /api/v1/reloj` | **Reloj de la noticia**: quién publicó primero y cuánto tardó cada medio |
| `GET /api/v1/gaps` | **Cobertura gap**: temas que se cubren en el país y casi nadie cubre en esa provincia |
| `GET /api/v1/mapa` | **Mapa de calor** provincial en JSON |
| `GET /api/v1/primicias` | Solo la fuente que fue **primera** en publicar cada nota |
| `GET /api/v1/huerfanas` | Notas de **una sola fuente** → posible exclusiva |
| `GET /api/v1/sources` | Catálogo de fuentes (editorial + YouTube) |
| `GET /api/v1/quotes` | Citas directas extraídas de la nota |
| `GET /api/v1/health` | Version y estado |

### Filtros de `/api/v1/items`

`provincia`, `region`, `tipo`, `tema`, `clusters`, `huerfanas`, `primicia`, `gap`,
`min_fuentes`, `sin_video`, `ventana` (`15m|1h|6h|24h|48h`), `orden` (`fecha|n_fuentes|velocidad`),
`fuente`, `search`, `page`, `page_size`.

### Señales por item

| Campo | Significado |
|---|---|
| `firma` | Hash del título normalizado (agrupa la misma nota) |
| `cluster_id` | Agrupador de "nota en expansión" |
| `n_fuentes` | Cuántas fuentes distintas replicaron |
| `es_primicia` | Esta fuente publicó primero |
| `es_huerfana` | Nadie más la replicó (posible exclusiva) |
| `velocidad_min` | Minutos desde la publicación original |
| `es_gap` | Tema cubierto nacionalmente pero no en su provincia |
| `tema` | Agenda: seguridad · política · servicio · economía · deportes · cultura · general |

### Ejemplos

```bash
# Notas de Salta en expansión, con 3+ fuentes
curl -H "X-API-Key: $KEY" "https://apifenix.mp4-render.site/api/v1/clusters?provincia=AR-A&min_fuentes=3"

# Qué se publicó en las últimas 6 horas y nadie replicó (exclusivas posibles)
curl -H "X-API-Key: $KEY" "https://apifenix.mp4-render.site/api/v1/huerfanas?ventana=6h"

# Reloj de la noticia: origen y demoras por medio
curl -H "X-API-Key: $KEY" "https://apifenix.mp4-render.site/api/v1/reloj?search=inundaci"
```

---

## 4. Portal de usuario

Todo vive dentro de la cuenta (nunca hace falta salir del panel):

| Ruta | Función |
|---|---|
| `/` | Landing con muestras reales del radar |
| `/registro`, `/login`, `/auth/google` | Acceso |
| `/portal` | Panel: stats, keys, consumo, feed con señales |
| `/portal/nota/{id}` | **Lector integrado**: foto o player de YouTube embebido, texto, etiquetas de señal, botón *Resumir con mi agente* y *Analizar ángulo* |
| `/portal/canales` | **Canales de YouTube** del radar: filtro por canal/provincia + últimos videos |
| `/portal/buscar?q=` | **Buscador** en título, bajada y fuente, con ventanas 15m→48h |
| `/mapa` | Mapa de calor provincial (público) |
| `/mural` | Mural con etiquetas periodísticas + filtro por agenda (público) |
| `/tablero` | Tableros guardados (filtros como JSON) |
| `/portal/agente` | Agente de redacción IA con tu propia API key |
| `/portal/placas` | Diseñador de placas 1080×1350, exportación PNG |
| `/portal/fuentes` | Proponer fuente al radar |
| `/portal/recorder` | **FENIX Recorder**: grabación de pantalla/pestaña/cámara 100% en tu navegador |
| `/portal/publicar` | **Publicar en PRENSA** (requiere contrato firmado + identidad documentada) |
| `/catalogo` | Catálogo público de fuentes |

El lector abre el video con `youtube-nocookie.com/embed` (sin cookies de
terceros) y los relacionados son de la misma provincia.

---

## 5. Inteligencia 100% del lado del navegador

El análisis de sentimiento por entidad, framing/sesgo y temas IPTC corre con
**Transformers.js en el navegador del periodista** (caché IndexedDB): el server
solo sirve datos indexados, nunca modelos ni inferencia. Por el mismo principio,
**FENIX Recorder** graba con MediaRecorder y guarda los videos en IndexedDB —
al server solo viaja la ficha (título, duración, peso, hash SHA-256) para el
historial.

---

## 6. Límites del plan gratuito

| | Valor |
|---|---|
| Requests por minuto | 30 |
| Requests por día | 5.000 |
| Vigencia de la key | hasta rotarla vos |

Los planes de pago se lanzan con la API Premium; por ahora el acceso es gratis
con registro.
