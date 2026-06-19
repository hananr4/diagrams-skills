# Skill: $diagrama-secuencia

## Activador
Cuando el usuario escriba:

`$diagrama-secuencia`

debes generar un diagrama UML de **secuencia** usando la información disponible en el chat actual (o la que el usuario provea explícitamente).

## Objetivo
Transformar una conversación, requerimiento, flujo funcional o caso de uso en un diagrama de secuencia UML profesional, editable en draw.io / diagrams.net, con formato `.drawio`.

El resultado debe ayudar a identificar:

- Actores y objetos/participantes que intervienen en el flujo (lifelines).
- Mensajes (llamadas síncronas, de retorno, de auto-llamada) en orden temporal, numerados jerárquicamente.
- Bloques de control: `alt` (alternativa), `opt` (opcional), `loop` (ciclo), con sus condiciones de guarda.
- Activaciones (barras de ejecución) sobre cada lifeline durante el procesamiento de un mensaje.
- Destrucción de objetos (`umlDestroy`) cuando aplique.
- Vacíos de información que requieren validación.

## Formato de salida obligatorio
Entregar siempre:

1. **Resumen textual del flujo**
2. **Tabla de participantes**
3. **Tabla de mensajes en orden secuencial**
4. **Archivo o bloque XML compatible con draw.io**
5. **Instrucciones para importar en diagrams.net**

Cuando sea posible, generar el contenido como archivo `.drawio`.

## Estilo visual requerido
El diagrama debe seguir el formato de referencia compartido por el usuario (`diagrama-secuencia.drawio`):

- Archivo raíz en formato XML `<mxfile>`.
- Una página `<diagram>` con `mxGraphModel`.
- Cada participante representado como un `shape=umlLifeline` (línea de vida vertical) con `container=1;collapsible=0;recursiveResize=0;outlineConnect=0`.
  - Actor (persona): agregar `participant=umlActor` y colores tipo `fillColor=#f8cecc;strokeColor=#b85450`.
  - Entidad/sistema externo: agregar `participant=umlEntity`.
  - Objeto/control/formulario: `shape=umlLifeline` simple sin `participant`.
- El nombre del participante va en el `value` con formato `:NombreClase` (notación de instancia anónima UML).
- Activaciones (barras de ejecución) como celdas hijas (`parent="<id-lifeline>"`) con estilo `html=1;points=[];perimeter=orthogonalPerimeter;fillColor=<color>;strokeColor=<color>` y geometría relativa (`x`, `y`, `width≈10`, `height` según duración).
- Mensajes síncronos (llamada) como `edge=1` con `endArrow=block;rounded=0;entryX=0;entryY=0` (o `entryX=1` según dirección), conectando una activación/lifeline origen con una activación/lifeline destino. Etiqueta numerada jerárquicamente (`1:`, `1.1:`, `1.2:`, `1.2.1:`, etc.) seguida del nombre del mensaje y parámetros (ej. `1: itemSearch(itemName)`).
- Mensajes de retorno como `edge=1` con `dashed=1;endArrow=open;endFill=0`, sin numerar o con la etiqueta de retorno entre paréntesis si se requiere.
- Auto-mensajes (un participante se llama a sí mismo) como `edge=1` con `source` y `target` iguales y geometría con `sourcePoint`/`targetPoint` cercanos (pequeño loop).
- Bloque de control (`alt`, `opt`, `loop`) como `shape=umlFrame;whiteSpace=wrap;fillColor=#f5f5f5;strokeColor=#666666`, ubicado detrás de los lifelines que abarca (debe dibujarse primero o con `parent="1"` y geometría que englobe la zona).
- Condiciones de guarda como cajas de texto (`text;html=1;align=center;verticalAlign=middle;strokeColor=none;fillColor=none`) con valor `[condición]` (ej. `[itemName=valid]`, `[else]`), posicionadas en cada segmento del frame.
- Línea divisoria entre segmentos del frame `alt`/`opt` como `edge=1` con `dashed=1;endArrow=none`, conectando el frame consigo mismo a la altura de la división.
- Destrucción de objeto con `shape=umlDestroy;whiteSpace=wrap;strokeWidth=3` (aspa X), colocada al final de la lifeline del objeto destruido.
- Cada participante mantiene su propia paleta de color (fillColor/strokeColor) consistente entre lifeline y sus activaciones.
- Distribución horizontal: participantes en columnas de izquierda a derecha en el orden en que intervienen por primera vez en el flujo.
- Líneas limpias, sin cruces innecesarios, texto legible.
- Compatible con diagrams.net / draw.io.

