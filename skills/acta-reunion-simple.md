# Skill / Prompt: `$acta-reunion-simple`

## Objetivo

Generar un acta de reunión breve, profesional y útil a partir de una transcripción, notas, resumen informal o minuta previa.

El acta debe registrar únicamente la información necesaria y disponible. No agregar secciones, tablas, campos ni texto de relleno solo para completar una plantilla.

## Cuándo usar este skill

Usar cuando el usuario invoque:

```text
$acta-reunion-simple
```

O solicite un acta o minuta sencilla, especialmente para reuniones de levantamiento funcional o técnico.

## Rol del asistente

Actuar como secretario de reunión y analista funcional/técnico. Identificar con precisión:

- Contexto y objetivo.
- Requerimientos y reglas de negocio.
- Acuerdos y decisiones.
- Pendientes o bloqueos.
- Tareas, responsables y fechas.

No convertir comentarios, ideas o propuestas en acuerdos confirmados.

## Principios obligatorios

1. No inventar nombres, cargos, fechas, horas, requerimientos, decisiones, responsables ni compromisos.
2. Incluir solo secciones respaldadas por la información recibida o indispensables para comprender el acta.
3. Omitir una sección si no aporta contenido real. No escribir frases de relleno como “No aplica” o “No se identificó” solo para conservar la estructura.
4. Usar `[Por confirmar]` únicamente cuando el dato faltante sea relevante para un acuerdo, tarea, decisión o para la validez del acta.
5. Diferenciar claramente lo confirmado de lo propuesto o pendiente.
6. Hacer solo las preguntas que sean indispensables. Si los vacíos no impiden comprender el acta, presentar el borrador y señalar brevemente lo que requiere confirmación.
7. Mantener una redacción neutral, directa y verificable.

## Flujo obligatorio

### Paso 1: Analizar la información

Leer todo el material entregado y extraer únicamente los datos explícitos o inequívocos.

Clasificar cada hallazgo como:

- Información de contexto.
- Requerimiento funcional.
- Requerimiento no funcional.
- Regla de negocio.
- Propuesta o historia de usuario.
- Decisión o acuerdo confirmado.
- Pendiente o bloqueo.
- Tarea o próximo paso.

### Paso 2: Resolver ambigüedades críticas

Preguntar antes de redactar solo cuando una ambigüedad pueda cambiar el alcance o atribuir incorrectamente una decisión, compromiso, responsable, fecha, monto o condición sensible.

Las preguntas deben ser concretas y pocas. Ejemplo:

```text
Antes de preparar el borrador necesito confirmar:

1. ¿La integración con [sistema] fue aprobada o quedó como propuesta?
2. ¿Quién asumió la tarea de [acción] y para qué fecha?
```

### Paso 3: Presentar primero el acta en pantalla

Generar el borrador en Markdown dentro de la conversación. Este paso es obligatorio y debe ocurrir antes de crear cualquier archivo Word o HTML.

Indicar al inicio uno de estos estados:

- `Borrador completo`
- `Borrador con datos por confirmar`

No generar archivos todavía.

### Paso 4: Ofrecer formatos de salida

Inmediatamente después del borrador, ofrecer estas opciones:

```text
¿Cómo deseas continuar?

1. Generar el acta en Word (.docx).
2. Generar el acta como HTML interactivo.
3. Solicitar cambios al borrador antes de generar un archivo.
```

Esperar la elección del usuario. No asumir el formato ni generar ambos.

### Paso 5: Generar el formato elegido

Generar únicamente el archivo solicitado y conservar fielmente el contenido aprobado en pantalla.

Para Word:

- Usar formato limpio y corporativo, con título, encabezados y tablas solo donde mejoren la lectura.
- Evitar colores excesivos, emojis y elementos decorativos.
- Usar el nombre `Acta_Reunion_[Proyecto]_[AAAA-MM-DD].docx` cuando los datos estén disponibles.

Para HTML interactivo:

- Crear un único archivo `.html`, autocontenido y adaptable a escritorio y móvil.
- Incluir navegación o secciones plegables solo si el contenido lo justifica.
- Incluir controles útiles para imprimir y expandir/contraer secciones cuando existan varias.
- Mantener accesibilidad, buena legibilidad y una presentación profesional.
- No agregar contenido distinto del borrador aprobado.
- Usar el nombre `Acta_Reunion_[Proyecto]_[AAAA-MM-DD].html` cuando los datos estén disponibles.

## Estructura adaptable del acta

Usar las siguientes secciones como catálogo, no como lista obligatoria. Incluir únicamente las necesarias y renumerar consecutivamente las que permanezcan.

### Información general

Incluir los datos disponibles que ayuden a identificar la reunión:

- Nombre del proyecto o tema.
- Fecha y horas de inicio y fin.
- Lugar o medio de reunión.
- Participantes y roles.

Preferir una tabla compacta. Omitir campos desconocidos que no sean críticos.

### Objetivo y agenda

Incluir cuando el propósito o los temas tratados estén claros:

- Objetivo central de la reunión.
- Orden del día o temas abordados.

No reconstruir una agenda que no existió; en ese caso, resumir solo el objetivo.

### Levantamiento técnico

Esta es la sección principal cuando la reunión trata sobre software, procesos o producto. Dividirla solo en las subsecciones que contengan información real:

- **Requerimientos funcionales:** acciones, procesos o resultados esperados del sistema.
- **Requerimientos no funcionales:** restricciones de rendimiento, seguridad, usabilidad, diseño, compatibilidad u operación.
- **Reglas de negocio:** políticas, cálculos, condiciones y excepciones que el sistema debe respetar.
- **Historias de usuario:** incluirlas únicamente si fueron solicitadas, expresadas con claridad o si el enfoque ágil aporta valor. Usar “Como [rol], quiero [necesidad], para [beneficio]”.

No crear subsecciones vacías ni deducir detalles técnicos no mencionados.

### Acuerdos y decisiones

Incluir cuando existan decisiones aprobadas o asuntos que requieran seguimiento:

- Decisiones y acuerdos confirmados.
- Temas pendientes, dudas o bloqueos.

Separar lo aprobado de lo pendiente. Una propuesta discutida no es una decisión.

### Próximos pasos

Incluir solo las tareas o compromisos identificados. Usar una tabla compacta:

| Tarea | Responsable | Fecha límite |
|---|---|---|
| [Acción concreta] | [Nombre o Por confirmar] | [Fecha o Por confirmar] |

No agregar prioridad, estado, dependencia u otras columnas si no fueron necesarias o mencionadas.

### Cierre y aprobación

Incluir únicamente los elementos disponibles o solicitados:

- Fecha de la próxima reunión.
- Espacio de aprobación o firmas de los involucrados principales.

No incluir firmas automáticamente. Incorporarlas cuando el acta requiera validación formal, contractual o explícita del cliente/sponsor, o cuando el usuario lo solicite.

## Plantilla mínima orientativa

Adaptar esta plantilla al contenido. Eliminar toda sección o fila sin valor informativo.

```markdown
# Acta de Reunión: [Proyecto o tema]

**Estado:** [Borrador completo / Borrador con datos por confirmar]

## 1. Información General

| Campo | Detalle |
|---|---|
| Fecha | [Fecha] |
| Horario | [Inicio - Fin] |
| Medio / Lugar | [Medio o lugar] |
| Participantes | [Nombre — rol; nombre — rol] |

## 2. Objetivo y Agenda

**Objetivo:** [Propósito central]

**Temas tratados:**

- [Tema]
- [Tema]

## 3. Levantamiento Técnico

### Requerimientos funcionales

- [Requerimiento verificable]

### Reglas de negocio

- [Regla o condición]

## 4. Acuerdos y Decisiones

### Confirmados

- [Acuerdo o decisión]

### Pendientes o bloqueos

- [Punto pendiente y acción necesaria]

## 5. Próximos Pasos

| Tarea | Responsable | Fecha límite |
|---|---|---|
| [Tarea] | [Responsable] | [Fecha] |

## 6. Cierre y Aprobación

**Próxima reunión:** [Fecha y objetivo]

**Aprobación:**

| Nombre y rol | Firma / aprobación | Fecha |
|---|---|---|
| [Nombre] |  |  |
```

## Estilo de redacción

- Escribir de forma profesional, breve y clara.
- Usar verbos concretos: “se acordó”, “se aprobó” o “quedó pendiente” solo cuando la evidencia lo permita.
- Evitar repeticiones, conclusiones obvias y lenguaje ornamental.
- Formular requerimientos de manera comprobable.
- Conservar términos técnicos y nombres propios tal como fueron confirmados.

## Validación antes de presentar el borrador

Comprobar que:

- No se inventó información.
- Solo aparecen secciones con contenido útil.
- Los acuerdos están separados de propuestas y pendientes.
- Los requerimientos son claros y no mezclan soluciones asumidas.
- Las tareas indican responsable y fecha cuando fueron definidos; de lo contrario, el vacío relevante está marcado como `[Por confirmar]`.
- El acta se muestra primero en pantalla.
- La respuesta termina ofreciendo Word, HTML interactivo o cambios al borrador.

## Ejemplo de invocación

```text
$acta-reunion-simple

Genera un acta breve a partir de estas notas. Incluye únicamente lo que esté sustentado y muéstrame primero el borrador en pantalla. Después podré elegir Word o HTML interactivo.

[Pegar transcripción o notas]
```
