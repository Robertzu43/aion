# Aion — Design Spec (v1)

**Fecha:** 2026-07-19
**Autor:** Roberto Zuniga
**Estado:** Aprobado (diseño) — pendiente de plan de implementación
**Contexto:** Entrega para el reto de Platzi "Claude Code para no programadores".

> **Nota (actualización posterior):** Este spec es el diseño original. Después de
> usarlo, el **dashboard HTML** se reemplazó por **tendencias en el chat**
> (sparklines/tablas) y se eliminó el comando `/aion-dashboard`; además se agregó
> un arranque automático del check-in vía un hook `SessionStart`. Fuente de verdad
> actual: `README.md`, `CLAUDE.md`, los comandos y el skill `aion`.

---

## 1. Resumen

**Aion** es un **agente de IA personal que vive como un proyecto de Claude Code**: clonas el repo, lo abres en Claude Code y lo usas con comandos. Cada mañana corres un comando, Aion hace un **check-in conversacional anclado en tus datos reales**, cruza tu descanso, tu entrenamiento, tu aprendizaje y las noticias de tu campo, y te arma el **día óptimo**. Guarda el historial y genera un **dashboard HTML** con gráficas de tu evolución.

El "cerebro" es **Claude Code mismo**, autenticado con la suscripción del usuario (Pro/Max) — **sin API keys, sin costo por token, sin backend**. Todo corre local.

Se adapta al contexto: si trasnochaste, mueve el entreno y reordena el estudio; si vas atrasado en una meta, prioriza; si un ejercicio se estancó en peso, lo señala.

## 2. Objetivos y no-objetivos

### Objetivos (v1)
- Loop diario redondo: **check-in contextual → día optimizado**.
- **Historial persistente en archivos** + **dashboard HTML con gráficas** de descanso, entrenamiento (progresión de cargas + adherencia) y aprendizaje.
- **Publicable y usable por cualquiera** con Claude Code + suscripción, de cualquier profesión.
- **Privacidad total**: los datos personales nunca salen del repo local del usuario.

### No-objetivos (v1)
- App web o móvil.
- Integración en vivo con Apple Watch / wearables por API (imposible sin app nativa — ver §8).
- Backend, cuentas o base de datos en la nube.
- Uso de API key de Anthropic / cobro por tokens (se usa la suscripción vía Claude Code).

## 3. Decisiones de arquitectura (y por qué)

| Decisión | Elección | Razón |
|---|---|---|
| Plataforma | **Proyecto de Claude Code** (comandos + skill + CLAUDE.md) | Es exactamente lo que el reto evalúa; el cerebro es Claude Code. |
| Cerebro / auth | **Claude Code con la suscripción del usuario** | Sin API keys ni costo por token. (La suscripción Pro/Max **no** sirve para apps de terceros vía API — solo para Claude Code; ver §8.) |
| Persistencia | **Archivos locales** en `data/` (JSON + Markdown) | Privacidad máxima, cero infra; Claude Code lee/escribe archivos de forma nativa. |
| Privacidad | `data/` real en `.gitignore`; se publican **plantillas** | Repo publicable sin exponer datos personales. |
| Noticias del campo | **WebSearch integrado de Claude Code** | Sin API de noticias, sin CORS; configurable por profesión. |
| Dashboard | **HTML autocontenido** (skill `dataviz`) abierto en navegador | Gráficas bonitas e interactivas, sin dependencias externas. |
| Distribución | **Repo de GitHub** (`aion`) | Cualquiera clona, corre `/aion-setup` y empieza. |

## 4. Estructura del repo

```
aion/
├─ CLAUDE.md                      # Orienta a Claude Code: qué es Aion, cómo usar los archivos
├─ README.md                      # Guía para no programadores: instalar Claude Code, clonar, /aion-setup
├─ .gitignore                     # Ignora data/ real (solo plantillas se publican)
├─ .claude/
│  ├─ commands/
│  │  ├─ aion-setup.md            # Configura perfil, metas, horario, campos de interés, rutina
│  │  ├─ aion.md                  # Check-in matutino + genera el día
│  │  ├─ aion-platzi.md           # Parsea un SingleFile de Platzi al historial de aprendizaje
│  │  └─ aion-dashboard.md        # Genera el dashboard HTML con gráficas
│  └─ skills/
│     └─ aion/SKILL.md            # Lógica de razonamiento/optimización de Aion
├─ data/                          # (gitignored) datos reales del usuario
│  ├─ perfil.json
│  ├─ rutina-entrenamiento.md     # o PDF
│  ├─ entrenamiento-log.json      # sesiones + pesos por ejercicio
│  ├─ checkins.json               # historial diario (sueño, energía, notas)
│  ├─ aprendizaje.json            # snapshots de progreso Platzi
│  ├─ dias/                       # planes del día generados
│  └─ platzi/                     # SingleFiles crudos
└─ data.ejemplo/                  # (commiteado) plantillas de ejemplo para arrancar
```