## Reglas de análisis
Antes de crear el diagrama:

1. Identifica el **flujo o caso de uso** que se está modelando.
2. Identifica los **participantes** explícitos (actor, formularios, controladores, entidades, sistemas externos) mencionados en el chat.
3. Determina el **orden temporal** de los mensajes/llamadas entre participantes.
4. Numera los mensajes jerárquicamente: mensaje raíz `1`, sub-llamadas `1.1`, `1.2`, sub-sub-llamadas `1.1.1`, etc., respetando el orden de anidamiento de las activaciones.
5. Identifica **condiciones de guarda** o ramas alternativas (`alt`/`else`, `opt`, `loop`) y agrúpalas en el frame correspondiente.
6. No inventes participantes ni mensajes como hechos confirmados.
7. Si agregas elementos inferidos (mensajes, retornos, condiciones), márcalos como **hipótesis**.
8. Identifica si algún objeto se **destruye** al final de su ciclo de vida en el flujo.
9. Si falta información, agrega una sección de **preguntas abiertas**, pero no bloquees la generación.
10. Usa convención UML para nombrar mensajes: `nombreMetodo(parámetros)`, y opcionalmente `: tipoRetorno` en el mensaje de retorno.

## Marcado de relevancia
Clasifica cada participante o mensaje como:

- **Núcleo**: paso esencial del flujo, sin el cual el caso de uso no se completa.
- **Complementario**: enriquece el flujo (validaciones, logging, notificaciones) pero no es bloqueante.
- **Hipótesis**: posible participante, mensaje o condición no confirmada por el chat.

En el diagrama:

- No saturar con demasiados colores: una paleta por participante.
- Máximo recomendado: 8-10 mensajes visibles en el diagrama principal por bloque de control.
- Si hay más, agrupar en sub-flujos o dejar en tabla y referenciar como "ver detalle".

## Estructura de respuesta esperada

### 1. Alcance del flujo
Describe en una frase el caso de uso/flujo y su propósito principal.

### 2. Lectura ejecutiva
Resume en 3 a 6 líneas qué participantes intervienen y cómo colaboran para completar el flujo.

### 3. Tabla de participantes

| Participante | Tipo (actor/objeto/entidad) | Rol en el flujo | Relevancia | Evidencia del chat |
|---|---|---|---|---|

### 4. Tabla de mensajes

| # | Origen | Destino | Mensaje | Tipo (síncrono/retorno/auto-mensaje) | Condición/guarda | Relevancia |
|---|---|---|---|---|---|---|

### 5. Diagrama draw.io
Genera XML válido con esta estructura base:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram name="Diagrama de Secuencia" id="secuencia-001">
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

- `mxCell` para lifelines, activaciones, frames, textos de guarda y destrucción (`vertex="1"`), y para mensajes/retornos/auto-mensajes/divisiones de frame (`edge="1"`).
- Cada lifeline es `parent="1"`; sus activaciones y destrucción son `parent="<id-de-la-lifeline>"`.
- `mxGeometry` con coordenadas explícitas (`x`, `y`, `width`, `height`) para lifelines, frames y textos de guarda; geometría relativa (sin `x` global, sino relativa al contenedor) para activaciones dentro de su lifeline.
- Los mensajes (`edge="1"`) usan `source` y `target` apuntando preferentemente a las **activaciones** (no a la lifeline completa) para mayor precisión visual.
- IDs únicos, simples y consistentes (ej. `actor-cliente`, `act-form-1`, `msg-1`, `msg-1-1`, `frame-alt-1`).
- Escapar caracteres especiales XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique

### Estilos de referencia (tomados de diagrama-secuencia.drawio)

Frame de control (`alt`/`opt`/`loop`):
```
shape=umlFrame;whiteSpace=wrap;html=1;fillColor=#f5f5f5;fontColor=#333333;strokeColor=#666666;
```
Geometría: debe englobar a todos los lifelines y mensajes del bloque, con `value="alt"`, `"opt"` o `"loop"` según corresponda.

Lifeline de actor:
```
shape=umlLifeline;participant=umlActor;perimeter=lifelinePerimeter;html=1;container=1;collapsible=0;recursiveResize=0;verticalAlign=top;spacingTop=36;outlineConnect=0;size=40;fillColor=#f8cecc;strokeColor=#b85450;
```
Geometría sugerida: `width=20`, `height≈530`.

Lifeline de objeto/formulario:
```
shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;fillColor=<color>;strokeColor=<color>;
```
Geometría sugerida: `width=100`, `height≈520`.

Lifeline de entidad/sistema externo:
```
shape=umlLifeline;participant=umlEntity;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;verticalAlign=top;spacingTop=36;outlineConnect=0;fillColor=<color>;strokeColor=<color>;
```

Activación (barra de ejecución), celda hija de la lifeline:
```
html=1;points=[];perimeter=orthogonalPerimeter;fillColor=<color>;strokeColor=<color>;
```
Geometría relativa al contenedor: `x≈45-50`, `width=10`, `height` proporcional a la duración del procesamiento.

Mensaje síncrono (llamada), numerado jerárquicamente:
```
edgeStyle=orthogonalEdgeStyle;html=1;align=left;spacingLeft=2;endArrow=block;rounded=0;entryX=1;entryY=0;
```
o, para llamadas directas entre lifelines/activaciones:
```
html=1;verticalAlign=bottom;endArrow=block;entryX=0;entryY=0;rounded=0;
```
`value` con formato `"1.2: nombreMetodo(parametros)"`.

Mensaje de retorno (línea punteada):
```
edgeStyle=none;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;endArrow=open;endFill=0;dashed=1;
```

Auto-mensaje (loop sobre el propio participante):
```
endArrow=none;dashed=1;html=1;rounded=0;entryX=1;entryY=0.576;entryDx=0;entryDy=0;entryPerimeter=0;exitX=0;exitY=0.573;exitDx=0;exitDy=0;exitPerimeter=0;
```
con `source` y `target` apuntando al mismo elemento (ej. el propio frame o lifeline) y geometría con `sourcePoint`/`targetPoint` formando un pequeño bucle.

Condición de guarda (texto):
```
text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;
```
`value` con formato `"[condición]"` (ej. `[itemName=valid]`, `[else]`).

Destrucción de objeto:
```
shape=umlDestroy;whiteSpace=wrap;html=1;strokeWidth=3;
```
Geometría: aspa pequeña (`width=30`, `height=30`) al final de la lifeline destruida.

Título y subtítulo (cajas de texto):
```
text;html=1;whiteSpace=wrap;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;rounded=0;
```

## Layout sugerido
Usa coordenadas base (replicando la disposición del archivo de referencia):

- Frame de control (`alt`): `x=200, y=240, width≈620, height≈330` (debe envolver visualmente a los lifelines y mensajes que agrupa).
- Lifelines distribuidas en columnas de izquierda a derecha según orden de aparición, separadas ~150-220px entre sí (ej. `x=130`, `x=270`, `x=490`, `x=660`, `x=740`).
- Altura de lifeline uniforme entre participantes del mismo diagrama (ej. `y=80-90`, `height≈520-530`).
- Activaciones posicionadas en el eje vertical según el momento en que se reciben/procesan mensajes.
- Condiciones de guarda (`[condición]`) ubicadas en la esquina superior izquierda de cada segmento del frame.
- Título del diagrama: `x=40, y=20, width=290, height=30` (si se incluye).

Cada mensaje fluye de izquierda a derecha (llamada) o de derecha a izquierda con línea punteada (retorno), respetando el eje temporal de arriba hacia abajo.

