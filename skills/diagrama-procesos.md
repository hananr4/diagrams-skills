# Skill: $diagrama-procesos

## Activador
Cuando el usuario escriba:

`$diagrama-procesos`

debes generar un diagrama de **proceso de negocio (BPMN)** usando la información disponible en el chat actual (o la que el usuario provea explícitamente).

## Objetivo
Transformar una conversación, requerimiento, procedimiento operativo o flujo de negocio en un diagrama **BPMN 2.0** profesional, editable en draw.io / diagrams.net, con formato `.drawio`.

El resultado debe ayudar a identificar:

- **Pool** (la organización/proceso completo) y **lanes** (roles, áreas o sistemas que ejecutan actividades dentro del pool).
- **Eventos**: inicio (mensaje, ninguno), intermedios (temporizador, mensaje, múltiple), de límite (boundary: error, escalación), de fin (normal, terminar).
- **Actividades/tareas** con su tipo de marcador BPMN (manual, script, envío/recepción de mensaje, abstracta/subproceso).
- **Compuertas (gateways)**: exclusiva (XOR), paralela (AND), basada en eventos, con sus ramas y condiciones de salida.
- **Flujos de secuencia** (dentro de un mismo pool/lane) y **flujos de mensaje** (entre pools/participantes distintos, línea punteada con ícono de sobre).
- **Artefactos de datos o sistemas externos** referenciados por el proceso (ej. sistema de inventario).
- Vacíos de información que requieren validación.

## Formato de salida obligatorio
Entregar siempre:

1. **Resumen textual del proceso**
2. **Tabla de lanes/participantes**
3. **Tabla de actividades y eventos en orden de flujo**
4. **Tabla de compuertas y condiciones de rama**
5. **Archivo o bloque XML compatible con draw.io**
6. **Instrucciones para importar en diagrams.net**

Cuando sea posible, generar el contenido como archivo `.drawio`.

## Estilo visual requerido
El diagrama debe seguir el formato de referencia compartido por el usuario (`diagrama-proceso.drawio`):

- Archivo raíz en formato XML `<mxfile>`.
- Una página `<diagram>` con `mxGraphModel`.
- El **pool** principal como `swimlane;html=1;childLayout=stackLayout;resizeParent=1;resizeParentMax=0;horizontal=0;startSize=20;horizontalStack=0;`, con `value` igual al nombre de la organización/proceso.
- Cada **lane** (rol/área) como celda hija del pool: `swimlane;html=1;startSize=20;horizontal=0;fillColor=<color>;strokeColor=<color>;`, apiladas verticalmente dentro del pool (el `childLayout=stackLayout` las acomoda automáticamente).
- **Evento de inicio** (mensaje): `shape=mxgraph.bpmn.event;html=1;perimeter=ellipsePerimeter;outline=standard;symbol=message;` — círculo de borde simple.
- **Evento intermedio** (múltiple, temporizador, etc.): `shape=mxgraph.bpmn.event;...;outline=boundInt;symbol=<multiple|timer|message|error>;` — círculo de borde doble.
- **Evento de límite (boundary)** sobre una tarea: mismo shape de evento, `outline=boundInt` (interruptor) u `outline=boundNonint` (no interruptor), con `symbol=error`, `symbol=escalation`, etc., posicionado sobre el borde de la tarea a la que pertenece.
- **Evento de fin**: `outline=end;symbol=terminate;` (terminar) o sin símbolo para fin normal.
- **Tarea** (rectángulo redondeado): `shape=mxgraph.bpmn.task;rectStyle=rounded;size=10;taskMarker=<manual|script|send|receive|abstract|none>;`.
  - `taskMarker=manual`: tarea manual (ícono de mano).
  - `taskMarker=script`: tarea de script/automática (ícono de engranaje/script).
  - `taskMarker=send`: tarea de envío de mensaje (ícono de sobre relleno).
  - `taskMarker=abstract` + `bpmnShapeType=subprocess;isLoopSub=1`: subproceso/tarea abstracta repetible, puede combinarse con `outline=eventInt;symbol=escalation` para marcar un evento de escalación asociado.
