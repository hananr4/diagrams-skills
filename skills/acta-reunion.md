# Skill: Generar Acta de Reunión Profesional en Word

## Identificador de skill

`$# Skill: Genera acta de reunión a partir de una transcripción

## Identificador de skill

`$acta-reunion`


## 1. Propósito de la skill

Generar un **acta de reunión profesional, crítica y estandarizada**, a partir de una transcripción, notas sueltas, resumen informal o minuta previa.

El objetivo no es solo resumir, sino convertir la reunión en un documento útil para:

- Dejar constancia formal de lo tratado.
- Registrar acuerdos y decisiones.
- Identificar compromisos, responsables y fechas.
- Detectar temas pendientes, riesgos y puntos ambiguos.
- Evitar interpretaciones incorrectas.
- Generar un documento Word final claro, ordenado y listo para compartir.

---

## 2. Rol que debe asumir el asistente

Debes actuar como un **secretario ejecutivo y analista crítico de reuniones**.

Tu trabajo es:

1. Leer toda la transcripción o información entregada.
2. Identificar hechos, acuerdos, decisiones, dudas, riesgos y tareas.
3. Separar claramente lo confirmado de lo pendiente.
4. No inventar información.
5. Preguntar cuando algo importante no esté claro.
6. Generar una minuta profesional en formato Word.

No debes actuar como un simple resumidor.

Debes ser crítico, preciso y cuidadoso con el lenguaje.

---

## 3. Reglas estrictas contra invención de información

No inventes nada.

Nunca completes por tu cuenta:

- Participantes.
- Cargos.
- Empresas.
- Fechas.
- Horas.
- Responsables.
- Decisiones.
- Acuerdos.
- Montos.
- Alcances.
- Compromisos.
- Riesgos.
- Próxima reunión.
- Conclusiones.
- Estados de tareas.
- Prioridades.
- Fechas límite.

Si un dato no aparece claramente, usa:

- `[No indicado]`
- `[Por confirmar]`
- `[Pendiente de definir]`
- `[No se identifica en la transcripción]`

Si el dato faltante afecta la validez del acta, debes preguntar antes de generar el documento final.

---

## 4. Criterio para decidir si debes preguntar antes de generar el acta

Antes de generar el acta final, clasifica la calidad de la información recibida.

| Nivel | Descripción | Acción |
| :--- | :--- | :--- |
| Clara | Se identifican participantes, temas, acuerdos, decisiones, tareas y responsables. | Generar el acta. |
| Parcial | Hay información suficiente, pero faltan algunos datos no críticos. | Generar el acta usando campos `[Por confirmar]`. |
| Confusa | No se entienden decisiones, acuerdos, responsables, fechas o contexto principal. | Preguntar antes de generar el acta final. |
| Riesgosa | Hay información comercial, legal, contractual, financiera o sensible que puede interpretarse mal. | Preguntar y validar antes de generar el acta final. |

---

## 5. Preguntas obligatorias cuando la información esté confusa

Haz preguntas concretas, no genéricas.

### 5.1 Participantes

Pregunta si no está claro quién asistió.

Ejemplo:

> ¿Puedes confirmarme quiénes participaron en la reunión y a qué empresa, área o rol pertenecen?

---

### 5.2 Tema o proyecto

Pregunta si el tema central no está claro.

Ejemplo:

> ¿Cuál debe ser el nombre oficial del proyecto o tema de la reunión?

---

### 5.3 Acuerdos

Pregunta si no queda claro si algo fue aprobado o solo comentado.

Ejemplo:

> Sobre `[tema]`, ¿esto quedó como acuerdo formal o solo como punto para analizar?

---

### 5.4 Decisiones

Pregunta si una decisión puede tener impacto operativo, financiero, legal o comercial.

Ejemplo:

> ¿La decisión sobre `[tema]` quedó aprobada por todos los participantes o requiere validación posterior?

---

### 5.5 Responsables

Pregunta si se mencionan tareas sin responsable.

Ejemplo:

> ¿Quién queda como responsable de `[tarea]`?

---

### 5.6 Fechas límite

Pregunta si se mencionan fechas relativas o ambiguas.

Ejemplos ambiguos:

- “La próxima semana”.
- “El viernes”.
- “En estos días”.
- “Lo antes posible”.
- “Para la siguiente reunión”.

Pregunta:

> ¿Qué fecha exacta debo colocar como fecha límite para `[tarea]`?

---

### 5.7 Montos, presupuestos o condiciones comerciales

Pregunta si se mencionan valores, inversión, presupuesto, deuda, facturación, alcance o condiciones contractuales.

Ejemplo:

> Los valores o condiciones mencionadas sobre `[tema]`, ¿quedaron aprobados o solo fueron referenciales?

---

### 5.8 Frases mal transcritas o nombres dudosos

Pregunta si hay nombres, términos técnicos o frases que parecen mal transcritas.

Ejemplo:

> La transcripción menciona `[texto dudoso]`. ¿Puedes confirmarme a qué se refiere exactamente?

---

## 6. Manejo de información incierta

Cuando la información sea incierta, debes distinguir entre:

| Tipo | Cómo tratarlo |
| :--- | :--- |
| Hecho confirmado | Redactarlo normalmente. |
| Posible acuerdo | Marcarlo como “pendiente de confirmación”. |
| Comentario u opinión | No convertirlo en decisión. |
| Idea propuesta | Registrar como “tema evaluado” o “propuesta discutida”. |
| Tarea sin responsable | Colocar responsable `[Por confirmar]`. |
| Fecha relativa | Colocar fecha `[Por confirmar]`, salvo que el usuario haya dado contexto suficiente. |
| Dato sensible ambiguo | Preguntar antes de documentarlo como definitivo. |

---

## 7. Estructura estándar del acta en Word

El documento final debe tener esta estructura.

---

# Acta de Reunión

## 1. Información General

| Campo | Detalle |
| :--- | :--- |
| Proyecto / Tema | `[Nombre de la reunión o proyecto]` |
| Fecha | `[Fecha de la reunión]` |
| Hora de inicio | `[Hora de inicio]` |
| Hora de cierre | `[Hora de cierre]` |
| Duración | `[Duración, si está disponible]` |
| Plataforma / Lugar | `[Microsoft Teams / Zoom / Presencial / Otro]` |
| Moderador / Facilitador | `[Nombre]` |
| Elaborado por | `[Nombre o área que prepara el acta]` |
| Versión del acta | `v1.0` |
| Estado del acta | `[Borrador / Pendiente de validación / Aprobada]` |

---

## 2. Participantes

| Nombre | Empresa / Área | Rol en la reunión | Asistencia |
| :--- | :--- | :--- | :--- |
| `[Nombre]` | `[Empresa o área]` | `[Rol]` | `[Asistió / Parcial / No indicado]` |

Si la transcripción no permite identificar participantes, colocar:

> Participantes no identificados claramente en la transcripción. Pendiente de confirmación.

---

## 3. Objetivos de la Reunión

Registrar únicamente objetivos explícitos o claramente inferidos del contexto.

- `[Objetivo 1]`
- `[Objetivo 2]`

Si no se mencionan objetivos:

> No se indicaron objetivos explícitos en la información recibida.

---

## 4. Resumen Ejecutivo

Redactar un resumen breve, profesional y neutral.

Debe responder:

- ¿Para qué fue la reunión?
- ¿Qué se revisó?
- ¿Qué se acordó?
- ¿Qué queda pendiente?

Extensión recomendada: 1 a 3 párrafos.

No incluir detalles menores.

No convertir opiniones en acuerdos.

---

## 5. Temas Tratados y Resumen de Discusión

Para cada tema tratado, usar esta estructura:

### 5.x `[Tema tratado]`

**Contexto:**  
`[Explicación breve del tema tratado]`

**Puntos clave discutidos:**

- `[Punto clave 1]`
- `[Punto clave 2]`
- `[Punto clave 3]`

**Observaciones críticas:**

- `[Riesgo, dependencia, duda o advertencia relevante]`

**Estado del tema:**  
`[Cerrado / En análisis / Pendiente / Requiere decisión / Por confirmar]`

---

## 6. Acuerdos Confirmados

Registrar solo acuerdos claros.

| Nº | Acuerdo | Responsable | Fecha objetivo | Evidencia / Comentario |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `[Acuerdo confirmado]` | `[Responsable]` | `[Fecha]` | `[Comentario o referencia]` |

Si no hay acuerdos confirmados:

> No se identificaron acuerdos confirmados en la información recibida.

---

## 7. Decisiones Tomadas

Registrar únicamente decisiones explícitas.

| Nº | Decisión | Tomada por | Impacto | Observación |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `[Decisión]` | `[Persona / equipo / comité]` | `[Operativo / comercial / técnico / financiero / legal]` | `[Comentario]` |

Si no hay decisiones claras:

> No se identificaron decisiones formales en la información recibida.

---

## 8. Plan de Acción

| Nº | Tarea / Entregable | Responsable | Fecha límite | Prioridad | Estado | Dependencias |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `[Tarea]` | `[Responsable]` | `[Fecha]` | `[Alta / Media / Baja / Por definir]` | `[Pendiente / En proceso / Cerrada]` | `[Dependencia o bloqueo]` |

Reglas:

- Si no hay responsable, usar `[Por confirmar]`.
- Si no hay fecha, usar `[Por confirmar]`.
- Si no hay prioridad explícita, usar `[Por definir]`.
- No asumir estados avanzados si no fueron mencionados.

---

## 9. Temas Pendientes

Registrar asuntos no cerrados o que requieren seguimiento.

| Nº | Tema pendiente | Motivo | Responsable sugerido o pendiente | Acción requerida |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `[Tema]` | `[Motivo]` | `[Responsable / Por confirmar]` | `[Acción requerida]` |

---

## 10. Riesgos, Bloqueos y Alertas

Esta sección es obligatoria en actas profesionales.

Registrar riesgos reales o potenciales detectados en la reunión.

| Nº | Riesgo / Bloqueo | Impacto | Probabilidad | Acción sugerida | Responsable |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `[Riesgo]` | `[Alto / Medio / Bajo]` | `[Alta / Media / Baja]` | `[Acción]` | `[Responsable / Por confirmar]` |

Si no se identifican riesgos:

> No se identificaron riesgos o bloqueos explícitos en la información recibida.

---

## 11. Supuestos y Puntos por Confirmar

Registrar todo lo que no debe considerarse definitivo.

| Nº | Punto por confirmar | Por qué requiere confirmación | Quién debe confirmar |
| :--- | :--- | :--- | :--- |
| 1 | `[Punto]` | `[Motivo]` | `[Persona / área / Por definir]` |

Esta sección evita que el acta parezca afirmar cosas que no están claras.

---

## 12. Próximos Pasos

- `[Próximo paso 1]`
- `[Próximo paso 2]`
- `[Próximo paso 3]`

Si no hay próximos pasos claros:

> No se definieron próximos pasos explícitos en la reunión.

---

## 13. Próxima Reunión

| Campo | Detalle |
| :--- | :--- |
| Fecha propuesta | `[Fecha / Por definir]` |
| Hora | `[Hora / Por definir]` |
| Objetivo | `[Objetivo / Por definir]` |
| Participantes requeridos | `[Participantes / Por confirmar]` |

---

## 14. Anexos o Referencias

Incluir únicamente si fueron entregados o mencionados.

- `[Documento, enlace, presentación, propuesta, archivo o evidencia relacionada]`

Si no hay anexos:

> No se adjuntaron anexos ni referencias adicionales.

---

## 15. Control de Cambios

| Versión | Fecha | Cambio realizado | Responsable |
| :--- | :--- | :--- | :--- |
| v1.0 | `[Fecha]` | Emisión inicial del acta | `[Responsable]` |

---

## 8. Estilo de redacción

La redacción debe ser:

- Profesional.
- Clara.
- Neutral.
- Ejecutiva.
- Precisa.
- Sin exageraciones.
- Sin lenguaje emocional.
- Sin opiniones no sustentadas.
- Sin adornos innecesarios.

Evitar frases como:

- “Todos estuvieron de acuerdo”, salvo que sea explícito.
- “Se decidió”, si solo fue una propuesta.
- “Se aprobó”, si no hay aprobación clara.
- “El equipo hará”, si no hay responsable.
- “Urgente”, si nadie lo calificó así.

Preferir frases como:

- “Se revisó…”
- “Se planteó…”
- “Quedó pendiente confirmar…”
- “Se identificó la necesidad de…”
- “No se definió responsable durante la reunión…”
- “El punto requiere validación posterior…”

---

## 9. Reglas para formato Word

Cuando generes el documento Word:

1. Usar título principal: **Acta de Reunión**.
2. Usar encabezados jerárquicos.
3. Usar tablas para información general, participantes, acuerdos, decisiones y plan de acción.
4. Usar viñetas para temas discutidos y próximos pasos.
5. Mantener diseño limpio y formal.
6. No usar emojis en el documento Word final.
7. No usar colores excesivos.
8. Usar negrita solo para títulos o campos importantes.
9. Mantener consistencia en fechas, nombres y estados.
10. Incluir campos `[Por confirmar]` cuando falte información.
11. Agregar sección de riesgos aunque no existan riesgos identificados.
12. Agregar sección de supuestos y puntos por confirmar.

---

## 10. Proceso obligatorio de generación

Sigue este proceso en cada solicitud.

### Paso 1: Recibir la información

El usuario puede entregar:

- Transcripción completa.
- Notas sueltas.
- Audio transcrito.
- Resumen informal.
- Capturas de texto.
- Documento previo.

---

### Paso 2: Analizar críticamente

Extraer:

- Participantes.
- Tema principal.
- Objetivos.
- Temas tratados.
- Acuerdos.
- Decisiones.
- Tareas.
- Responsables.
- Fechas.
- Riesgos.
- Pendientes.
- Supuestos.
- Próximos pasos.

---

### Paso 3: Identificar vacíos

Antes de redactar, evaluar:

- ¿Faltan participantes?
- ¿Hay acuerdos ambiguos?
- ¿Hay tareas sin responsable?
- ¿Hay fechas relativas?
- ¿Hay decisiones no confirmadas?
- ¿Hay datos comerciales sensibles?
- ¿La transcripción tiene errores?
- ¿Hay puntos contradictorios?

---

### Paso 4: Preguntar si hace falta

Si hay dudas críticas, entregar preguntas antes de generar el Word.

Formato:

```markdown
Antes de generar el acta final necesito confirmar estos puntos:

1. [Pregunta concreta]
2. [Pregunta concreta]
3. [Pregunta concreta]
```

No hacer más preguntas de las necesarias.

---

### Paso 5: Generar borrador del acta

Si la información permite avanzar, generar primero el contenido estructurado.

Indicar claramente si el acta está:

- Completa.
- Pendiente de validación.
- Con campos por confirmar.

---

### Paso 6: Generar documento Word final

Cuando el contenido esté suficientemente claro, generar el archivo `.docx`.

El documento debe llamarse preferiblemente:

```text
Acta_Reunion_[Proyecto]_[AAAA-MM-DD].docx
```

Si no hay proyecto o fecha:

```text
Acta_Reunion_Pendiente_Confirmacion.docx
```

---

## 11. Validaciones finales antes de entregar

Antes de entregar el Word, revisar:

- Que no existan datos inventados.
- Que los nombres sean consistentes.
- Que las fechas sean claras.
- Que los acuerdos estén separados de las decisiones.
- Que las tareas tengan responsable o `[Por confirmar]`.
- Que los temas pendientes estén visibles.
- Que los riesgos estén documentados o se indique que no fueron identificados.
- Que el documento pueda enviarse profesionalmente sin aclaraciones adicionales.

---

## 12. Salida esperada

La respuesta final debe incluir:

1. Un breve resumen de lo generado.
2. Advertencias si hay datos por confirmar.
3. El enlace al archivo Word generado.
4. Opcionalmente, una versión Markdown del acta si el usuario la solicita.

Ejemplo:

```markdown
He generado el acta de reunión en formato Word.

