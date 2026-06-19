# Skill: $time-line-vertical

> Variante vertical de [time-line.md](time-line.md) (`$time-line`, horizontal). Usa este skill cuando el usuario escriba `$time-line-vertical`, o cuando pida explícitamente una línea de tiempo "vertical", "en columna", "de arriba hacia abajo" o "tipo lista". Si no especifica orientación, usa la horizontal (`$time-line`) por defecto.

## Activador
Cuando el usuario escriba:

`$time-line-vertical`

debes generar una **línea de tiempo / roadmap de proyecto en formato vertical** usando la información disponible en el chat actual (o la que el usuario provea explícitamente).

## Objetivo
Transformar una conversación, plan de proyecto, cronograma o roadmap en una **línea de tiempo vertical** profesional, editable en draw.io / diagrams.net, con formato `.drawio`.

El resultado debe ayudar a identificar:

- Un **eje/columna vertical central** que recorre todas las fases de arriba hacia abajo.
- **Fases o periodos** del proyecto (ej. meses, sprints) representados como barras de color, alternadas en dos columnas (izquierda/derecha) a ambos lados del eje.
- **Actividades/descripción** de cada fase, en un bloque de texto gris debajo de su barra de color, en la misma columna.
- **Conectores tipo "globo de diálogo"** (callout circular) que unen el eje central con cada fase, del color de la fase correspondiente.
- El **orden cronológico** de arriba hacia abajo.
- Vacíos de información que requieren validación.

## Formato de salida obligatorio
Entregar siempre:

1. **Resumen textual del cronograma**
2. **Tabla de fases/periodos**
3. **Archivo o bloque XML compatible con draw.io**
4. **Instrucciones para importar en diagrams.net**

Cuando sea posible, generar el contenido como archivo `.drawio`.

## Estilo visual requerido
El diagrama debe seguir el formato de referencia compartido por el usuario (`time-line-vertical.drawio`):

- Archivo raíz en formato XML `<mxfile>`.
- Una página `<diagram>` con `mxGraphModel`.
- Un **eje vertical**: una línea recta simple (`endArrow=none;html=1;strokeWidth=3;strokeColor=#CCCCCC;rounded=0;`) que conecta dos círculos pequeños sin relleno (`ellipse;fillColor=none;strokeColor=#333333;strokeWidth=2;`, `width=12`, `height=12`) ubicados en el extremo superior e inferior del recorrido (`source`/`target` del edge).
- Cada **fase** se compone de dos celdas apiladas en la misma columna:
  - Una **barra de título** (`fillColor=<color>;strokecolor=none;rounded=1;fontColor=#FFFFFF;strokeColor=none;fontStyle=1;fontSize=14;`) con `value` igual al nombre corto del periodo (ej. `"Month 1"`, `"Month 2-4"`). Geometría: `width=160`, `height=30`.
  - Un **bloque descriptivo gris** justo debajo (`rounded=1;strokeColor=none;fillColor=#EEEEEE;align=center;arcSize=12;verticalAlign=top;whiteSpace=wrap;html=1;fontSize=12;`) con `value` en HTML enriquecido: título en negrita con el color de la fase + texto descriptivo en fuente pequeña. Geometría: `width=160`, `height=70`, posicionado ~`y+50` respecto a la barra de título (se superpone parcialmente para verse como una sola tarjeta).
- Las fases **alternan columna**: columna izquierda (`x≈210`) y columna derecha (`x≈390`), descendiendo en `y` de forma escalonada para crear un patrón en zigzag vertical alrededor del eje central.
- Entre el eje central y cada fase hay un **conector tipo callout circular** (`shape=mxgraph.infographic.circularCallout2;direction=north;`), con `flipH=1` cuando la fase está en la columna derecha (para que el "pico" del globo apunte hacia el eje en la dirección correcta) y sin `flipH` cuando está en la columna izquierda. El `strokeColor` del callout coincide con el color de la fase; geometría aproximada `width=246`, `height=60`, posicionado entre el eje y la barra de título de la fase.
- Cada fase mantiene su propia paleta de color (mismo `fillColor` en la barra de título, `strokeColor` en el callout y color de fuente en el título del bloque descriptivo).
- Distribución de arriba hacia abajo según el orden cronológico de las fases.
- Sin sombras (`shadow=0`), bordes redondeados (`rounded=1`) en barras y bloques.
- Compatible con diagrams.net / draw.io.

## Reglas de análisis
Antes de crear el diagrama:

1. Identifica el **horizonte temporal** del proyecto (fecha de inicio y fin, o duración total) y la unidad de fase (meses, sprints, semanas).
2. Identifica las **fases o periodos** explícitos mencionados en el chat, en orden cronológico.
3. Para cada fase, determina su **descripción/actividades principales** (puede ser un párrafo corto, a diferencia de la variante horizontal que usa viñetas).
4. No inventes fases ni actividades como hechos confirmados.
5. Si agregas elementos inferidos, márcalos como **hipótesis**.
6. Si falta información (fechas exactas, duración de cada fase), agrega una sección de **preguntas abiertas**, pero no bloquees la generación; usa una duración proporcional razonable.

## Marcado de relevancia
Clasifica cada fase como:

- **Núcleo**: fase esencial del cronograma, sin la cual el proyecto no se completa.
- **Complementario**: fase que enriquece el cronograma pero no es bloqueante (documentación, traducciones, marketing).
- **Hipótesis**: posible fase no confirmada por el chat.

En el diagrama:

- No saturar con demasiadas fases: máximo recomendado 6-8 fases visibles en la línea de tiempo vertical principal (para que la página no quede demasiado larga).
- Un color por fase, sin reutilizar colores entre fases adyacentes.
- Mantener la descripción de cada fase breve (1-2 líneas) para que el bloque gris no crezca demasiado.

## Estructura de respuesta esperada

### 1. Alcance del cronograma
Describe en una frase el proyecto y el horizonte temporal cubierto.

### 2. Lectura ejecutiva
Resume en 3 a 6 líneas las fases principales y cómo se encadenan en el tiempo.

### 3. Tabla de fases/periodos

| # | Fase | Periodo (mes/sprint) | Descripción/actividades | Columna (izq/der) | Relevancia | Evidencia del chat |
|---|---|---|---|---|---|---|

### 4. Diagrama draw.io
Genera XML válido con esta estructura base:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram name="Línea de tiempo vertical" id="timeline-vertical-001">
    <mxGraphModel dx="1965" dy="1121" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" math="0" shadow="0">
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

- `mxCell` para los círculos extremos del eje, la línea del eje, los callouts circulares, las barras de título y los bloques descriptivos (`vertex="1"`), y para la línea del eje (`edge="1"`).
- Todas las celdas son `parent="1"` (sin agrupaciones jerárquicas, igual que en el archivo de referencia).
- `mxGeometry` con coordenadas explícitas (`x`, `y`, `width`, `height`).
- IDs únicos, simples y consistentes (ej. `axis-top`, `axis-bottom`, `axis-line`, `callout-1`, `phase-1`, `desc-1`).
- Escapar caracteres especiales XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique

### Estilos de referencia (tomados de time-line-vertical.drawio)

Círculo extremo del eje (inicio/fin):
```
ellipse;whiteSpace=wrap;html=1;aspect=fixed;shadow=0;fillColor=none;strokeColor=#333333;fontSize=16;align=center;strokeWidth=2;
```
Geometría: `width=12`, `height=12`.

Línea del eje (conecta los dos círculos extremos):
```
endArrow=none;html=1;strokeWidth=3;strokeColor=#CCCCCC;labelBackgroundColor=none;fontSize=16;rounded=0;
```
`source` = círculo superior, `target` = círculo inferior.

Callout circular (conector eje → fase), columna izquierda:
```
verticalLabelPosition=middle;verticalAlign=middle;html=1;shape=mxgraph.infographic.circularCallout2;dy=15;strokeColor=<color>;labelPosition=center;align=center;fontColor=<color>;fontStyle=1;fontSize=24;shadow=0;direction=north;
```
Columna derecha (idéntico + espejo horizontal):
```
verticalLabelPosition=middle;verticalAlign=middle;html=1;shape=mxgraph.infographic.circularCallout2;dy=15;strokeColor=<color>;labelPosition=center;align=center;fontColor=<color>;fontStyle=1;fontSize=24;shadow=0;direction=north;flipH=1;
```
Geometría: `width=246`, `height=60`.

Barra de título de fase:
```
fillColor=<color>;strokecolor=none;rounded=1;fontColor=#FFFFFF;strokeColor=none;fontStyle=1;fontSize=14;
```
`value` con el nombre corto del periodo (ej. `"Month 1"`). Geometría: `width=160`, `height=30`.

Bloque descriptivo (debajo de la barra, mismo color en el título interno):
```
rounded=1;strokeColor=none;fillColor=#EEEEEE;align=center;arcSize=12;verticalAlign=top;whiteSpace=wrap;html=1;fontSize=12;
```
`value` con HTML enriquecido:
```html
<font style="font-size: 12px" color="#10739E"><b>Requirements</b></font><br><br><font size="1">Lorem ipsum dolor sit amet, consectetur adipisicing elit</font>
```
Geometría: `width=160`, `height=70`, `y` ≈ `y` de la barra de título `+ 50`.

