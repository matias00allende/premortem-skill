# premortem

Skill de [Claude Code](https://docs.claude.com/en/docs/claude-code/skills) que
ejecuta un análisis premortem sobre un plan, proyecto o decisión: en vez de
preguntar "¿qué podría salir mal?" (que genera respuestas cautelosas y
genéricas), simula que el plan ya fracasó dentro de seis meses y reconstruye
la cadena de eventos, los supuestos ocultos y las señales de alerta tempranas
que lo hubieran anticipado - técnica descrita por Gary Klein.

Publicada como repo propio (no dentro de la colección general de skills) porque
es una técnica de análisis estratégico independiente del flujo de desarrollo de
software: aplica igual a una decisión de arquitectura, un lanzamiento de
producto o una decisión administrativa.

## Qué entrega

- Entre 5 y 8 modos de fracaso específicos al plan evaluado (no genéricos),
  cada uno con cadena de eventos, supuesto oculto y señales tempranas
  observables.
- El fracaso más probable y el más peligroso (no siempre son el mismo).
- El supuesto oculto crítico del plan completo.
- Un plan revisado que cierra los 3 modos de fracaso más importantes.
- Un checklist de lanzamiento verificable (máximo 8 ítems, cada uno sí/no).

## Instalación

```bash
# Windows
cp -r premortem-skill/ "$USERPROFILE/.claude/skills/premortem/"

# macOS / Linux
cp -r premortem-skill/ "$HOME/.claude/skills/premortem/"
```

Claude Code detecta automáticamente cualquier carpeta con un `SKILL.md` válido
en tu directorio de skills. El nombre de la carpeta debe coincidir con el
`name` declarado en el frontmatter de `SKILL.md` (`premortem`).

## Uso

Se activa automáticamente cuando el mensaje contiene frases como "premortem",
"qué podría fallar", "analiza los riesgos de este plan", "rompe este plan", o
se invoca explícitamente con `/premortem <descripción del plan>`.

No reemplaza una auditoría de seguridad técnica ni un code review - para eso
existen skills dedicadas (`auditar`, `review` en
[`claude-code-skills-toolkit`](https://github.com/matias00allende/claude-code-skills-toolkit)).
El premortem es sobre viabilidad y riesgo estratégico/operativo del plan como
un todo, no sobre calidad del código o configuración.

## Licencia

MIT. Ver [LICENSE](LICENSE).
