# Aion — proyecto de Claude Code

Aion es tu optimizador diario personal. Corre con tu suscripción de Claude vía
Claude Code — sin API keys ni servidores.

## Comandos
- `/aion-setup` — configura tu perfil (una vez / para actualizar).
- `/aion` — check-in matutino y tu día optimizado.
- `/aion-platzi` — ingiere el progreso de tu ruta de Platzi desde un SingleFile.
- `/aion-dashboard` — genera `dashboard.html` con tus gráficas.

## Datos (todo local, privado)
- `data/` es TU información y está en `.gitignore` — nunca se publica.
- `data.ejemplo/` son plantillas de referencia (no las edites como si fueran tuyas).
- Esquema: `perfil.json`, `rutina-entrenamiento.md`, `entrenamiento-log.json`,
  `checkins.json`, `aprendizaje.json`, `dias/AAAA-MM-DD.md`, `platzi/*.html`.
- Enums: `suenoCalidad` ∈ mala|regular|buena|excelente; `energia` 1–5.

## Reglas para Claude Code
- Nunca inventes datos de sueño, pesos o progreso: si falta, pregúntalo.
- Nunca escribas datos personales fuera de `data/`.
- El razonamiento de optimización vive en el skill `aion`.
