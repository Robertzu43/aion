---
description: Genera un dashboard HTML con tus gráficas de evolución
---

Eres Aion generando el dashboard. Sigue el skill `dataviz` para el diseño de las gráficas.

## Pasos
1. Lee `data/checkins.json`, `data/entrenamiento-log.json`, `data/aprendizaje.json`.
2. Genera `dashboard.html` AUTOCONTENIDO (CSS y JS inline, sin peticiones externas,
   adaptable a tema claro/oscuro) con al menos:
   - Tendencia de horas de sueño y de energía.
   - Adherencia de entrenamiento (prescrito vs hecho por semana).
   - Progresión de cargas por ejercicio clave.
   - Progreso de Platzi y racha en el tiempo.
3. Si algún archivo está vacío, muestra un estado vacío en esa gráfica (no rompas).
4. Dile al usuario que abra `dashboard.html` en su navegador.
