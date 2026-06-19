# Skill: $time-line (horizontal)

> Existen dos variantes de línea de tiempo: `$time-line` (horizontal, este archivo, basado en `time-line.drawio`) y `$time-line-vertical` (vertical, ver [time-line-vertical.md](time-line-vertical.md), basado en `time-line-vertical.drawio`). Si el usuario no especifica orientación, usa la horizontal por defecto; si pide "vertical", "en columna" o "de arriba hacia abajo", usa `$time-line-vertical`.

## Activador
Cuando el usuario escriba:

`$time-line`

debes generar una **línea de tiempo / roadmap de proyecto en formato horizontal** usando la información disponible en el chat actual (o la que el usuario provea explícitamente).

## Objetivo
Transformar una conversación, plan de proyecto, cronograma o roadmap en una **línea de tiempo horizontal** profesional, editable en draw.io / diagrams.net, con formato `.drawio`.

El resultado debe ayudar a identificar:

- **Fases o periodos** del proyecto (ej. meses, trimestres, sprints) representados como segmentos de color sobre una barra horizontal.
- **Actividades/entregables** de cada fase, listados como viñetas dentro de un bloque de texto asociado a su segmento.
- **Hitos (milestones)**: puntos de transición o eventos clave marcados con un círculo pequeño conectado visualmente a la fase correspondiente.
- El **orden cronológico** de izquierda a derecha.
- Vacíos de información que requieren validación.

## Formato de salida obligatorio
Entregar siempre:

1. **Resumen textual del cronograma**
2. **Tabla de fases/periodos**
3. **Tabla de hitos**
4. **Archivo o bloque XML compatible con draw.io**
5. **Instrucciones para importar en diagrams.net**

Cuando sea posible, generar el contenido como archivo `.drawio`.

## Estilo visual requerido
El diagrama debe seguir el formato de referencia compartido por el usuario (`time-line.drawio`):

- Archivo raíz en formato XML `<mxfile>`.
- Una página `<diagram>` con `mxGraphModel`.
- Una **barra horizontal segmentada**: cada fase es una celda `rounded=1` sin borde (`strokecolor=none`), con `fillColor`/`strokeColor` propios y `value` igual al nombre corto de la fase (ej. `"Nov"`, `"Jan"`, `"Mar"`).
- Todos los segmentos de fase se alinean en la **misma fila** (`y` constante, ej. `y=300`), uno a continuación del otro de izquierda a derecha, sin espacios entre ellos (el `x` de cada fase coincide con el `x + width` de la anterior).
- Cada fase tiene un **bloque descriptivo** (`rounded=1;strokeColor=none;fillColor=none;align=left;arcSize=12;verticalAlign=top;whiteSpace=wrap;html=1;`) que contiene en HTML enriquecido:
  - Título en negrita con el color de la fase (ej. `<b><font color="#647687">Feasibility</font></b>`).
  - Lista de actividades/entregables en fuente pequeña (`font-size: 10px`), separadas por `<br>`.
- Los bloques descriptivos se posicionan en **zigzag**: alternan arriba (`y≈220`, antes de la barra) y abajo (`y≈340`, después de la barra) de la fase a la que pertenecen, para evitar solapamiento visual y guiar la lectura en forma de onda.
- Cada fase tiene un **hito (milestone)**: un círculo pequeño (`ellipse;whiteSpace=wrap;html=1;aspect=fixed;shadow=0;rounded=1;fontStyle=1;`) del mismo color que la fase, ubicado en el mismo lado (arriba o abajo) que su bloque descriptivo, conectado a la barra de la fase con una **línea simple sin flechas** (`endArrow=none;endFill=0;`) que entra por la parte superior o inferior del segmento (`entryY=0` si el hito está arriba, `entryY=1` si está abajo).
- Paleta: cada fase usa un color distinto y consistente entre el segmento de barra, el hito y el título del bloque descriptivo (mismo `fillColor` para barra y círculo, `strokeColor` un tono más oscuro).
- Distribución estrictamente de **izquierda a derecha** según el orden cronológico de las fases.
- Sin sombras (`shadow=0`), bordes redondeados (`rounded=1`), tipografía limpia (`fontFamily` por defecto, `fontSize=12-14`).
- Compatible con diagrams.net / draw.io.

## Reglas de análisis
Antes de crear el diagrama:

1. Identifica el **horizonte temporal** del proyecto (fecha de inicio y fin, o duración total) y la unidad de fase (meses, trimestres, sprints, semanas).
2. Identifica las **fases o periodos** explícitos mencionados en el chat, en orden cronológico.
3. Para cada fase, determina sus **actividades o entregables principales** (máximo 3-4 ítems para no saturar el bloque).
4. Identifica los **hitos** (eventos puntuales de transición, entregas, aprobaciones, lanzamientos) y a qué fase pertenecen.
5. No inventes fases, actividades ni hitos como hechos confirmados.
6. Si agregas elementos inferidos, márcalos como **hipótesis**.
7. Si falta información (fechas exactas, duración de cada fase), agrega una sección de **preguntas abiertas**, pero no bloquees la generación; usa una duración proporcional razonable.

## Marcado de relevancia
Clasifica cada fase, actividad o hito como:

- **Núcleo**: fase o hito esencial del cronograma, sin el cual el proyecto no se completa.
- **Complementario**: actividad que enriquece la fase pero no es bloqueante (documentación, marketing, traducciones).
- **Hipótesis**: posible fase, actividad o hito no confirmado por el chat.

En el diagrama:

- No saturar con demasiadas fases: máximo recomendado 5-7 fases visibles en la línea de tiempo principal.
- Máximo 3-4 actividades por bloque descriptivo; si hay más, resumir y referenciar "ver detalle".
- Un color por fase, sin reutilizar colores entre fases adyacentes.

## Estructura de respuesta esperada

### 1. Alcance del cronograma
Describe en una frase el proyecto y el horizonte temporal cubierto.

### 2. Lectura ejecutiva
Resume en 3 a 6 líneas las fases principales y cómo se encadenan en el tiempo.

### 3. Tabla de fases/periodos

| # | Fase | Periodo (mes/trimestre) | Actividades/entregables | Relevancia | Evidencia del chat |
|---|---|---|---|---|---|

### 4. Tabla de hitos

| # | Hito | Fase asociada | Posición (arriba/abajo) | Relevancia |
|---|---|---|---|---|

### 5. Diagrama draw.io
Genera XML válido con esta estructura base:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram name="Línea de tiempo" id="timeline-001">
    <mxGraphModel dx="733" dy="1113" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" math="0" shadow="0">
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

- `mxCell` para segmentos de fase, bloques descriptivos y hitos (`vertex="1"`), y para las líneas conectoras hito → fase (`edge="1"`).
- Todas las celdas son `parent="1"` (sin agrupaciones jerárquicas, igual que en el archivo de referencia).
- `mxGeometry` con coordenadas explícitas (`x`, `y`, `width`, `height`) para segmentos, bloques y hitos.
- IDs únicos, simples y consistentes (ej. `phase-1`, `desc-1`, `milestone-1`, `conn-1`).
- Escapar caracteres especiales XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique

### Estilos de referencia (tomados de time-line.drawio)

Segmento de fase (barra):
```
fillColor=<color>;strokecolor=none;rounded=1;fontColor=#ffffff;strokeColor=<colorOscuro>;fontStyle=1;fontSize=14;
```
Geometría: `y=300` (constante para todas las fases), `height=30`, `width` proporcional a la duración de la fase, `x` continuo respecto a la fase anterior (`x` de la fase N = `x + width` de la fase N-1).

Bloque descriptivo (título + actividades):
```
rounded=1;strokeColor=none;fillColor=none;align=left;arcSize=12;verticalAlign=top;whiteSpace=wrap;html=1;fontSize=12;
```
`value` con HTML enriquecido:
```html
<font style="font-size: 12px" color="#647687"><b>Feasibility</b></font><br><br><font style="font-size: 10px">Requirements<br>Readiness</font>
```
Geometría: `width=140`, `height=70`. Si el bloque va **arriba** de la barra: `y≈220`. Si va **abajo**: `y≈340`. El `x` se alinea aproximadamente con el inicio del segmento de fase correspondiente.

Hito (milestone, círculo):
```
ellipse;whiteSpace=wrap;html=1;aspect=fixed;shadow=0;fillColor=<color>;strokeColor=<colorOscuro>;fontSize=14;align=center;strokeWidth=2;fontColor=#ffffff;rounded=1;fontStyle=1;
```
Geometría: `width=12`, `height=12`. Mismo lado (arriba `y≈220` / abajo `y≈410`) que el bloque descriptivo de su fase.

Conector hito → fase (línea simple sin flechas):
```
edgeStyle=none;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=none;endFill=0;fontSize=14;fillColor=<color>;strokeColor=<colorOscuro>;fontColor=#FFFFFF;fontStyle=1;
```
`source` = id del hito, `target` = id del segmento de fase. Usa `entryY=0` (con `entryX` cercano al borde izquierdo del segmento, ej. `0.07-0.12`) si el hito está arriba; `entryY=1` si el hito está abajo.

