# Aion

Aion es tu agente personal para armar, cada mañana, tu día óptimo. Cruza tu
descanso, tu entrenamiento, tu aprendizaje en Platzi y las noticias de tu
campo de interés, y te entrega un plan claro para hoy.

Corre dentro de **Claude Code**, usando tu propia suscripción de Claude. No
necesitas API keys, no necesitas montar ningún servidor: instalas Claude
Code, abres esta carpeta, y listo.

## Qué es Aion

Aion es un agente personal que cada mañana revisa cómo dormiste, qué toca en
tu rutina de entrenamiento, cómo va tu progreso en Platzi y las noticias de
tu campo de interés, y con todo eso te propone el mejor plan para tu día.
No es una app ni un dashboard en la nube: es un conjunto de instrucciones
que corre directamente dentro de Claude Code, en tu computadora, usando tu
suscripción de Claude. Sin API keys, sin servidores, sin nada que instalar
además de Claude Code.

## Requisitos

- Tener **Claude Code** instalado. Si aún no lo tienes, instálalo desde su
  sitio oficial (busca "Claude Code" — es la herramienta de línea de
  comandos de Anthropic).
- Tener una **suscripción de Claude** activa (Pro o Max). Aion usa esa
  suscripción para pensar; no se necesita ninguna clave de API adicional.

## Cómo empezar

1. **Clona este repositorio** en tu computadora (o descárgalo como ZIP y
   descomprímelo).
2. **Ábrelo en Claude Code** — entra a la carpeta del proyecto y arranca
   Claude Code ahí.
3. **Corre `/aion-setup`**. Es una entrevista corta y amigable: tus metas,
   tu horario, qué tracker de sueño/actividad usas, tu campo de interés y tu
   rutina de entrenamiento. Con eso Aion crea tu carpeta `data/` privada.
4. **(Opcional) Trae tu progreso de Platzi.** Exporta tu ruta con la
   extensión SingleFile (ver abajo cómo), guarda el archivo en
   `data/platzi/`, y corre `/aion-platzi` para que Aion lo lea.
5. **Cada mañana, corre `/aion`.** Te hace un check-in rápido (sueño,
   entrenamiento, energía) y te entrega tu plan del día: ventana de
   entrenamiento, plan de estudio, noticias de tu campo y qué cambió hoy.
6. **Cuando quieras ver tu evolución, corre `/aion-dashboard`** y abre el
   archivo `dashboard.html` que se genera en tu navegador. Ahí vas a ver tus
   gráficas de sueño, energía, entrenamiento y progreso en Platzi a lo largo
   del tiempo.

## Cómo exportar un SingleFile de Platzi

Para que Aion pueda leer tu progreso en Platzi, necesitas guardar la página
de tu ruta como un solo archivo HTML:

1. Instala la extensión **SingleFile** en tu navegador (está disponible para
   Chrome, Firefox y navegadores basados en Chromium).
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
