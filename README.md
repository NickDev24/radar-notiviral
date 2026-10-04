# Radar Notiviral — API de noticias de Argentina 🇦🇷

**Radar Notiviral (APIFENIX) es una API de noticias argentinas en tiempo real: radar de noticias de las 23 provincias, con señales periodísticas (primicias, notas en expansión, huérfanas y coverage gaps (notas sin cubrir)) para periodistas, redacciones y desarrolladores.**

## 🪽 APIFENIX — El radar de noticias de Argentina 🇦🇷

> **La API que le dice a un periodista: esto se está expandiendo, esto lo publicó primero nadie, y esto no lo está cubriendo nadie.**

[![API en vivo](https://img.shields.io/badge/API-radar-notiviral.online-10b981?style=flat-square&logo=fastapi)](https://radar-notiviral.online/api)
[![Hecho en Argentina](https://img.shields.io/badge/hecho%20en-Argentina-%F0%9F%87%A6%F0%9F%87%B7-celeste?style=flat-square)](#)
[![Licencia](https://img.shields.io/badge/licencia-MIT-blue?style=flat-square)](LICENSE)

Este repositorio es la **cara pública del proyecto**: documentación, presentación
y videos tutoriales. El código de la plataforma es privado.

- 📘 [Documentación de la API](docs/API.md)
- 🎬 [Videos tutoriales](docs/TUTORIALES.md)
- 📄 [Presentación en PDF](docs/Radar_Notiviral_y_APIFENIX.pdf)
- ⚖️ [Términos legales de PRENSA Notiviral](docs/legal/prensa-terminos-v2.md)

---

## 🔥 Qué la hace ÚNICA

No es un agregador de noticias. Es un **motor de inteligencia periodística** para las 23 provincias argentinas:

| Señal | Qué significa | Por qué importa al periodista |
|---|---|---|
| 🛰️ **Nota en expansión** | La misma nota ya la replicaron 2+ fuentes | Te dice cuándo una noticia se está haciendo **nacional** |
| 🥇 **Primicia** | La fuente que publicó primero | Permite citar "primero informó X" |
| ⏱️ **Reloj de la noticia** | Minutos entre la publicación original y cada réplica | Mide la velocidad de cada medio |
| 🎯 **Nota huérfana** | Una sola fuente, nadie la replicó | **Posible exclusiva tuya** |
| 🕳️ **Cobertura gap** | Tema con poca cobertura nacional | **Dónde hay nota y no hay columna** |

Nada de esto existe en APIs genéricas. Es 100% construido end-to-end por un periodista argentino sobre fuentes reales del país.

---

## 🚀 Quickstart (60 segundos)

```bash
# 1. Registrate y obtené tu key
curl -X POST https://radar-notiviral.online/registro   # o /auth/google

# 2. Explorá el radar (con header X-API-Key)
curl -H "X-API-Key: TU_KEY" "https://radar-notiviral.online/api/v1/items?provincia=AR-A&page_size=5"
```

**Sin key, mirá el radar igual:**
- 🗺️ [Mapa de calor en vivo](https://radar-notiviral.online/mapa)
- 🗞️ [Mural de noticias](https://radar-notiviral.online/mural)
- 📰 [Catálogo de fuentes](https://radar-notiviral.online/catalogo)

---

## 📡 Endpoints del Motor Radar v2

```
GET /api/v1/items         Filtros: provincia, region, tipo, tema, clusters,
                          huerfanas, primicia, gap, min_fuentes, ventana,
                          sin_video, orden, search
GET /api/v1/clusters      Notas EN EXPANSIÓN (de dónde salió, cuántas fuentes, en qué minutos)
GET /api/v1/reloj         Reloj de la noticia: quién publicó primero y cuánto tardó cada medio
GET /api/v1/gaps          Cobertura gap: qué temas NO cubre nadie (oportunidad)
GET /api/v1/mapa          Mapa de calor provincial en JSON
GET /api/v1/primicias     Solo la fuente que fue primera en cada nota
GET /api/v1/huerfanas     Notas con 1 sola fuente (posible exclusiva)
GET /api/v1/sources       Catálogo de fuentes (editorial + YouTube)
```

Documentación interactiva: [api/docs](https://radar-notiviral.online/api/docs) · Esquema: [openapi.json](https://radar-notiviral.online/api/openapi.json) · Referencia completa: [docs/API.md](docs/API.md)

---

## 🧩 Integraciones

- **SDK Python** y **SDK JavaScript** — incluidos con tu API key (ver portal)
- **Servidor MCP** para agentes de IA (Claude Desktop, Cursor)
- **Plugin n8n** — webhook listo desde el panel

```python
from apifenix import ApiFenix
radar = ApiFenix("TU_KEY")

# ¿Qué se está expandiendo AHORA?
for c in radar.clusters(min_fuentes=3):
    print(c["titulo"], "→", c["n_fuentes"], "fuentes")

# ¿Dónde no cubre nadie?
for g in radar.gaps(provincia="AR-Y"):
    print("Oportunidad:", g["tema"], g["titulos"][0]["titulo"])
```

---

## 🎨 Extras del portal de usuario

- 🤖 **Agente de redacción IA** — conectá TU propia API key (OpenAI / OpenRouter / Groq / Gemini / Claude), cifrada en reposo, con tono, largo, formato y público ajustables; chat por nota con contexto del radar y tus apuntes.
- 📝 **Mis Notas** — todo lo que redactás en el bloc queda listo para retomar o pasarle al agente.
- 🧠 **Inteligencia IA** — sentimiento por entidad, framing, temas IPTC y clusters: el ML corre 100% en tu navegador (Transformers.js) con caché IndexedDB; el server solo sirve datos indexados.
- 🎥 **FENIX Recorder** — grabá pantalla/pestaña/cámara o reacción con cámara en tu navegador (MediaRecorder + IndexedDB); al server solo le llega la ficha (duración, peso, hash). Desde cada nota de YouTube: botón **"Grabar esta nota"**.
- 🎨 **Diseñador de placas** 1080×1350 con preview en vivo y descarga PNG.
- 📡 **Sumá tu fuente al radar** — los usuarios proponen medios, el admin aprueba, alimenta a todos.
- 📌 **Tableros guardados** — guardá filtros y volvé a ellos.
- 📰 **Feed con etiquetas** — el mismo contenido que la API, con señal periodística visible.

---

## 🗞️ PRENSA Notiviral — el medio libre

- **prensa.radar-notiviral.online**: periodistas independientes publican notas firmadas. Cada alta exige consentimiento explícito del contrato vigente (**hash único + IP + fecha-hora + versión**) e **identidad acreditada con documento** (DNI frente+dorso o pasaporte).
- **Responsabilidad exclusiva del autor**: la plataforma opera como intermediario tecnológico (declaración jurada de autoría/derechos, Ley 11.723) — texto canónico en [docs/legal/](docs/legal/prensa-terminos-v2.md) y en `/prensa/terminos`.
- **Moderación asíncrona**: las notas nacen `pending_review`; un worker de heurísticas locales las publica o las rechaza con motivo técnico privado.
- **Take-down en milisegundos**: `POST /api/v1/notes/{id}/report` — con 3 IPs distintas o un reclamo de copyright la nota pasa a bloqueo preventivo atómico y desaparece del feed y del índice de Google.

---

## 🏗️ Arquitectura (visión pública)

```
  Fuentes RSS + YouTube (23 provincias)
            │  ingesta c/15min
            ▼
     Motor Radar v2  ── clusters · primicias · huérfanas · reloj · gaps
            │
            ▼
    PostgreSQL  ──────  Redis (rate limit + cuotas)
            │
            ▼
      FastAPI pública  ──►  Portal  ·  Docs interactivas  ·  MCP
```

- **Stack**: FastAPI · SQLAlchemy · PostgreSQL · Redis · feedparser · APScheduler
- **Auth**: API keys hasheadas (SHA-256) + Google OAuth + verificación por email
- **Privacidad por diseño**: el ML de análisis corre en el navegador del periodista y la grabación de video (Recorder) jamás toca el servidor

---

## 🎬 Presentación en video (se reproduce en el navegador, sin descarga)

**[▶ Ver el demo de Radar Notiviral y APIFENIX (6:58, narrado por IA)](https://radar-notiviral.online/static/videos/demo-notebooklm.mp4)** — qué es el radar, cómo leer las señales y cómo empezar con la API gratis. Se abre en la misma pestaña con el reproductor nativo del navegador.

📄 **La presentación completa en PDF**: [Radar Notiviral y APIFENIX](docs/Radar_Notiviral_y_APIFENIX.pdf) (GitHub abre el lector de PDF en la misma pestaña).

Además: [tutorial técnico de la API paso a paso](https://github.com/NickDev24/radar-notiviral/blob/main/videos/api_tutorial_16x9.mp4) (28 MB, en `videos/`). Más detalle en [docs/TUTORIALES.md](docs/TUTORIALES.md).

---

## 🇦🇷 Identidad

APIFENIX es **API ARGENTINA**: fuentes reales de las 23 provincias, español rioplatense, y un producto pensado para el periodismo del país. Si tenés un medio, un canal o una radio: [sumalo al radar](https://radar-notiviral.online/registro).

## 📄 Licencia

MIT — ver [LICENSE](LICENSE). Los textos legales de PRENSA Notiviral (`docs/legal/`) son de publicación obligatoria y rigen las relaciones con los usuarios del medio.