## Layout sugerido
Usa coordenadas base (replicando la disposición del archivo de referencia):

- Barra de fases en `y=300`, `height=30`, iniciando en `x≈90` y avanzando de forma continua hacia la derecha según la duración relativa de cada fase.
- Bloques descriptivos y hitos alternan posición:
  - Fase 1: bloque y hito **arriba** (`y≈220` / `y≈220`).
  - Fase 2: bloque y hito **abajo** (`y≈340` / `y≈410`).
  - Fase 3: bloque y hito **arriba**.
  - Fase 4: bloque y hito **abajo**.
  - Fase 5: bloque y hito **arriba**.
  - (continuar alternando para fases adicionales)
- Separación horizontal entre fases de ~10-30px o continua según el ancho proporcional a su duración.

## Paleta sugerida
Usa una paleta distinta y consistente por fase (segmento, hito y título coinciden):

- Gris azulado (fase inicial, ej. viabilidad/exploración): `fillColor=#647687;strokeColor=#314354`
- Verde (fase de planificación): `fillColor=#6d8764;strokeColor=#3A5431`
- Marrón/terracota (fase de desarrollo): `fillColor=#A0522D;strokeColor=#6D1F00`
- Morado (fase de preparación de lanzamiento): `fillColor=#76608A;strokeColor=#432D57`
- Rojo (fase de lanzamiento/soporte): `fillColor=#E51400;strokeColor=#B20000`

Si hay más de 5 fases, agrega colores adicionales evitando tonos repetidos o muy similares entre fases adyacentes.

## Ejemplo de invocación
Usuario:

`$time-line genera el cronograma del proyecto de migración del core bancario, de enero a octubre`

Respuesta esperada:

- Identificar fases (ej. `Análisis`, `Diseño`, `Construcción`, `Pruebas`, `Despliegue`) en orden cronológico.
- Listar actividades/entregables principales de cada fase.
- Identificar hitos clave (ej. `Aprobación de arquitectura`, `Go-live`) y asociarlos a su fase.
- Entregar XML `.drawio` con la barra segmentada, bloques alternados en zigzag y conectores de hito.

## Prompt interno recomendado
Cuando se active `$time-line`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica el horizonte temporal del proyecto, sus fases o periodos en orden cronológico, las actividades/entregables principales de cada fase y los hitos clave asociados. Usa únicamente información explícita del chat; si agregas inferencias, márcalas como hipótesis. Genera una tabla de fases/periodos y una tabla de hitos. Luego genera un archivo XML `.drawio` compatible con diagrams.net, con estructura `<mxfile>`, una página `<diagram>`, `mxGraphModel`, una barra horizontal continua de segmentos de fase (`fillColor` distinto por fase, alineados en la misma `y`), bloques descriptivos con título en negrita y actividades en viñetas que alternan posición arriba/abajo en zigzag respecto a su fase, e hitos como pequeños círculos del mismo color que su fase conectados a la barra con una línea simple sin flechas. El XML debe ser válido, editable e importable en draw.io.

## Validaciones antes de entregar
Antes de responder, verifica:

- El horizonte temporal está claro y las fases están en orden cronológico.
- Cada fase tiene al menos una actividad/entregable asociado.
- Las fases, actividades e hitos no están inventados como hechos; lo inferido está marcado como hipótesis.
- Los bloques descriptivos y sus hitos alternan correctamente arriba/abajo (zigzag).
- Cada fase tiene un color único y consistente entre barra, hito y título del bloque.
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>`, `<root>`.
- Todos los `mxCell` tienen IDs únicos.
- El archivo puede guardarse con extensión `.drawio`.
- El usuario puede importar el contenido en diagrams.net.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `time-line.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File → Open From → Device**.
5. Abre el archivo `.drawio`.
6. Edita textos, colores o posiciones si hace falta.

## Variante corta para llamar desde cualquier chat
`$time-line: toma el contexto actual, identifica el horizonte temporal del proyecto, sus fases o periodos en orden cronológico, las actividades/entregables principales de cada fase y los hitos clave asociados, genera las tablas correspondientes, y entrega un archivo draw.io editable con formato de línea de tiempo horizontal segmentada por color, con bloques descriptivos en zigzag y marcadores de hito conectados a su fase, usando la paleta y estilos del archivo time-line.drawio de referencia. No inventes información; lo inferido márcalo como hipótesis.`