- **Compuerta exclusiva (XOR)**: `shape=mxgraph.bpmn.gateway2;perimeter=rhombusPerimeter;gwType=exclusive;` — rombo, con o sin marca de "X" según el símbolo elegido; etiqueta de pregunta en el `value` (ej. `"All items?"`).
- **Compuerta paralela (AND)**: mismo shape con `gwType=parallel;` — rombo con cruz "+"; suele usarse `fillColor=#E6E6E6` para diferenciarla visualmente.
- **Flujo de secuencia** (dentro del mismo pool, entre lanes del mismo pool incluido): `edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;` con `startArrow=none;endArrow=classic;endFill=1;` línea continua.
- **Etiqueta de condición de rama** sobre un flujo de secuencia que sale de una compuerta: celda hija del edge, `edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;points=[];` con el texto de la condición (ej. `"Payment received"`, `"Item not available"`, `"In stock"`).
- **Flujo de mensaje** (entre el pool principal y otro participante/pool, ej. Cliente): `endArrow=blockThin;html=1;dashed=1;dashPattern=8 4;endFill=0;startArrow=oval;startFill=0;edgeStyle=orthogonalEdgeStyle;` línea punteada con círculo en el origen y flecha delgada en el destino; lleva como celda hija un ícono `shape=message;html=1;outlineConnect=0;labelPosition=center;verticalLabelPosition=bottom;` con el nombre del mensaje (ej. `"Order"`, `"Invoice"`, `"Receipt"`).
- **Sistema/artefacto externo** (ej. sistema de inventario) como un swimlane plano fuera del pool: `swimlane;startSize=70;horizontal=0;swimlaneFillColor=#E6E6E6;fillColor=#E6E6E6;`, conectado a las tareas relevantes con línea punteada sin flecha: `edgeStyle=elbowEdgeStyle;dashed=1;dashPattern=1 4;endArrow=none;startArrow=none;`.
- Cada lane mantiene su propia paleta de color (fillColor/strokeColor) consistente entre la lane y, opcionalmente, sus eventos de fin sin relleno explícito (`fillColor=#FFFFFF`).
- Distribución de izquierda a derecha según el orden temporal del proceso; las lanes se apilan de arriba hacia abajo dentro del pool en el orden de intervención de cada rol.
- Líneas limpias, uso de `jumpStyle=arc;jumpSize=13` en flujos que se cruzan para evitar ambigüedad visual.
- Compatible con diagrams.net / draw.io.

## Reglas de análisis
Antes de crear el diagrama:

1. Identifica el **proceso de negocio** que se está modelando y su disparador (evento de inicio).
2. Identifica los **participantes/lanes** explícitos (roles, departamentos, sistemas) mencionados en el chat, y agrúpalos en un único pool si pertenecen a la misma organización, o en pools separados si son organizaciones/participantes externos (ej. Cliente).
3. Determina la **secuencia de actividades** y el orden temporal en que cada lane las ejecuta.
4. Identifica **compuertas de decisión** (exclusivas) y **bifurcaciones paralelas** (paralelas), con sus condiciones de salida etiquetadas.
5. Identifica **eventos intermedios** (temporizadores, mensajes recibidos/enviados, errores) y **eventos de límite** asociados a tareas específicas.
6. Identifica los **flujos de mensaje** entre el proceso y participantes externos (cliente, proveedor, sistema externo).
7. No inventes lanes, tareas, compuertas ni mensajes como hechos confirmados.
8. Si agregas elementos inferidos, márcalos como **hipótesis**.
9. Identifica el o los **eventos de fin** del proceso (normal o de terminación forzada).
10. Si falta información, agrega una sección de **preguntas abiertas**, pero no bloquees la generación.

## Marcado de relevancia
Clasifica cada lane, actividad o compuerta como:

- **Núcleo**: paso esencial del proceso, sin el cual el flujo no se completa.
- **Complementario**: enriquece el proceso (recordatorios, actualizaciones de inventario, notificaciones) pero no es bloqueante para el camino feliz.
- **Hipótesis**: posible lane, actividad, compuerta o mensaje no confirmado por el chat.

En el diagrama:

- No saturar con demasiados colores: una paleta por lane.
- Máximo recomendado: 8-10 actividades visibles por lane en el diagrama principal.
- Si hay más, agrupar en subprocesos (`taskMarker=abstract;bpmnShapeType=subprocess`) o dejar en tabla y referenciar como "ver detalle".

## Estructura de respuesta esperada

### 1. Alcance del proceso
Describe en una frase el proceso de negocio y su propósito principal.

