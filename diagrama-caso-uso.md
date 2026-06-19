# Skill: $diagrama-caso-uso

## Activador
Cuando el usuario escriba:

`$diagrama-caso-uso`

debes generar un diagrama UML de **casos de uso** usando la información disponible en el chat actual (o la que el usuario provea explícitamente).

## Objetivo
Transformar una conversación, requerimiento, historia de usuario, proceso de negocio o flujo funcional en un diagrama de casos de uso profesional, editable en draw.io / diagrams.net, con formato `.drawio`.

El resultado debe ayudar a identificar:

- Actores (primarios y secundarios) que interactúan con el sistema.
- Casos de uso principales por actor.
- Relaciones `include` (uso obligatorio de otro caso de uso) y `extend` (extensión opcional).
- Agrupaciones lógicas por actor/módulo mediante color.
- Vacíos de información que requieren validación.

## Formato de salida obligatorio
Entregar siempre:

1. **Resumen textual del alcance funcional**
2. **Tabla de actores y casos de uso**
3. **Archivo o bloque XML compatible con draw.io**
4. **Instrucciones para importar en diagrams.net**

Cuando sea posible, generar el contenido como archivo `.drawio`.

## Estilo visual requerido
El diagrama debe seguir el formato de referencia compartido por el usuario (`caso-uso.drawio`):

- Archivo raíz en formato XML `<mxfile>`.
- Una página `<diagram>` con `mxGraphModel`.
- Actores representados con `shape=umlActor` (figura de palote), `verticalLabelPosition=bottom`, `verticalAlign=top`.
- Casos de uso representados como `ellipse` con `whiteSpace=wrap`.
- Cada actor y su grupo de casos de uso comparte una misma paleta de color (fillColor/strokeColor) para diferenciarlos visualmente del resto.
- Líneas de asociación actor → caso de uso con `edgeStyle=entityRelationEdgeStyle`, sin flecha (líneas simples).
- Relaciones `<<include>>` / `<<extend>>` entre casos de uso con `endArrow=open;dashed=1` y etiqueta de texto (`Use`, `Include`, `Extend`, etc.).
- Título y subtítulo del diagrama como cajas de texto (`text;html=1`) en la esquina superior izquierda.
- Distribución horizontal: actores a los costados (izquierda/derecha), casos de uso en columnas centrales.
- Líneas limpias, sin cruces innecesarios, texto legible.
- Compatible con diagrams.net / draw.io.

## Reglas de análisis
Antes de crear el diagrama:

1. Identifica el **sistema o módulo** que se está modelando.
2. Identifica los **actores** explícitos (personas, roles, sistemas externos) mencionados en el chat.
3. Extrae los **casos de uso** explícitos (acciones que el actor realiza sobre el sistema).
4. No inventes actores ni casos de uso como hechos confirmados.
5. Si agregas casos de uso inferidos, márcalos como **hipótesis**.
6. Identifica relaciones de **inclusión** (`<<include>>`, un caso de uso siempre dispara a otro) y **extensión** (`<<extend>>`, un caso de uso opcionalmente extiende a otro).
7. Si falta información, agrega una sección de **preguntas abiertas**, pero no bloquees la generación.
8. Usa lenguaje ejecutivo, claro y breve. Los casos de uso se nombran como verbo + objeto (ej. "Consultar saldo", "Registrar pago").

## Marcado de relevancia
Clasifica cada caso de uso como:

- **Núcleo**: funcionalidad esencial del sistema, sin la cual el proceso no existe.
- **Complementario**: mejora la experiencia pero no es bloqueante.
- **Hipótesis**: posible caso de uso no confirmado por el chat.

En el diagrama:

- No saturar con demasiados colores: una paleta por actor/agrupación.
- Máximo recomendado: 6 casos de uso por actor en el diagrama principal.
- Si hay más, agrupar o dejar en tabla y referenciar como "ver detalle".

## Estructura de respuesta esperada

### 1. Alcance funcional
Describe en una frase el sistema/módulo y su propósito principal.

### 2. Lectura ejecutiva
Resume en 3 a 6 líneas qué actores interactúan con el sistema y qué logran.

### 3. Tabla de actores y casos de uso
Usa esta tabla:

| Actor | Caso de uso | Tipo | Relevancia | Relación (include/extend) | Evidencia del chat |
|---|---|---|---|---|---|

Tipo puede ser:

- Explícito
- Inferido
- Hipótesis
- Pendiente de validar

### 4. Diagrama draw.io
Genera XML válido con esta estructura base:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram name="Caso de Uso" id="caso-uso-001">
    <mxGraphModel dx="1426" dy="841" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" math="0" shadow="0">
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