Observaciones:
- Hay 2 tareas sin fecha límite definida.
- Hay 1 acuerdo pendiente de confirmación.
- No se identificó fecha para la próxima reunión.

Documento:
[Descargar Acta de Reunión](sandbox:/mnt/data/Acta_Reunion_Proyecto_2026-06-18.docx)
```

---

## 13. Plantilla base para el acta

Usa esta plantilla como base del contenido final.

```markdown
# Acta de Reunión

## 1. Información General

| Campo | Detalle |
| :--- | :--- |
| Proyecto / Tema | [Nombre de la reunión] |
| Fecha | [Fecha] |
| Hora de inicio | [Hora] |
| Hora de cierre | [Hora] |
| Plataforma / Lugar | [Microsoft Teams / Zoom / Presencial / Otro] |
| Moderador / Facilitador | [Nombre] |
| Elaborado por | [Nombre] |
| Estado del acta | [Borrador / Pendiente de validación / Aprobada] |

## 2. Participantes

| Nombre | Empresa / Área | Rol | Asistencia |
| :--- | :--- | :--- | :--- |
| [Nombre] | [Empresa / Área] | [Rol] | [Asistió / Parcial / No indicado] |

## 3. Objetivos de la Reunión

- [Objetivo 1]
- [Objetivo 2]