### 2. Lectura ejecutiva
Resume en 3 a 6 líneas qué lanes/participantes intervienen y cómo colaboran para completar el proceso.

### 3. Tabla de lanes/participantes

| Lane/Participante | Pool | Rol en el proceso | Relevancia | Evidencia del chat |
|---|---|---|---|---|

### 4. Tabla de actividades y eventos

| # | Lane | Elemento | Tipo (evento inicio/intermedio/fin, tarea, subproceso) | Marcador BPMN | Relevancia |
|---|---|---|---|---|---|

### 5. Tabla de compuertas y condiciones

| Compuerta | Tipo (exclusiva/paralela) | Rama | Condición/etiqueta | Destino | Relevancia |
|---|---|---|---|---|---|

### 6. Tabla de flujos de mensaje

| # | Origen | Destino | Mensaje | Relevancia |
|---|---|---|---|---|

### 7. Diagrama draw.io
Genera XML válido con esta estructura base:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram name="Diagrama de Proceso" id="proceso-001">
    <mxGraphModel dx="1064" dy="779" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="850" pageHeight="1100" math="0" shadow="0">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>
        <!-- Celdas generadas aquí -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Reglas técnicas para el XML draw.io
El XML debe ser importable en diagrams.net.

Usa:

- `mxCell` para pools, lanes, eventos, tareas, compuertas, sistemas externos y textos de etiqueta (`vertex="1"`), y para flujos de secuencia y de mensaje (`edge="1"`).
- El pool principal es `parent="1"`; cada lane es `parent="<id-del-pool>"`; cada evento/tarea/compuerta es `parent="<id-de-la-lane>"` correspondiente.
- Los flujos de secuencia dentro del pool son `parent="<id-de-la-lane>"` si conectan elementos de la misma lane, o `parent="<id-del-pool>"` si conectan elementos de lanes distintas dentro del mismo pool.
- Los flujos de mensaje entre pools distintos (ej. proceso ↔ Cliente) son `parent="1"`.
- `mxGeometry` con coordenadas explícitas (`x`, `y`, `width`, `height`) para pools, lanes, eventos, tareas y compuertas; geometría relativa para etiquetas de condición y de mensaje (celdas hijas de un edge).
- IDs únicos, simples y consistentes (ej. `pool-1`, `lane-ventas`, `evt-inicio-1`, `task-1`, `gw-1`, `msg-1`).
- Escapar caracteres especiales XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique

### Estilos de referencia (tomados de diagrama-proceso.drawio)

Pool:
```
swimlane;html=1;childLayout=stackLayout;resizeParent=1;resizeParentMax=0;horizontal=0;startSize=20;horizontalStack=0;
```
Geometría: `width` suficiente para todo el flujo horizontal; `height` suma de las alturas de sus lanes.

Lane:
```
swimlane;html=1;startSize=20;horizontal=0;fillColor=<color>;strokeColor=<color>;
```
Geometría: `width` igual al pool menos el margen; `height` según cantidad de actividades apiladas que contenga.

Evento de inicio (mensaje):
```
shape=mxgraph.bpmn.event;html=1;verticalLabelPosition=bottom;labelBackgroundColor=#ffffff;verticalAlign=top;align=center;perimeter=ellipsePerimeter;outlineConnect=0;aspect=fixed;outline=standard;symbol=message;
```
Geometría: `width=50`, `height=50`.

Evento intermedio (múltiple/temporizador/error):
```
shape=mxgraph.bpmn.event;html=1;verticalLabelPosition=bottom;labelBackgroundColor=#ffffff;verticalAlign=top;align=center;perimeter=ellipsePerimeter;outlineConnect=0;aspect=fixed;outline=boundInt;symbol=<multiple|timer|message|error>;fillColor=#FFFFFF;
```
Geometría: `width=35-50`, `height=35-50`.

Evento de límite (boundary, sobre una tarea, no interruptor):
```
shape=mxgraph.bpmn.event;html=1;perimeter=ellipsePerimeter;outline=boundNonint;symbol=escalation;
```
Geometría pequeña (`width≈39`, `height≈39`), posicionado sobre el borde inferior/lateral de la tarea padre.

Evento de fin (terminar):
```
shape=mxgraph.bpmn.event;html=1;perimeter=ellipsePerimeter;outlineConnect=0;aspect=fixed;outline=end;symbol=terminate;fillColor=#FFFFFF;
```
Geometría: `width=30`, `height=30`.