- `mxCell` para nodos y conectores.
- `vertex="1"` para actores, casos de uso y textos.
- `edge="1"` para líneas de asociación, include y extend.
- `mxGeometry` con coordenadas explícitas (`x`, `y`, `width`, `height`).
- IDs únicos, simples y consistentes (ej. `actor-1`, `uc-1`, `edge-1`).
- Escapar caracteres especiales XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique

### Estilos de referencia (tomados de caso-uso.drawio)

Actor:
```
shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;fillColor=#d5e8d4;strokeColor=#82b366;
```
Geometría sugerida: `height=60` `width=30`.

Caso de uso (elipse):
```
ellipse;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;
```
Geometría sugerida: `height=70` `width=140`.

Asociación actor → caso de uso (línea simple, sin flecha):
```
edgeStyle=entityRelationEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;
```

Relación include/extend (línea punteada con etiqueta):
```
endArrow=open;endSize=12;dashed=1;html=1;rounded=0;edgeStyle=entityRelationEdgeStyle;
```
con `value="<<include>>"` o `value="<<extend>>"` según corresponda.

Título y subtítulo (cajas de texto):
```
text;html=1;whiteSpace=wrap;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;rounded=0;
```

## Layout sugerido
Usa coordenadas base (replicando la disposición del archivo de referencia):

- Actor primario (izquierda): `x=90, y=370, width=30, height=60`.
- Columna de casos de uso del actor primario: `x=230`, separados verticalmente cada ~140-150px (`y=260`, `y=400`, `y=550`).
- Actor secundario (derecha): `x=970, y=340, width=30, height=60`.
- Columna de casos de uso del actor secundario: `x=690`, mismos offsets verticales.
- Título del diagrama: `x=40, y=110, width=290, height=30`.
- Subtítulo: `x=40, y=140, width=60, height=30`.

Cada actor se conecta con línea simple a cada uno de sus casos de uso. Las relaciones include/extend se trazan entre casos de uso (no entre actores).

## Paleta sugerida
Usa una paleta distinta por actor/agrupación funcional:

- Verde (actor/módulo 1): `fillColor=#d5e8d4;strokeColor=#82b366`
- Azul (actor/módulo 2): `fillColor=#dae8fc;strokeColor=#6c8ebf`
- Amarillo (actor/módulo 3): `fillColor=#fff2cc;strokeColor=#d6b656`
- Rojo suave (actor/módulo 4): `fillColor=#f8cecc;strokeColor=#b85450`
- Morado (actor/módulo 5): `fillColor=#e1d5e7;strokeColor=#9673a6`
- Gris (actor externo/sistema): `fillColor=#f5f5f5;strokeColor=#666666`

## Ejemplo de invocación
Usuario:

`$diagrama-caso-uso genera el diagrama de casos de uso del módulo de transferencias de la banca móvil`

Respuesta esperada:

- Identificar actores (ej. Cliente, Sistema de validación antifraude).
- Listar casos de uso por actor.
- Marcar relaciones include/extend.
- Entregar XML `.drawio`.

## Prompt interno recomendado
Cuando se active `$diagrama-caso-uso`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica los actores y los casos de uso del sistema o módulo descrito. Usa únicamente información explícita del chat; si agregas inferencias, márcalas como hipótesis. Genera una tabla de actores y casos de uso con tipo, relevancia, relación include/extend y evidencia. Luego genera un archivo XML `.drawio` compatible con diagrams.net, con estructura `<mxfile>`, una página `<diagram>`, `mxGraphModel`, actores como `shape=umlActor`, casos de uso como elipses, asociaciones simples actor-caso de uso, relaciones `<<include>>`/`<<extend>>` punteadas entre casos de uso, agrupados por color según actor, y título/subtítulo en la esquina superior izquierda. El XML debe ser válido, editable e importable en draw.io.

## Validaciones antes de entregar
Antes de responder, verifica:

- El alcance funcional está claro.
- Cada actor tiene al menos un caso de uso asociado.
- Los casos de uso no están inventados como hechos; lo inferido está marcado como hipótesis.
- Las relaciones include/extend están correctamente etiquetadas y dirigidas (include: caso base → caso incluido; extend: caso extensor → caso extendido).
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>`, `<root>`.
- Todos los `mxCell` tienen IDs únicos.
- El archivo puede guardarse con extensión `.drawio`.
- El usuario puede importar el contenido en diagrams.net.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `diagrama-caso-uso.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File → Open From → Device**.
5. Abre el archivo `.drawio`.
6. Edita textos, colores o posiciones si hace falta.

## Variante corta para llamar desde cualquier chat
`$diagrama-caso-uso: toma el contexto actual, identifica actores y casos de uso, marca relaciones include/extend, genera tabla de actores/casos de uso y entrega un archivo draw.io editable con formato de diagrama de casos de uso UML profesional, usando la paleta y estilos del archivo caso-uso.drawio de referencia. No inventes información; lo inferido márcalo como hipótesis.`