## Layout sugerido
Usa coordenadas base (replicando la disposición del archivo de referencia):

- Eje vertical centrado en `x≈380`, recorriendo todo el alto del diagrama (`y` desde el inicio hasta el fin del cronograma).
- Fases alternando columna y descendiendo en `y`:
  - Fase 1: columna izquierda (`x≈210`), callout sin `flipH`.
  - Fase 2: columna derecha (`x≈390`), callout con `flipH=1`.
  - Fase 3: columna izquierda.
  - Fase 4: columna derecha.
  - (continuar alternando para fases adicionales)
- Cada fase nueva desciende ~`y+70` a `y+80` respecto a la anterior, generando el escalonado en zigzag vertical.
- Barra de título y bloque descriptivo de cada fase comparten la misma `x`; el bloque descriptivo se posiciona ~50px por debajo del inicio de la barra (parcialmente superpuesto, simulando una sola tarjeta con encabezado de color).

## Paleta sugerida
Usa una paleta distinta y consistente por fase (barra, callout y título del bloque coinciden):

- Azul (fase inicial, ej. requerimientos): `fillColor=#10739E` / `strokeColor=#10739E`
- Naranja (fase de planificación): `fillColor=#F2931E` / `strokeColor=#F2931E`
- Rojo ladrillo (fase de desarrollo): `fillColor=#AE4132` / `strokeColor=#AE4132`
- Azul oscuro (fase de QA): `fillColor=#23445D` / `strokeColor=#23445D`
- Turquesa (fase de documentación): `fillColor=#12AAB5` / `strokeColor=#12AAB5`
- Morado (fase de release/lanzamiento): `fillColor=#56517E` / `strokeColor=#56517E`

Si hay más de 6 fases, agrega colores adicionales evitando tonos repetidos o muy similares entre fases adyacentes.

## Ejemplo de invocación
Usuario:

`$time-line-vertical genera el cronograma del proyecto de migración del core bancario, de enero a octubre, en formato vertical`

Respuesta esperada:

- Identificar fases (ej. `Requerimientos`, `Planificación`, `Desarrollo`, `QA`, `Documentación`, `Release`) en orden cronológico.
- Asignarles columna alternada (izquierda/derecha) y un color distinto a cada una.
- Redactar una descripción breve por fase.
- Entregar XML `.drawio` con el eje vertical, callouts circulares alternando `flipH`, y tarjetas (barra + bloque gris) en zigzag descendente.

## Prompt interno recomendado
Cuando se active `$time-line-vertical`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica el horizonte temporal del proyecto, sus fases o periodos en orden cronológico y una descripción breve de cada una. Usa únicamente información explícita del chat; si agregas inferencias, márcalas como hipótesis. Genera una tabla de fases/periodos. Luego genera un archivo XML `.drawio` compatible con diagrams.net, con estructura `<mxfile>`, una página `<diagram>`, `mxGraphModel`, un eje vertical central (línea simple entre dos círculos sin relleno), fases alternando columna izquierda/derecha en orden descendente, cada una compuesta por una barra de título de color y un bloque descriptivo gris debajo, conectadas al eje central mediante un callout circular (`shape=mxgraph.infographic.circularCallout2`) del color de la fase, con `flipH=1` en las fases de la columna derecha. El XML debe ser válido, editable e importable en draw.io.

## Validaciones antes de entregar
Antes de responder, verifica:

- El horizonte temporal está claro y las fases están en orden cronológico descendente.
- Cada fase tiene una descripción asociada.
- Las fases y descripciones no están inventadas como hechos; lo inferido está marcado como hipótesis.
- Las fases alternan correctamente columna izquierda/derecha.
- Cada fase tiene un color único y consistente entre barra, callout y título del bloque descriptivo.
- Los callouts de la columna derecha incluyen `flipH=1`; los de la izquierda no.
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>`, `<root>`.
- Todos los `mxCell` tienen IDs únicos.
- El archivo puede guardarse con extensión `.drawio`.
- El usuario puede importar el contenido en diagrams.net.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `time-line-vertical.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File → Open From → Device**.
5. Abre el archivo `.drawio`.
6. Edita textos, colores o posiciones si hace falta.

## Variante corta para llamar desde cualquier chat
`$time-line-vertical: toma el contexto actual, identifica el horizonte temporal del proyecto, sus fases o periodos en orden cronológico y una descripción breve de cada una, genera la tabla correspondiente, y entrega un archivo draw.io editable con formato de línea de tiempo vertical: eje central, fases alternadas en columnas izquierda/derecha con barra de título de color + bloque descriptivo gris, conectadas al eje mediante callouts circulares, usando la paleta y estilos del archivo time-line-vertical.drawio de referencia. No inventes información; lo inferido márcalo como hipótesis.`