Tarea (manual/script/envío/abstracta):
```
shape=mxgraph.bpmn.task;rectStyle=rounded;size=10;taskMarker=<manual|script|send|abstract>;
```
Para subproceso repetible agrega: `bpmnShapeType=subprocess;isLoopSub=1;outline=eventInt;symbol=escalation;`.
Geometría sugerida: `width=90-134`, `height=60-90`.

Compuerta exclusiva (XOR):
```
shape=mxgraph.bpmn.gateway2;html=1;perimeter=rhombusPerimeter;outlineConnect=0;outline=none;symbol=none;gwType=exclusive;fillColor=#FFFFFF;
```
Geometría: `width=40-50`, `height=35-55`. `value` con la pregunta de decisión si aplica (ej. `"All items?"`).

Compuerta paralela (AND):
```
shape=mxgraph.bpmn.gateway2;html=1;perimeter=rhombusPerimeter;outlineConnect=0;outline=none;symbol=none;gwType=parallel;fillColor=#E6E6E6;
```
Geometría: `width=50`, `height=55`.

Flujo de secuencia (línea continua):
```
edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;startArrow=none;startFill=0;endArrow=classic;endFill=1;strokeColor=#000000;strokeWidth=1;
```
Agrega `jumpStyle=arc;jumpSize=13` si el flujo cruza otras líneas.

Etiqueta de condición sobre un flujo de secuencia:
```
edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;points=[];
```
`value` con el texto de la condición (ej. `"Payment received"`, `"In stock"`, `"Missing items"`).

Flujo de mensaje (línea punteada entre pools/participantes):
```
endArrow=blockThin;html=1;labelPosition=left;verticalLabelPosition=middle;align=right;verticalAlign=middle;dashed=1;dashPattern=8 4;endFill=0;startArrow=oval;startFill=0;endSize=6;startSize=4;rounded=1;edgeStyle=orthogonalEdgeStyle;strokeWidth=1;
```
Como celda hija (icono del mensaje):
```
shape=message;html=1;outlineConnect=0;labelPosition=center;verticalLabelPosition=bottom;align=center;verticalAlign=top;spacingRight=5;labelBackgroundColor=#ffffff;
```
Geometría del icono: `width=40`, `height=26`, posicionado a mitad del recorrido del flujo. `value` con el nombre del mensaje (ej. `"Order"`, `"Invoice"`, `"Receipt"`, `"Payment"`, `"Reminder"`).

Conexión a sistema/artefacto externo (línea punteada sin flecha):
```
edgeStyle=elbowEdgeStyle;fontSize=12;html=1;endFill=0;startFill=0;endSize=6;startSize=6;dashed=1;dashPattern=1 4;endArrow=none;startArrow=none;strokeWidth=2;
```

Sistema/artefacto externo (swimlane plano):
```
swimlane;startSize=70;horizontal=0;labelBackgroundColor=none;strokeColor=#666666;fontColor=#333333;swimlaneFillColor=#E6E6E6;fillColor=#E6E6E6;
```

## Layout sugerido
Usa coordenadas base (replicando la disposición del archivo de referencia):

- Pool principal: `x=-370, y=250` aproximadamente, ancho suficiente para todo el proceso horizontal (ej. `width≈1810`).
- Lanes apiladas dentro del pool en el orden de intervención de cada rol (ej. `Accounts` arriba, `Warehouse` en medio, `Purchasing` debajo), cada una con `height≈160-180`.
- Evento de inicio al extremo izquierdo de la primera lane (`x≈60-80`).
- Tareas distribuidas de izquierda a derecha siguiendo el orden temporal del proceso, separadas ~100-150px entre sí.
- Compuertas justo antes de las ramas de decisión/paralelización, con las ramas distribuidas verticalmente alrededor del eje horizontal del flujo principal.
- Eventos de fin al extremo derecho del flujo correspondiente.
- Pool/participante externo (ej. `Client`) debajo del pool principal, con flujos de mensaje verticales conectando ambos.
- Sistema externo (ej. `Inventory management system`) sobre el pool principal, conectado por líneas punteadas a las tareas que lo consultan/actualizan.

## Paleta sugerida
Usa una paleta distinta por lane/participante:

- Azul (lane de cuentas/finanzas): `fillColor=#dae8fc;strokeColor=#4E668A`
- Verde (lane de almacén/operaciones): `fillColor=#d5e8d4;strokeColor=#688F51`
- Naranja (lane de compras/abastecimiento): `fillColor=#ffe6cc;strokeColor=#AB7B00`
- Rojo suave (pool/participante externo, ej. Cliente): `fillColor=#f8cecc;strokeColor=#944440`
- Gris (sistema externo/artefacto de datos): `fillColor=#E6E6E6;strokeColor=#666666`
- Blanco (eventos y compuertas, para resaltar sobre el color de la lane): `fillColor=#FFFFFF;strokeColor=#000000`

## Ejemplo de invocación
Usuario:

`$diagrama-procesos genera el diagrama de proceso de aprobación de créditos de la banca móvil`

Respuesta esperada:

- Identificar lanes (ej. `Atención al cliente`, `Análisis de riesgo`, `Tesorería`) y, si aplica, un pool externo (ej. `Cliente`).
- Listar actividades y eventos en orden de flujo, con su marcador BPMN.
- Marcar compuertas de decisión/paralelización con sus condiciones de rama.
- Identificar flujos de mensaje entre el proceso y el cliente u otros sistemas.
- Entregar XML `.drawio`.

## Prompt interno recomendado
Cuando se active `$diagrama-procesos`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica el proceso de negocio descrito, sus lanes/participantes (roles, áreas, sistemas), y si existe un participante externo que requiera un pool separado (ej. Cliente). Usa únicamente información explícita del chat; si agregas inferencias, márcalas como hipótesis. Determina la secuencia de actividades y eventos (inicio, intermedios, de límite, de fin) por lane, las compuertas de decisión exclusivas/paralelas con sus condiciones de rama, y los flujos de mensaje entre el proceso y participantes externos o sistemas. Genera una tabla de lanes/participantes, una tabla de actividades/eventos, una tabla de compuertas/condiciones y una tabla de flujos de mensaje. Luego genera un archivo XML `.drawio` compatible con diagrams.net, con estructura `<mxfile>`, una página `<diagram>`, `mxGraphModel`, un pool como `swimlane;childLayout=stackLayout` que contiene lanes como `swimlane` apiladas, eventos como `shape=mxgraph.bpmn.event` con el `symbol` y `outline` correspondiente, tareas como `shape=mxgraph.bpmn.task` con el `taskMarker` adecuado, compuertas como `shape=mxgraph.bpmn.gateway2` con `gwType` exclusive o parallel, flujos de secuencia con `endArrow=classic`, y flujos de mensaje punteados con ícono `shape=message` hacia/desde participantes externos. El XML debe ser válido, editable e importable en draw.io.

## Validaciones antes de entregar
Antes de responder, verifica:

- El alcance del proceso está claro y tiene al menos un evento de inicio y un evento de fin.
- Cada lane interviene en al menos una actividad o evento.
- Las actividades y eventos no están inventados como hechos; lo inferido está marcado como hipótesis.
- Cada compuerta de decisión tiene al menos dos ramas con condiciones claramente etiquetadas.
- Los flujos de mensaje conectan participantes/pools distintos, no elementos dentro del mismo pool.
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>`, `<root>`.
- Todos los `mxCell` tienen IDs únicos y `parent` correcto (lanes dentro del pool, actividades/eventos dentro de su lane).
- El archivo puede guardarse con extensión `.drawio`.
- El usuario puede importar el contenido en diagrams.net.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `diagrama-proceso.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File → Open From → Device**.
5. Abre el archivo `.drawio`.
6. Edita textos, colores o posiciones si hace falta.

## Variante corta para llamar desde cualquier chat
`$diagrama-procesos: toma el contexto actual, identifica el proceso de negocio, sus lanes/participantes (incluyendo pools externos como Cliente), la secuencia de actividades y eventos (inicio/intermedio/límite/fin) con su marcador BPMN, las compuertas de decisión exclusivas/paralelas con condiciones de rama, y los flujos de mensaje entre participantes, genera las tablas correspondientes, y entrega un archivo draw.io editable con formato de diagrama de proceso BPMN profesional, usando la paleta y estilos del archivo diagrama-proceso.drawio de referencia. No inventes información; lo inferido márcalo como hipótesis.`
