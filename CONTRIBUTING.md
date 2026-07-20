# Contribuir a Aion

Gracias por querer mejorar Aion. Toda ayuda es bienvenida — no necesitas ser
programador experto para contribuir.

## Cómo está hecho

Aion es casi todo **instrucciones en Markdown**, no un programa que se compila:

- `.claude/commands/*.md` — los comandos (`/aion`, `/aion-setup`, `/aion-platzi`).
- `.claude/skills/aion/SKILL.md` — la lógica de razonamiento (cómo prioriza y adapta).
- `.claude/settings.json` — el hook que arranca el check-in al abrir el proyecto.
- `data.ejemplo/` — plantillas que muestran la forma de cada archivo de datos.

No hay build ni dependencias que instalar.

## Cómo probar tu cambio

1. Abre el repo en Claude Code.
2. Corre `/aion-setup`, luego `/aion` y `/aion-platzi` con datos de prueba.
3. Revisa que el flujo siga claro y que el plan del día conserve sus 5 secciones.

## Reglas simples

- **Privacidad primero:** nunca subas datos personales. La carpeta `data/` está en
  `.gitignore` — que siga así.
- Si cambias el **modelo de datos**, actualiza también `data.ejemplo/` para que quede
  en sync.
- PRs pequeños y con una descripción clara de qué mejora y por qué.
- Para ideas grandes, abre primero un *issue* y lo conversamos.

## ¿Dudas o ideas?

Abre un *issue*. Y si Aion te sirvió, recomiéndalo a quien creas que le pueda ayudar.
