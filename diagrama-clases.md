# Skill: $diagrama-clases

## Activador
Cuando el usuario escriba:

`$diagrama-clases`

debes generar un diagrama UML de **clases** usando la información disponible en el chat actual (o la que el usuario provea explícitamente).

## Objetivo
Transformar una conversación, requerimiento, modelo de dominio o descripción de entidades en un diagrama de clases UML profesional, editable en draw.io / diagrams.net, con formato `.drawio`.

El resultado debe ayudar a identificar:

- Clases del dominio, con sus atributos y métodos.
- Visibilidad de cada miembro (`+` público, `-` privado, `#` protegido, `/` derivado).
- Relaciones de **herencia**, **asociación**, **agregación**, **composición** y **dependencia**.
- Multiplicidades en las asociaciones (ej. `0..1`, `1`, `0...*`, `1...5`).
- Agrupaciones lógicas por color según familia/jerarquía de clases.
- Vacíos de información que requieren validación.

## Formato de salida obligatorio
Entregar siempre:

1. **Resumen textual del modelo de dominio**
2. **Tabla de clases, atributos, métodos y relaciones**
3. **Archivo o bloque XML compatible con draw.io**
4. **Instrucciones para importar en diagrams.net**

Cuando sea posible, generar el contenido como archivo `.drawio`.

## Estilo visual requerido
El diagrama debe seguir el formato de referencia compartido por el usuario (`diagrama-clases.drawio`):

- Archivo raíz en formato XML `<mxfile>`.
- Una página `<diagram>` con `mxGraphModel`.
- Cada clase representada como un `swimlane` (caja con título) usando `childLayout=stackLayout;horizontal=1;startSize=26;horizontalStack=0;resizeParent=1;resizeLast=0`.
- El nombre de la clase va en el `value` del swimlane; `fontStyle=2` para clases concretas destacadas o clases base, `fontStyle=0` para el resto.
- Atributos y métodos como celdas hijas (`text;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden`) apiladas dentro del swimlane.
- Una línea separadora (`style=line;html=1;strokeWidth=1`) entre el bloque de atributos y el bloque de métodos.
- Visibilidad de cada miembro indicada con el prefijo textual: `+` público, `-` privado, `#` protegido, `/` atributo derivado/calculado.
- Métodos abstractos en *italic* (`fontStyle=4`); miembros estáticos subrayados (`fontStyle=8` o combinado, ej. `fontStyle=12` para estático+abstracto) si aplica.
- Relación de **herencia** con flecha hueca triangular: `endArrow=block;endFill=0;edgeStyle=elbowEdgeStyle;elbow=vertical`, desde la clase hija (`source`) hacia la clase padre (`target`).
- Relación de **asociación** con flecha abierta simple: `endArrow=open;endFill=1` (o `endFill=0` si no se desea relleno), con etiquetas de multiplicidad (`0..1`, `1`, etc.) en los extremos y, opcionalmente, una etiqueta de rol en el medio (ej. `lives at`).
- Relación de **dependencia/asociación entre miembros** (ej. "supervises") puede dibujarse como `edgeStyle=orthogonalEdgeStyle;endArrow=open;endFill=0` conectando celdas de atributos específicas, con etiquetas de multiplicidad en cada extremo.
- Cada clase y su jerarquía comparte una misma paleta de color (fillColor/strokeColor) para diferenciarla visualmente del resto.
- Título y subtítulo del diagrama como cajas de texto (`text;html=1`) en la esquina superior izquierda, si se requiere contexto adicional.
- Distribución equilibrada: clases base arriba o al centro, subclases debajo, clases asociadas a los costados.
- Líneas limpias, sin cruces innecesarios, texto legible.
- Compatible con diagrams.net / draw.io.

## Reglas de análisis
Antes de crear el diagrama:

1. Identifica el **dominio o módulo** que se está modelando.
2. Identifica las **clases** explícitas (entidades, conceptos del negocio) mencionadas en el chat.
3. Extrae los **atributos** (nombre y tipo) y **métodos** (nombre, parámetros, tipo de retorno) de cada clase.
4. Determina la **visibilidad** de cada miembro; si no se especifica, infiere `+` (público) y márcalo como hipótesis.
5. No inventes clases, atributos ni métodos como hechos confirmados.
6. Si agregas elementos inferidos, márcalos como **hipótesis**.
7. Identifica relaciones de:
   - **Herencia** (`es un`, generalización/especialización).
   - **Asociación** (una clase usa/conoce a otra, con multiplicidad).
   - **Agregación** (relación "tiene un" débil, el todo no posee el ciclo de vida de la parte).
   - **Composición** (relación "tiene un" fuerte, el todo posee el ciclo de vida de la parte).
   - **Dependencia** (una clase depende de otra para funcionar, sin ser atributo).
