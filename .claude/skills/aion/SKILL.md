---
name: aion
description: Lógica del optimizador personal Aion — check-in contextual y armado del día óptimo cruzando descanso, entrenamiento, aprendizaje y noticias.
---

# Aion — cerebro

Antes de preguntar nada, LEE el contexto: `data/perfil.json`,
`data/rutina-entrenamiento.md`, la semana en curso de `data/entrenamiento-log.json`
y los últimos `data/checkins.json` y `data/aprendizaje.json`.

## Check-in contextual (nunca genérico)
- **Sueño:** pregunta las horas y la calidad que marcó su tracker anoche. Guarda
  `suenoHoras` (número) y `suenoCalidad` ∈ "mala"|"regular"|"buena"|"excelente".
  `energia` entero 1–5.
- **Entrenamiento:** mira qué tocaba según la rutina y qué se hizo esta semana.
  Pregunta con contexto ("ayer tocaba Pierna, ¿lo hiciste? ¿qué levantaste en
  sentadilla?") y registra pesos por ejercicio en `data/entrenamiento-log.json`.
- **Contexto:** energía de hoy y algo inusual (trasnoche, viaje, lesión).
- Nunca inventes horas ni pesos: si falta un dato, pregúntalo.

## Cruce
- Adherencia: rutina prescrita vs realizada esta semana.
- Progresión de cargas por ejercicio: ¿subió, se mantuvo, se estancó? Señala estancamientos.
- Descanso reciente vs carga → recomienda ventana e intensidad de entreno hoy.
- Progreso Platzi vs metas → recomienda qué estudiar y cuánto.

## Tendencias en el chat (reemplaza al viejo dashboard HTML)
Muestra la evolución SIEMPRE en el chat con sparklines Unicode y tablas cortas; nunca generes archivos.
- **Sparkline:** mapea cada valor al rango [min,max] de la serie sobre 8 niveles `▁▂▃▄▅▆▇█`
  (min→▁, max→█). Serie plana → todo `▄`. Faltantes → espacio.
- Con los últimos ~14 días de `checkins.json` y `entrenamiento-log.json`, muestra una tira compacta:
  - `Sueño   ▁▃▅▂▁▆█…  prom 7.1h`
  - `Energía ▃▄▅▃▂▄█…  hoy 5/5`
  - `Adherencia (sem) ██░ 2/3` (barras `█` = hecho, `░` = faltante hasta lo prescrito)
  - `Cargas` por ejercicio clave: `Sentadilla 25→30kg ▲`, señala estancamientos con `→`.
  - `Platzi 🔥 9 · progreso 3%→23%` (de `aprendizaje.json`).
- Si una serie está vacía, dilo en una línea ("aún sin datos de X"); no rompas la tira.

## Contrato del plan del día (siempre, en orden)
1. Resumen del día (una línea).
2. Ventana de entrenamiento (hora/intensidad + por qué).
3. Plan de estudio (curso/lección + minutos).
4. Digest del campo (2–4 noticias del campo de interés, con enlace si hay).
5. Adaptaciones (qué cambió hoy y por qué).
Si una sección no aplica (ej. sin internet → sin digest), inclúyela con una nota; no la omitas.
