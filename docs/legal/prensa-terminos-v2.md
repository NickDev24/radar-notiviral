# CONDICIONES DE PUBLICACIÓN — PRENSA NOTIVIRAL
### Versión: **v2** · Vigente desde 2026-10-03 · **Sustituye a la v1** · Radar Notiviral / API FENIX

> Este documento es el contrato que todo usuario debe aceptar, con hash
> criptográfico propio, antes de publicar en `prensa.radar-notiviral.online`.
> La aceptación se registra en `fenix_api.legal_consents` con IP, user-agent,
> fecha/hora y versión exacta. Cada nota publicada queda sellada contra el
> hash de ese consentimiento: la cadena probatoria es inmutable.

---

## 1. Definiciones y naturaleza de la plataforma

1.1. **Radar Notiviral / API FENIX** (en adelante, "la Plataforma") es un
**intermediario de servicios tecnológicos** que provee infraestructura de
alojamiento, indexación y distribución automatizada de contenidos. La
Plataforma **no es autora, editora, ni directora responsable** del contenido
publicado por los usuarios en el medio comunitario `prensa.radar-notiviral.online`.

1.2. **Usuario-Publisher** (en adelante, "el/la Publicador/a") es la persona
humana o jurídica que crea una cuenta, acepta estas condiciones y sube
contenidos. El/la Publicador/a es **titular y único/a responsable** editorial
de todo lo que publica, conforme al art. 23 de la Ley 11.723 (propiedad
intelectual) y al régimen de responsabilidad de la Ley 26.032 y del Código
Civil y Comercial de la Nación.

1.3. La Plataforma actúa por **delegación técnica automatizada**: no revisa,
no selecciona, no recomienda ni edita el contenido humano más allá de los
filtros automáticos de spam/toxicidad descriptos en la cláusula 6, los cuales
se aplican sin conocimiento real del caso y no implican curaduría editorial.

---

## 2. Declaración jurada del Publicador (condición esencial de habilitación)

2.1. Al aceptar estas condiciones y al publicar cada nota, el/la Publicador/a
**declara bajo juramento**, conforme al art. 24 de la Ley 11.723:

a) que el contenido publicado es **de su autoría** o que **dispone de los
derechos de reproducción, difusión y comunicación pública** suficientes para
publicarlo en todo territorio y por toda la vida del medio;

b) que el contenido **no viola derechos de terceros**: ni propiedad intelectual
(plagio), ni derechos de imagen, ni datos personales (Ley 25.326), ni secreto
profesional, judicial o de sumarios en curso de reserva;

c) que **no publica a sabiendas información falsa** con capacidad de causar
daño público o privado (desinformación), ni contenido destinado a acoso,
incitación a la violencia o discriminación (Ley 23.592);

d) que las fuentes citadas son **reales y verificables** y que conserva los
respaldos (grabaciones, documentos, capturas) por el plazo de prescripción
civil y penal aplicable, obligándose a presentarlos si la Plataforma se los
reclama por denuncia de tercero;

e) que **no utiliza el medio para fines de proselitismo pago encubierto,
publirreportaje sin etiquetar, ni campañas de desprestigio coordinadas**.

2.2. La aceptación del punto 2.1 es **condición tecnológica y contractual
sine qua non**: el sistema deniega el alta de cualquier nota si no existe un
consentimiento activo y vigente de la versión en curso del contrato (código
`CONSENTIMIENTO_FALTANTE`, HTTP 412).

2.3. **Identificación previa (v2)**: además de la firma digital del
consentimiento, para quedar habilitado como Publicador se exige **cargar un
documento de identidad propio y vigente** — DNI argentino (frente y dorso) o
pasaporte — a través del panel (`/portal/publicar`). La imagen se almacena
**fuera del ámbito público**, sellada con su hash SHA-256, IP, user-agent y
marca temporal, y **no puede ser editada ni borrada** por el Publicador ni
por operadores de la Plataforma (trigger de congelamiento en base de datos).
Sin identidad acreditada, el sistema deniega el alta de notas con código
`DOCUMENTOS_FALTANTES` (HTTP 412), también a nivel de la propia base.

---

## 3. Exención de responsabilidad de la Plataforma (intermediario tecnológico)

3.1. El/la Publicador/a **asume personal, exclusiva y solidariamente con sus
eventuales codifusores** toda responsabilidad **civil, penal, administrativa y
por derechos de autor** que derivara del contenido publicado, incluyendo
reclamos por difamación, injuria, calumnia, violación de privacidad,
plagio, competencia desleal, daño moral y desinformación.

3.2. El/la Publicador/a **mantendrá indemne (cláusula de resarcimiento/
*hold harmless*) a la Plataforma**, a sus titulares, dependientes y
proveedores frente a todo reclamo, denuncia, mediación o demanda de terceros
originada en su contenido, **asumiendo gastos de defensa, settlement e
indemnizaciones** que resultaren.

3.3. La Plataforma **no garantiza** veracidad, exactitud ni legalidad del
contenido del Publicador, y **no emite aval editorial alguno**. La aparición
de una nota en `prensa.radar-notiviral.online` no constituye verificación ni
endorsamiento por parte de la Plataforma.

