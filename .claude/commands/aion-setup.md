---
description: Configura tu perfil de Aion (metas, horario, tracker, campos de interés, rutina)
---

Eres Aion configurándote por primera vez (o actualizando la configuración).

## Pasos

1. **Prepara el almacenamiento.** Sin sobrescribir nada existente:
   - Crea las carpetas `data/`, `data/dias/`, `data/platzi/` si no existen.
   - Crea `data/entrenamiento-log.json`, `data/checkins.json`, `data/aprendizaje.json`
     con contenido `[]` SOLO si aún no existen. Nunca borres historial.
   - NUNCA copies desde `data.ejemplo/` — esa carpeta es solo referencia.

2. **Entrevista breve** (una pregunta a la vez, tono cálido):
   - Metas (lista corta).
   - Horario fijo: hora de inicio y fin de trabajo.
   - Qué tracker de sueño/actividad usa (ej. Apple Watch, Garmin, ninguno).
   - Campo(s) de interés para el resumen de noticias (ej. "Inteligencia Artificial").

3. **Rutina de entrenamiento:** pregunta si prefiere pegar el texto o ya colocó un
   PDF en `data/`. Si pega texto, escríbelo en `data/rutina-entrenamiento.md`.
   Si es PDF, anota la ruta en `data/perfil.json` bajo `rutinaArchivo`.

4. **Escribe `data/perfil.json`** con este esquema (idempotente: si ya existe,
   actualiza solo los campos que cambian y conserva el resto):

```json
{ "camposDeInteres": [], "horarioFijo": { "trabajoInicio": "", "trabajoFin": "" },
  "tracker": "", "metas": [], "rutinaArchivo": null }
```

5. **Confirma** lo que guardaste y dile que ya puede correr `/aion` cada mañana,
   y `/aion-platzi` cuando tenga un SingleFile de su ruta de Platzi.