8. Si falta información, agrega una sección de **preguntas abiertas**, pero no bloquees la generación.
9. Usa convención UML para nombrar miembros: atributos como `nombre: tipo`, métodos como `nombre(parámetros): tipoRetorno`.

## Marcado de relevancia
Clasifica cada clase o relación como:

- **Núcleo**: entidad esencial del dominio, sin la cual el modelo no existe.
- **Complementario**: enriquece el modelo pero no es bloqueante.
- **Hipótesis**: posible clase, atributo, método o relación no confirmada por el chat.

En el diagrama:

- No saturar con demasiados colores: una paleta por clase/jerarquía.
- Máximo recomendado: 6-8 miembros visibles por clase en el diagrama principal.
- Si hay más, agrupar conceptualmente o dejar en tabla y referenciar como "ver detalle".

## Estructura de respuesta esperada

### 1. Alcance del modelo
Describe en una frase el dominio/módulo y su propósito principal.

### 2. Lectura ejecutiva
Resume en 3 a 6 líneas qué clases componen el modelo y cómo se relacionan.

### 3. Tabla de clases y miembros
Usa esta tabla:

| Clase | Miembro | Tipo (atributo/método) | Visibilidad | Relevancia | Evidencia del chat |
|---|---|---|---|---|---|

### 4. Tabla de relaciones
Usa esta tabla:

| Origen | Destino | Tipo de relación | Multiplicidad | Etiqueta/rol | Relevancia |
|---|---|---|---|---|---|

Tipo de relación puede ser: Herencia, Asociación, Agregación, Composición, Dependencia.

### 5. Diagrama draw.io
Genera XML válido con esta estructura base:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram name="Diagrama de Clases" id="clases-001">
    <mxGraphModel dx="1059" dy="779" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="850" pageHeight="1100" math="0" shadow="0">
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

- `mxCell` para nodos (clases, miembros, líneas separadoras, textos) y conectores (relaciones).
- `vertex="1"` para swimlanes de clase, celdas de miembro, líneas separadoras y textos.
- `edge="1"` para herencia, asociación, agregación, composición y dependencia.
- Cada swimlane de clase es `parent="1"`; sus miembros (atributos, métodos, separador) son `parent="<id-de-la-clase>"`.
- `mxGeometry` con coordenadas explícitas (`x`, `y`, `width`, `height`) para las clases, y `y`/`width`/`height` relativos (sin `x`) para los miembros apilados dentro del swimlane.
- IDs únicos, simples y consistentes (ej. `class-person`, `attr-name`, `edge-herencia-1`).
- Escapar caracteres especiales XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique

### Estilos de referencia (tomados de diagrama-clases.drawio)

Swimlane de clase:
```
swimlane;fontStyle=2;align=center;verticalAlign=top;childLayout=stackLayout;horizontal=1;startSize=26;horizontalStack=0;resizeParent=1;resizeLast=0;collapsible=1;marginBottom=0;rounded=0;shadow=0;strokeWidth=1;fillColor=#f8cecc;strokeColor=#b85450;
```
Geometría sugerida: `width=160`, `height` según cantidad de miembros (`26` por la barra de título + `26` por cada miembro + `8` por el separador).

Atributo/método (celda de texto):
```
text;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;
```
Geometría: `y` acumulativo (múltiplos de `26` desde el inicio del swimlane), `width=160`, `height=26`.
Para métodos abstractos agrega `fontStyle=4` (italic). Para atributos/métodos estáticos agrega subrayado vía `fontStyle` combinado.

Separador entre atributos y métodos:
```
line;html=1;strokeWidth=1;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=3;rotatable=0;labelPosition=right;points=[];portConstraint=eastwest;
```
Geometría: `width=160`, `height=8`.

Relación de herencia (flecha hueca, hija → padre):
```
endArrow=block;endSize=10;endFill=0;shadow=0;strokeWidth=1;rounded=0;edgeStyle=elbowEdgeStyle;elbow=vertical;
```

Relación de asociación (flecha abierta simple, con multiplicidades y rol):
```
endArrow=open;shadow=0;strokeWidth=1;rounded=0;endFill=1;edgeStyle=elbowEdgeStyle;elbow=vertical;
```
Multiplicidades como celdas hijas del edge (`resizable=0;align=left|right;verticalAlign=bottom;labelBackgroundColor=none;fontSize=12;`), y rol como celda de texto centrada sobre la línea.