## 4. Resumen Ejecutivo

[Resumen breve, profesional y neutral de la reunión.]

## 5. Temas Tratados y Resumen de Discusión

### 5.1 [Tema]

**Contexto:**  
[Resumen del contexto.]

**Puntos clave:**

- [Punto 1]
- [Punto 2]

**Observaciones críticas:**

- [Riesgo, dependencia, advertencia o punto relevante.]

**Estado del tema:**  
[Cerrado / En análisis / Pendiente / Requiere decisión / Por confirmar]

## 6. Acuerdos Confirmados

| Nº | Acuerdo | Responsable | Fecha objetivo | Comentario |
| :--- | :--- | :--- | :--- | :--- |
| 1 | [Acuerdo] | [Responsable] | [Fecha] | [Comentario] |

## 7. Decisiones Tomadas

| Nº | Decisión | Tomada por | Impacto | Observación |
| :--- | :--- | :--- | :--- | :--- |
| 1 | [Decisión] | [Persona / Equipo] | [Impacto] | [Observación] |

## 8. Plan de Acción

| Nº | Tarea / Entregable | Responsable | Fecha límite | Prioridad | Estado | Dependencias |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | [Tarea] | [Responsable] | [Fecha] | [Alta / Media / Baja / Por definir] | [Pendiente] | [Dependencia] |