## 5. Componentes (comandos y skill)

1. **`/aion-setup`** — configuración inicial (idempotente/actualizable).
   - Captura: metas, horario fijo (ej. trabajo 8–4), tracker que usa, **campo(s) de interés** para noticias, y la **rutina de entrenamiento** (pega texto o coloca un PDF/`.md` en `data/`).
   - **Bootstrap en un clon nuevo:** `/aion-setup` **crea el árbol `data/`** (incluyendo subcarpetas `dias/` y `platzi/`) y **genera los archivos desde cero** a partir de la conversación — inicializa `entrenamiento-log.json`, `checkins.json` y `aprendizaje.json` como arreglos vacíos `[]`. **No copia** desde `data.ejemplo/`: esa carpeta es solo **referencia commiteada** para que un recién llegado vea la forma esperada de cada archivo.
   - Escribe `perfil.json` y `rutina-entrenamiento.md`.
   - **Idempotente:** si `perfil.json` ya existe, actualiza los campos indicados sin sobrescribir el historial ni corromper el archivo.

2. **`/aion-platzi`** — ingiere un SingleFile de Platzi.
   - Entrada: HTML exportado con la extensión SingleFile, colocado en `data/platzi/`.
   - Extrae cursos, **% de progreso**, **racha** y completados → añade snapshot a `aprendizaje.json`.
   - Validado contra un archivo real (contiene cursos, %, "Streak", "Progreso", "Completado"). Tolerante: si el HTML cambió, cae a captura manual.

3. **`/aion`** — el comando estrella (check-in matutino + día óptimo).
   - **Check-in anclado en datos reales** (ver §6): Aion lee la rutina + `entrenamiento-log.json` de la semana antes de preguntar.
   - Cruza descanso + entrenamiento + progreso Platzi + metas + noticias del campo (WebSearch).
   - Escribe el **plan del día** en `data/dias/AAAA-MM-DD.md` y actualiza logs.
   - **Contrato del plan del día** (secciones obligatorias, siempre en este orden):
     1. **Resumen del día** — una línea con el foco del día.
     2. **Ventana de entrenamiento** — hora/intensidad recomendada y por qué.
     3. **Plan de estudio** — qué curso/lección de Platzi y cuánto tiempo.
     4. **Digest del campo** — 2–4 noticias del campo de interés (con enlace si hay).
     5. **Adaptaciones** — qué cambió hoy y por qué (ej. "trasnochaste → entreno movido a la tarde").
     Si una sección no aplica (ej. sin internet → sin digest), se incluye igual con una nota explícita; nunca se omite del todo.

4. **`/aion-dashboard`** — genera `dashboard.html` autocontenido con gráficas y lo deja listo para abrir en el navegador.

5. **Skill `aion`** — contiene la lógica de razonamiento: cómo prioriza, cómo adapta el día ante un trasnoche, cómo detecta estancamiento de cargas, cómo pondera metas. Los comandos la invocan.

6. **`CLAUDE.md`** — describe el proyecto, la estructura de `data/` y las convenciones para que Claude Code opere consistente en cada sesión.

## 6. El check-in contextual (núcleo del ajuste clave)

Aion **no hace preguntas genéricas**. Antes de preguntar, lee `rutina-entrenamiento.md`, `entrenamiento-log.json` (semana en curso) y `checkins.json`. Luego:

- **Sueño (anclado en el tracker):** pregunta por las **horas** y la **calidad/score** que marcó el wearable anoche (el usuario las lee de su tracker y las reporta). Las guarda para la tendencia.
- **Entrenamiento (anclado en rutina + semana):** pregunta con contexto específico, p. ej. *"Ayer tocaba pierna según tu rutina. ¿Lo hiciste? ¿Qué levantaste en sentadilla y peso muerto?"* — y **registra los pesos por ejercicio** en `entrenamiento-log.json`.
- **Energía y contexto:** energía hoy (1–5) y si hubo algo inusual (trasnoche, viaje, lesión).

