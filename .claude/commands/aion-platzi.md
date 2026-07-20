---
description: Lee un SingleFile HTML de tu ruta de Platzi y guarda tu progreso
---

Eres Aion ingiriendo el progreso de Platzi desde un archivo SingleFile.

## Pasos
1. Busca el HTML más reciente en `data/platzi/`. Si no hay ninguno nuevo, **reduce la
   fricción abriéndole el navegador** (lee `navegador` y `platziRutaURL` de `data/perfil.json`):
   - Pídele confirmación ("¿abro tu ruta de Platzi en <navegador>?") y **solo entonces**
     abre la URL en su navegador (macOS: `open -a "<navegador>" "<platziRutaURL>"`;
     adapta el comando al sistema operativo). Si no hay `platziRutaURL`, pídesela y guárdala.
   - Si aún no tiene SingleFile, ofrécele abrir la página de instalación de la extensión igual.
   - Recuérdale en una línea: con SingleFile, guarda la página como `.html` dentro de
     `data/platzi/` y vuelve a correr `/aion-platzi`. Luego detente hasta que exista el archivo.
2. Lee el HTML y extrae, por curso: título, porcentaje de progreso y si está
   completado; además la racha (streak) de la cuenta. Señal determinista para la
   racha: el número que sigue a la etiqueta "Streak"/"racha" es el valor de `racha`.
3. Sé tolerante: el HTML de Platzi puede cambiar. Si no logras extraer con
   confianza, pídele al usuario que te dicte los cursos y % manualmente.
4. Añade un snapshot al final de `data/aprendizaje.json` (crea `[]` si no existe):

```json
{ "fecha": "AAAA-MM-DD", "racha": 0,
  "cursos": [{ "titulo": "", "progresoPct": 0, "completado": false }] }
```

   Usa la fecha de hoy. No dupliques si ya hay un snapshot de hoy: reemplázalo.
5. Confirma cuántos cursos leyó y el % promedio.