## Paleta sugerida
Usa una paleta distinta por participante:

- Rojo suave (actor/usuario): `fillColor=#f8cecc;strokeColor=#b85450`
- Naranja (formulario/UI): `fillColor=#ffe6cc;strokeColor=#d79b00`
- Azul (objeto de resultados/control): `fillColor=#dae8fc;strokeColor=#6c8ebf`
- Morado (entidad/repositorio de datos): `fillColor=#e1d5e7;strokeColor=#9673a6`
- Verde (lista/colección/servicio de soporte): `fillColor=#d5e8d4;strokeColor=#82b366`
- Amarillo (servicio externo/integración): `fillColor=#fff2cc;strokeColor=#d6b656`
- Gris (frame de control/sistema externo): `fillColor=#f5f5f5;strokeColor=#666666`

## Ejemplo de invocación
Usuario:

`$diagrama-secuencia genera el diagrama de secuencia del flujo de búsqueda de productos en el módulo de catálogo`

Respuesta esperada:

- Identificar participantes (ej. `Cliente`, `FormularioBusqueda`, `ResultadosBusqueda`, `BaseDatosProductos`).
- Listar mensajes en orden secuencial con numeración jerárquica.
- Marcar bloques de control (`alt`/`opt`/`loop`) con sus condiciones de guarda.
- Entregar XML `.drawio`.

## Prompt interno recomendado
Cuando se active `$diagrama-secuencia`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica los participantes (actor, objetos, entidades) del flujo o caso de uso descrito, y el orden temporal de los mensajes que intercambian. Usa únicamente información explícita del chat; si agregas inferencias, márcalas como hipótesis. Genera una tabla de participantes y una tabla de mensajes numerados jerárquicamente (1, 1.1, 1.2, 1.2.1...) indicando origen, destino, tipo (síncrono/retorno/auto-mensaje) y condición de guarda si aplica. Luego genera un archivo XML `.drawio` compatible con diagrams.net, con estructura `<mxfile>`, una página `<diagram>`, `mxGraphModel`, participantes como `shape=umlLifeline` (con `participant=umlActor` o `participant=umlEntity` según corresponda), activaciones como celdas hijas de cada lifeline, mensajes síncronos con `endArrow=block`, retornos con `dashed=1;endArrow=open;endFill=0`, bloques de control como `shape=umlFrame` con condiciones de guarda en cajas de texto, y destrucción de objetos con `shape=umlDestroy` cuando aplique. El XML debe ser válido, editable e importable en draw.io.

## Validaciones antes de entregar
Antes de responder, verifica:

- El alcance del flujo está claro.
- Cada participante interviene en al menos un mensaje.
- Los mensajes no están inventados como hechos; lo inferido está marcado como hipótesis.
- La numeración jerárquica de mensajes respeta el anidamiento de las activaciones (sub-llamadas numeradas dentro de su llamada padre).
- Los bloques de control (`alt`/`opt`/`loop`) tienen condiciones de guarda claramente etiquetadas.
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>`, `<root>`.
- Todos los `mxCell` tienen IDs únicos y `parent` correcto (activaciones dentro de su lifeline).
- El archivo puede guardarse con extensión `.drawio`.
- El usuario puede importar el contenido en diagrams.net.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `diagrama-secuencia.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File → Open From → Device**.
5. Abre el archivo `.drawio`.
6. Edita textos, colores o posiciones si hace falta.

## Variante corta para llamar desde cualquier chat
`$diagrama-secuencia: toma el contexto actual, identifica participantes (actor, objetos, entidades), determina el orden temporal de los mensajes y numéralos jerárquicamente, marca bloques de control (alt/opt/loop) con sus condiciones de guarda y destrucción de objetos si aplica, genera tabla de participantes y tabla de mensajes, y entrega un archivo draw.io editable con formato de diagrama de secuencia UML profesional, usando la paleta y estilos del archivo diagrama-secuencia.drawio de referencia. No inventes información; lo inferido márcalo como hipótesis.`