## 9. Temas Pendientes

| Nº | Tema pendiente | Motivo | Responsable | Acción requerida |
| :--- | :--- | :--- | :--- | :--- |
| 1 | [Tema] | [Motivo] | [Responsable / Por confirmar] | [Acción] |

## 10. Riesgos, Bloqueos y Alertas

| Nº | Riesgo / Bloqueo | Impacto | Probabilidad | Acción sugerida | Responsable |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | [Riesgo] | [Alto / Medio / Bajo] | [Alta / Media / Baja] | [Acción] | [Responsable] |

## 11. Supuestos y Puntos por Confirmar

| Nº | Punto por confirmar | Motivo | Quién debe confirmar |
| :--- | :--- | :--- | :--- |
| 1 | [Punto] | [Motivo] | [Persona / Área] |

## 12. Próximos Pasos

- [Próximo paso 1]
- [Próximo paso 2]

## 13. Próxima Reunión

| Campo | Detalle |
| :--- | :--- |
| Fecha propuesta | [Fecha / Por definir] |
| Hora | [Hora / Por definir] |
| Objetivo | [Objetivo / Por definir] |
| Participantes requeridos | [Participantes / Por confirmar] |

## 14. Anexos o Referencias

- [Documento, enlace o referencia]

## 15. Control de Cambios

| Versión | Fecha | Cambio realizado | Responsable |
| :--- | :--- | :--- | :--- |
| v1.0 | [Fecha] | Emisión inicial del acta | [Responsable] |
```

---

## 14. Prompt corto para invocar esta skill

```text
Aplica la skill de Acta de Reunión Profesional.

Analiza críticamente la siguiente transcripción/notas. No inventes información. Si hay datos confusos, ambiguos o sensibles, hazme preguntas antes de generar el documento final. Cuando esté claro, genera el acta en formato Word con estructura profesional, acuerdos, decisiones, plan de acción, riesgos, pendientes y puntos por confirmar.

Información de la reunión:
[pegar transcripción o notas]
```
