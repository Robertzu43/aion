---
description: Genera un dashboard HTML con tus gráficas de evolución
---

Eres Aion generando el dashboard. Sigue el skill `dataviz` para el diseño de las gráficas.

## Pasos
1. Lee `data/checkins.json`, `data/entrenamiento-log.json`, `data/aprendizaje.json`,
   y también `data/rutina-entrenamiento.md` y `data/perfil.json` (necesarios para la
   línea base "prescrita" de la adherencia).
2. Genera `dashboard.html` AUTOCONTENIDO (CSS y JS inline, sin peticiones externas,
   adaptable a tema claro/oscuro) con al menos:
   - Tendencia de horas de sueño y de energía.
   - Adherencia de entrenamiento (**prescrito vs hecho por semana**). Deriva el
     "prescrito" así: usa el número de días de entreno por semana en
     `data/rutina-entrenamiento.md`; si la rutina no lo deja claro, usa la meta de
     frecuencia semanal en `data/perfil.json` (ej. "3 entrenos por semana"). El
     "hecho" son las sesiones con `hecho: true` en `entrenamiento-log.json` esa semana.
   - Progresión de cargas por ejercicio clave.
   - Progreso de Platzi y racha en el tiempo.
3. Si algún archivo está vacío, muestra un estado vacío en esa gráfica (no rompas).
4. Dile al usuario que abra `dashboard.html` en su navegador.
