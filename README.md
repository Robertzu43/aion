# Aion

Aion es tu agente personal para armar, cada mañana, tu día óptimo. Cruza tu
descanso, tu entrenamiento, tu aprendizaje en Platzi y las noticias de tu
campo de interés, y te entrega un plan claro para hoy.

Corre dentro de **Claude Code**, usando tu propia suscripción de Claude. No
necesitas API keys, no necesitas montar ningún servidor: instalas Claude
Code, abres esta carpeta, y listo.

## Por qué se llama Aion

**Aion** (griego *Αἰών*) es la deidad del **tiempo eterno y cíclico** —la vida
que se renueva ciclo tras ciclo—, a diferencia de *Chronos*, el tiempo lineal
del reloj. El nombre encaja con la idea del proyecto: Aion no te apura minuto a
minuto; trabaja sobre tus **ciclos diarios** y tu **evolución en el tiempo**.
Cada día es una vuelta del ciclo —descansas, entrenas, aprendes— y Aion te ayuda
a que cada vuelta sume a la siguiente.

## Qué es Aion

Aion es un agente personal que cada mañana revisa cómo dormiste, qué toca en
tu rutina de entrenamiento, cómo va tu progreso en Platzi y las noticias de
tu campo de interés, y con todo eso te propone el mejor plan para tu día.
No es una app ni un dashboard en la nube: es un conjunto de instrucciones
que corre directamente dentro de Claude Code, en tu computadora, usando tu
suscripción de Claude. Sin API keys, sin servidores, sin nada que instalar
además de Claude Code.

## Cómo se ve

Una mañana con Aion se ve más o menos así (los datos son de ejemplo):

```
Tendencias (últimos días)
  Sueño   ▅▃▂▁▃▆▇   prom 6.8h
  Energía ▄▄▃▂▃▄▅   hoy 4/5
  Adherencia (sem) ██░ 2/3
  Sentadilla 25→30 kg ▲    Platzi 🔥 9 · 3%→23%

Tu día
  1. Resumen — día de foco medio; hoy priorizamos estudio sobre carga pesada.
  2. Entrenamiento — 6:30 pm, intensidad moderada (dormiste 6.1 h anoche).
  3. Estudio — Curso de Fundamentos de IA, lección 4 · 40 min.
  4. Noticias de tu campo — 2 a 4 titulares de IA, con enlace.
  5. Adaptaciones — trasnochaste → moví el entreno a la tarde y bajé el volumen.
```

## Requisitos

- Tener **Claude Code** instalado. Si aún no lo tienes, instálalo desde su
  sitio oficial (busca "Claude Code" — es la herramienta de línea de
  comandos de Anthropic).
- Tener una **suscripción de Claude** activa (Pro o Max). Aion usa esa
  suscripción para pensar; no se necesita ninguna clave de API adicional.

## Cómo empezar

1. **Clona este repositorio** en tu computadora (o descárgalo como ZIP y
   descomprímelo).
2. **Ábrelo en Claude Code.** Elige la vía que uses:
   - **Terminal:** entra a la carpeta y arranca Claude Code:
     ```
     cd aion
     claude
     ```
   - **App de escritorio o web (claude.ai/code):** abre Claude Code y elige la
     carpeta `aion` como proyecto.

   Ya adentro, todos los `/comandos` de abajo se escriben **en el chat** de
   Claude Code (empezando con `/`).
3. **Corre `/aion-setup`**. Es una entrevista corta y amigable: tus metas, tu
   horario, tu tracker, tu campo de interés y qué navegador usas. Tu **rutina de
   entrenamiento la puedes entregar como quieras** —PDF, Word, Excel o texto
   pegado—: Aion la lee, la ordena y te la muestra para confirmar. Con eso crea
   tu carpeta `data/` privada.
4. **(Opcional) Trae tu progreso de Platzi.** Corre `/aion-platzi`: Aion te
   **abre tu ruta de Platzi en tu navegador** (con tu permiso), tú la guardas con
   SingleFile en `data/platzi/` y Aion la lee. La primera vez te ayuda a instalar
   SingleFile.
5. **Cada mañana, solo abre Aion.** Al abrir el proyecto en Claude Code, Aion te
   saluda y **arranca tu check-in solo** —a la hora que empieces tu día, sin
   comando— si aún no lo hiciste hoy. (Si prefieres dispararlo tú, corre `/aion`.)
   Te hace un check-in rápido (sueño, entrenamiento, energía) y te entrega tu plan
   del día: ventana de entrenamiento, plan de estudio, noticias y qué cambió hoy.
6. **Tu evolución aparece en el mismo chat.** Cada vez que corres `/aion`, Aion
   te muestra una tira de tendencias —sueño, energía, adherencia de entreno,
   progresión de cargas y progreso en Platzi— con mini-gráficas de texto, justo
   antes del plan del día. No hay que abrir ningún archivo.

## Cómo exportar un SingleFile de Platzi

`/aion-platzi` te abre la página en tu navegador para ahorrarte pasos; solo
necesitas guardarla como un archivo HTML con SingleFile. El detalle completo:

1. Instala la extensión **SingleFile** (gratis):
   - [Chrome, Edge o Brave](https://chromewebstore.google.com/detail/singlefile/mpiodijhokgodhhofbcjdecpffjipkle)
   - [Firefox](https://addons.mozilla.org/firefox/addon/single-file/)
2. Abre en tu navegador la página de tu ruta de Platzi (donde se ve tu
   progreso por curso y tu racha).
3. Usa la extensión SingleFile para guardar esa página como un único
   archivo `.html`.
4. Coloca ese archivo dentro de la carpeta `data/platzi/` de este proyecto.
5. Corre `/aion-platzi` en Claude Code para que Aion lo lea y guarde tu
   progreso.

## Privacidad

Tus datos son solo tuyos y viven **únicamente en tu computadora**, dentro de
la carpeta `data/`. Esa carpeta está en `.gitignore`, así que nunca se sube
a GitHub ni se comparte con nadie: se queda en tu máquina.

La carpeta `data.ejemplo/` que ves en el repositorio no es tu información —
son solo plantillas de referencia que muestran la forma que van a tener tus
archivos. No las edites pensando que son tuyas; tus datos reales se crean
automáticamente en `data/` cuando corres `/aion-setup`.

## Contribuciones y comunidad

Aion es **open source** y se hizo para compartirse. Si eres de la **comunidad de
Platzi** —o de cualquier lado— y se te ocurre una mejora, **eres bienvenido a
sumarla**: abre un *issue* con tu idea o manda un *pull request* con tu cambio.
Toda mejora que ayude a más gente a organizar mejor su día es bienvenida.

Y si Aion te sirvió, el mejor agradecimiento es **recomendarlo**: si crees que a
alguien le puede ayudar a descansar, entrenar o aprender mejor, pásale el
proyecto. 🙌

## Licencia

Publicado bajo la **licencia MIT** — puedes usarlo, modificarlo y compartirlo
libremente. Ver el archivo [`LICENSE`](LICENSE) para el detalle.
