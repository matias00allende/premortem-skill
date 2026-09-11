---
name: premortem
description: >
  Ejecuta un análisis premortem sobre un plan, proyecto o decisión: imagina que
  ya fracasó seis meses después y reconstruye por qué, con cadena de eventos,
  supuestos ocultos y señales de alerta tempranas. Entrega un análisis
  estratégico completo con plan revisado y checklist de lanzamiento.
  Usar cuando el usuario diga "premortem", "haz un premortem", "simula el
  fracaso", "qué podría fallar", "analiza los riesgos de este plan",
  "rompe este plan", "por qué podría fallar esto", "adversarial review",
  "red team de este plan". No usar para auditorías de seguridad técnica
  (usar /auditar) ni para revisiones de código (usar /review).
model: sonnet
disable-model-invocation: false
allowed-tools: Read Glob Grep
---

# Premortem - Análisis de fracaso anticipado

Ejecuta un premortem sobre: **$ARGUMENTS**

El objetivo es el opuesto de un postmortem: en lugar de analizar el fracaso después de que ocurre, imaginamos que ya ocurrió y reconstruimos por qué, antes de comprometer recursos.

---

## Paso 1: Encuadre del plan

Antes de cualquier análisis, establece con precisión qué se está evaluando:

1. ¿Cuál es el objetivo declarado del plan o proyecto?
2. ¿Cuál es el criterio de éxito? (métrica, fecha, entregable concreto)
3. ¿Quiénes son los actores clave y cuáles son sus supuestos implícitos?
4. ¿Qué recursos, dependencias externas o aprobaciones requiere?
5. ¿Cuál es el punto de no retorno? (momento en que el costo de abortar supera el costo de continuar)

Si el usuario no proporcionó contexto suficiente, infiere razonablemente desde los detalles disponibles. Solo pregunta si la ambigüedad cambia materialmente el análisis.

---

## Paso 2: Activar modo retrospectiva prospectiva

**No preguntes "¿qué podría salir mal?"**. Eso genera respuestas cautelosas y genéricas.

Usa el encuadre de Klein: **"Han pasado seis meses. El proyecto fracasó de forma clara y costosa. Los involucrados están en la sala de crisis. ¿Qué ocurrió?"**

Genera entre 5 y 8 modos de fracaso específicos para este plan. Para cada uno:

```
[F-NN] Título del modo de fracaso

Cadena de eventos:
→ [Evento desencadenante]
→ [Escalada]
→ [Punto de quiebre]
→ [Consecuencia final]

Supuesto oculto: [La cosa que parecía tan obvia que nadie la cuestionó, pero de la que dependía todo]

Señales tempranas a vigilar:
- [Indicador observable 1 - medible o verificable]
- [Indicador observable 2]

Probabilidad estimada: Alta / Media / Baja
Daño si ocurre: Crítico / Alto / Medio
```

---

## Paso 3: Análisis estratégico consolidado

Después de mapear los modos de fracaso, sintetiza:

### Fracaso más probable
[Cuál de los F-NN tiene mayor probabilidad de materializarse y por qué]

### Fracaso más peligroso
[Cuál causaría mayor daño aunque no sea el más probable - el que hay que evitar a cualquier costo]

### Supuesto oculto crítico
[La suposición no declarada más importante del plan. Si falla esta sola, el plan colapsa. Suele ser algo que parece evidente y por eso nadie lo cuestionó.]

### Dependencias que no están bajo control del equipo
[Lista de lo que requiere acción de terceros: proveedores, aprobaciones, sistemas externos, presupuesto, personas específicas]

---

## Paso 4: Plan revisado

Entrega una versión mejorada del plan original que:
- Cierra o mitiga los 3 modos de fracaso más importantes
- Hace explícito el supuesto oculto crítico como requisito verificable
- Agrega hitos de validación temprana antes del punto de no retorno
- No sobre-ingeniería: ajusta lo mínimo necesario para que el plan sea defendible

---

## Paso 5: Checklist de lanzamiento

Lista corta (máximo 8 ítems) de cosas que deben ser verdaderas antes de ejecutar. Cada ítem debe ser verificable con un sí/no:

```
[ ] [Condición verificable 1]
[ ] [Condición verificable 2]
...
```

---

## Criterios de calidad

- Cada modo de fracaso debe ser específico al plan evaluado, no genérico
- Los supuestos ocultos deben ser no-obvios: si parecen evidentes al leerlos, no son supuestos ocultos reales
- Las señales tempranas deben ser observables antes de que sea demasiado tarde para corregir
- Distingue siempre: Verificado (hay evidencia) / Inferido (hay lógica) / Asumido (hipótesis sin datos)
- No suavices el análisis por cortesía. El valor está exactamente en lo incómodo

## Troubleshooting

**El usuario da un plan muy vago:** Usa el contexto del proyecto activo para inferir el stack, dependencias y restricciones. Si sigue sin ser suficiente, identifica los 3 supuestos más probables y hazlos explícitos antes de continuar.

**El plan es una comunicación o decisión administrativa, no un proyecto técnico:** El método aplica igual. Sustituye "deploy" por "envío" y "stack" por "proceso o comunicación". Los supuestos ocultos en decisiones administrativas suelen ser políticos o de alineación, no técnicos.

**El usuario ya conoce el premortem y pide análisis rápido:** Omite Pasos 1 y 5, entrega directamente los modos de fracaso (Paso 2) y el análisis estratégico (Paso 3) en formato compacto.