3.4. En la medida permitida por la ley argentina, la consiente expresamente
con el art. 1112 y cc. del C.C.y.C.: la única relación sustantiva por el
contenido es **entre el/la Publicador/a y los terceros afectados**; la
Plataforma es sujeto procesal pasivo solo en su calidad de alojador, con las
obligaciones de hacer cesar el hecho lesivo una vez mediando **noticia
acreditada e idónea** (art. 21 de la Ley 11.723, doctrina "criterio de la
conducta" — *Telerman, M. c/ Google Inc.*).

---

## 4. Cesión de derechos a la Plataforma (para operar el servicio)

4.1. El/la Publicador/a concede a la Plataforma una licencia **no exclusiva,
gratuita, transferible a sucesores técnicos**, por el plazo de publicación y
retención legal, con derecho a: almacenar, indexar, citar, compendiar y
mostrar el contenido en el medio y en los productos derivados (API, RSS,
módulos analíticos), siempre **manteniendo el seudónimo/crédito** declarado.

4.2. Los derechos morales de autor **permanecen intactos** (art. 22 Ley
11.723, irrenunciables); el Publicador conserva la titularidad de los
patrimoniales y puede retirar su contenido (cláusula 8).

---

## 5. Identidad, seudónimo y trazabilidad

5.1. La Plataforma registra por cada consentimiento y por cada nota: **IP de
origen, user-agent, marca temporal, hash SHA-256 del cuerpo y hash único del
consentimiento**. Esta bitácora es la base de la defensa del intermediario y
será conservada por **el plazo de prescripción de acciones derivadas del
contenido (10 años reales y personales; art. 2562/4037 C.C.y.C. y regímenes
especiales)**, sin divulgación pública.

5.2. El/la Publicador/a puede actuar con **seudónimo** declarado en su
perfil de prensa; el seudónimo **no oculta la identidad ante requerimiento
judicial**, que la Plataforma podrá atender conforme a la ley.

5.3. Datos personales tratados conforme a **Ley 25.326** y su reglamento;
el Publicador otorga consentimiento específico para el tratamiento descrito
en esta cláusula y puede ejercer acceso/rectificación/supresión ante
contacto legal indicado en el aviso legal del medio, **con la siguiente
excepción**: los documentos de identidad de la cláusula 2.3 y los
consentimientos de la cláusula 5.1 son **prueba legal inmutable** y se
conservan aún ante pedido de supresión de cuenta, por el plazo de
prescripción (art. 2562/4037 C.C.y.C.), a solo efecto de defensa de la
Plataforma y atención de requerimientos judiciales.

5.4. El Publicador declara que el documento de identidad cargado **le
pertenece, es auténtico y está vigente**, y que las imágenes son suyas o
cuenta con consentimiento de su titular. La carga de un documento ajeno o
adulterado es incumplimiento grave y habilita la baja del perfil sin
desmedro de las acciones legales por suplantación (art. 175 CP).

---

## 6. Moderación asíncrona automatizada (sin curaduría)

6.1. Toda nota nace con estado `pending_review` y pasa por un **filtro
automático** de spam/enlace malicioso/toxicidad. Resultado posible:
`published` (pasa al feed público) o `rejected` (no se distribuye; el motivo
técnico queda en registro privado y se notifica al Publicador sin
detallarlo en público).

6.2. El filtro es una medida **de higiene técnica de la plataforma, no de
censura editorial**; su existencia y sus resultados **no otorgan ni implican
conocimiento real** del contenido a efectos de responsabilidad de
intermediario.

---

## 7. Reporte y política de remoción (*notice & takedown*)

7.1. Cualquier persona puede denunciar una nota por **copyright, plagio,
difamación, desinformación o violación de privacidad** desde el endpoint
`POST /api/v1/notes/{id}/report` (o el formulario público del medio), con
nombre y contacto cuando se trate de un **reclamo de derechos de autor**.

7.2. Efectos automáticos:
- **Reclamo de copyright/plagio** con identifiación del reclamante: la nota
  pasa **de inmediato** a `preventive_block` (se retira del feed público y
  queda no-indexable para buscadores mientras se resuelve la disputa, en
  términos análogos al procedimiento DMCA / art. 21 Ley 11.723);
- **Tres (3) o más denuncias válidas de IPs distintas** sobre la misma nota:
  `preventive_block` automático igualmente, sin esperar resolución.

7.3. El/la Publicador puede **subsanar**: aportar documentación de
titularidad/derechos o editar la nota; la Plataforma restablece el estado a
`pending_review` para revalidación automática. La reincidencia (2 bloqueos
por la misma causa) implica **baja del perfil de prensa**.

7.4. Un requerimiento judicial o mediación previa acreditada ordena
remoción definitiva (`retirada`) y conservación de la bitácora 5.1 por el
plazo legal.

---

## 8. Retiro voluntario y portabilidad

8.1. El/la Publicador puede retirar una nota propia en cualquier momento
(estado `retirada`: desaparece del feed; se conserva internamente por
trazabilidad legal 5.1). Sus contenidos propios son exportables en JSON.

---

## 9. Ceses, suspensiones y cambios de contrato

9.1. La Plataforma puede suspender cuentas que incumplan estas condiciones,
**sin efecto retroactivo sobre la trazabilidad** ya registrada.

9.2. Toda nueva versión del contrato exige **nuevo consentimiento con hash
propio** antes de habilitar publicaciones: el sistema no permite publicar
bajo consentimiento de versión vencida.

---

## 10. Ley aplicable y jurisdicción

10.1. Estas condiciones se rigen por las leyes de la **República Argentina**
(Leyes 11.723, 25.326, 26.032, 23.592, 24.071 y C.C.y.C.). Para controversias
entre Publicador y Plataforma: **fuero civil y comercial de la Ciudad
Autónoma de Buenos Aires**, con intento previo de mediación (Ley 24.787 en
cuanto resulte aplicable).

---

*Documento canónico: `docs/legal/prensa-terminos-v2.md`. Versión: `v2` (incorpora la exigencia de identificación de la cláusula 2.3; la v1 queda como evidencia histórica y no se edita).*
Al aceptar, el sistema calcula
`SHA-256(usuario | versión | ip | user-agent | timestamp)` y lo guarda como
`hash_consentimiento` — prueba única e inmutable de esta firma digital.*