Relación entre miembros específicos (ej. "supervises"):
```
edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endArrow=open;endFill=0;
```
con etiquetas de multiplicidad (`edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;`) en cada extremo.

Título y subtítulo (cajas de texto):
```
text;html=1;whiteSpace=wrap;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;rounded=0;
```

## Layout sugerido
Usa coordenadas base (replicando la disposición del archivo de referencia):

- Clase base/central (ej. `Person`): `x=200, y=20, width=160`.
- Subclases debajo de la clase base, separadas horizontalmente (ej. `x=60, y=280` y `x=360, y=280`), conectadas por herencia hacia arriba.
- Clase asociada a la derecha de la clase base (ej. `Address`): `x=488, y=20, width=160`.
- Separación vertical entre clases con relación de herencia: al menos `260px` para dar espacio a la flecha en codo (`elbowEdgeStyle`).
- Título del diagrama: `x=40, y=110, width=290, height=30` (si se incluye).

Cada subclase se conecta con flecha hueca hacia su clase padre. Las asociaciones llevan multiplicidad en ambos extremos y, opcionalmente, una etiqueta de rol centrada.

## Paleta sugerida
Usa una paleta distinta por clase/jerarquía funcional:

- Rojo suave (clase base 1): `fillColor=#f8cecc;strokeColor=#b85450`
- Naranja (subclase 1): `fillColor=#ffe6cc;strokeColor=#d79b00`
- Amarillo (subclase 2): `fillColor=#fff2cc;strokeColor=#d6b656`
- Azul (clase asociada): `fillColor=#dae8fc;strokeColor=#6c8ebf`
- Verde (clase de soporte/valor): `fillColor=#d5e8d4;strokeColor=#82b366`
- Morado (clase utilitaria/servicio): `fillColor=#e1d5e7;strokeColor=#9673a6`
- Gris (clase externa/sistema): `fillColor=#f5f5f5;strokeColor=#666666`

## Ejemplo de invocación
Usuario:

`$diagrama-clases genera el diagrama de clases del módulo de cuentas y transferencias de la banca móvil`

Respuesta esperada:

- Identificar clases (ej. `Cuenta`, `Cliente`, `Transferencia`, `Comprobante`).
- Listar atributos y métodos por clase con visibilidad.
- Marcar relaciones de herencia, asociación, agregación, composición o dependencia con multiplicidad.
- Entregar XML `.drawio`.

## Prompt interno recomendado
Cuando se active `$diagrama-clases`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica las clases del dominio o módulo descrito, junto con sus atributos y métodos, indicando visibilidad (`+`, `-`, `#`, `/`). Usa únicamente información explícita del chat; si agregas inferencias, márcalas como hipótesis. Genera una tabla de clases/miembros y una tabla de relaciones (herencia, asociación, agregación, composición, dependencia) con multiplicidad y evidencia. Luego genera un archivo XML `.drawio` compatible con diagrams.net, con estructura `<mxfile>`, una página `<diagram>`, `mxGraphModel`, clases como `swimlane` con `childLayout=stackLayout`, miembros apilados como celdas de texto con su visibilidad, línea separadora entre atributos y métodos, herencia con flecha hueca (`endArrow=block;endFill=0`), asociaciones con flecha abierta y multiplicidades, agrupadas por color según jerarquía, y título/subtítulo en la esquina superior izquierda si aplica. El XML debe ser válido, editable e importable en draw.io.

## Validaciones antes de entregar
Antes de responder, verifica:

- El alcance del modelo está claro.
- Cada clase tiene al menos un atributo o método.
- Los miembros no están inventados como hechos; lo inferido está marcado como hipótesis.
- Las relaciones de herencia están dirigidas correctamente (hija → padre).
- Las asociaciones tienen multiplicidad en ambos extremos cuando aplica.
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>`, `<root>`.
- Todos los `mxCell` tienen IDs únicos y `parent` correcto (miembros dentro de su swimlane).
- El archivo puede guardarse con extensión `.drawio`.
- El usuario puede importar el contenido en diagrams.net.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `diagrama-clases.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File → Open From → Device**.
5. Abre el archivo `.drawio`.
6. Edita textos, colores o posiciones si hace falta.

## Variante corta para llamar desde cualquier chat
`$diagrama-clases: toma el contexto actual, identifica clases, atributos, métodos (con visibilidad) y relaciones (herencia, asociación, agregación, composición, dependencia) con multiplicidad, genera tabla de clases/miembros y tabla de relaciones, y entrega un archivo draw.io editable con formato de diagrama de clases UML profesional, usando la paleta y estilos del archivo diagrama-clases.drawio de referencia. No inventes información; lo inferido márcalo como hipótesis.`