**Cruce que hace Aion con eso:**
- Rutina **prescrita** vs **realizada** esta semana (adherencia).
- **Progresión de cargas** por ejercicio (¿subió, se mantuvo, se estancó?).
- Descanso reciente vs carga → recomienda ventana e intensidad de entreno hoy.
- Progreso Platzi vs metas → recomienda qué estudiar y cuánto.

## 7. Modelo de datos (borrador)

```jsonc
// perfil.json
{
  "camposDeInteres": ["Inteligencia Artificial"],
  "horarioFijo": { "trabajoInicio": "08:00", "trabajoFin": "16:00" },
  "tracker": "Apple Watch",
  "metas": ["3 entrenos/semana", "terminar ruta de IA en Platzi"]
}

// entrenamiento-log.json  (una entrada por sesión)
[{ "fecha": "2026-07-18", "diaRutina": "Pierna", "hecho": true,
   "ejercicios": [{ "nombre": "Sentadilla", "series": [{ "reps": 5, "kg": 100 }] }] }]

// checkins.json
// suenoCalidad: enum fijo -> "mala" | "regular" | "buena" | "excelente"
// energia: entero 1-5
[{ "fecha": "2026-07-19", "suenoHoras": 5.5, "suenoCalidad": "mala",
   "energia": 2, "notas": "trasnoché" }]

// aprendizaje.json  (snapshot por ingesta de SingleFile)
[{ "fecha": "2026-07-19", "racha": 12,
   "cursos": [{ "titulo": "Curso de Fundamentos de IA", "progresoPct": 70 }] }]

// data/dias/2026-07-19.md  -> plan del día (ventana de entreno, plan de estudio, digest, adaptaciones)
```

## 8. Restricciones verificadas (investigación)

- **Suscripción Claude Pro/Max:** autentica **Claude.ai** y **Claude Code**, **no** apps de terceros vía API. No existe un "login con Claude" para que una web externa gaste contra la suscripción. Por eso Aion vive **dentro de Claude Code** (así sí aprovecha la suscripción).
- **API de Anthropic:** se cobra aparte (API key / créditos). Descartada para evitar costo/fricción; se usa la suscripción vía Claude Code.
- **Apple Watch / HealthKit:** solo nativo iOS/watchOS; no hay API web ni server-to-server. Por eso el descanso/entreno entra por el **check-in** (el usuario lee su tracker), no por integración en vivo.
- **Platzi:** sin API pública oficial → enfoque **SingleFile HTML**, validado con archivo real.
- **Noticias:** resueltas con el **WebSearch** integrado de Claude Code; campo configurable por profesión/ocupación.

## 9. Manejo de errores / bordes
- **Falta setup** → si no existe `perfil.json`, `/aion` sugiere correr `/aion-setup` primero.
- **SingleFile cambió/ilegible** → parseo tolerante; fallback a captura manual de cursos/progreso.
- **Sin internet** → el día se genera igual; el digest de noticias se omite con aviso.
- **Datos incompletos del día** → Aion pregunta solo lo que falta; nunca inventa pesos ni horas.
- **PDF de rutina ilegible** → permitir pegar la rutina como texto en `rutina-entrenamiento.md`.

## 10. Estrategia de pruebas
- **Parser de SingleFile:** verificar extracción de cursos/%/racha con el archivo real como fixture.
- **Contrato del día:** `/aion` siempre produce un `data/dias/AAAA-MM-DD.md` con las secciones esperadas y actualiza los logs.
- **Dashboard:** `dashboard.html` renderiza con un historial de muestra (sueño, cargas, adherencia, Platzi).
- **Setup idempotente:** correr `/aion-setup` dos veces no corrompe `perfil.json`.

## 11. Fuera de alcance / v2 (ideas)
- Check-in nocturno / reflexión del día.
- Recordatorios/notificaciones.
- Integración opcional con wearables de OAuth en la nube (Garmin/Oura/Whoop vía Terra/ROOK) para quien los tenga.
- Sincronización multi-dispositivo cifrada (opt-in).

## 12. Riesgos y mitigaciones
- **Fragilidad del parser de Platzi** (el HTML puede cambiar) → parseo tolerante + fallback manual + fixture.
- **Requiere Claude Code + suscripción** para usarse → documentado claramente en el README; es coherente con el reto.
- **Datos personales** → `data/` en `.gitignore`; solo plantillas de ejemplo se publican.

## 13. Nombre
Repo y proyecto: **`aion`**.
