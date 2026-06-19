# Skill: $diagrama-maquina-estados

## Activador
Cuando el usuario escriba:

`$diagrama-maquina-estados`

debes generar un **diagrama de máquina de estados (UML State Machine)** usando la información disponible en el chat actual (o la que el usuario provea explícitamente).

## Objetivo
Transformar una conversación, requerimiento, especificación de comportamiento o ciclo de vida de un objeto/sistema en un diagrama de **máquina de estados UML 2.x** profesional, editable en draw.io / diagrams.net, con formato `.drawio`.

El resultado debe ayudar a identificar:

- **Estado inicial** (pseudo-estado, círculo negro relleno) y **estado(s) final(es)** (`shape=endState`).
- **Estados simples** (`shape=umlState`, rectángulo redondeado con esquina superior tipo "collapse state"), incluyendo si tienen *entry/do/exit activities* en el `label` (ej. `do / actividad`).
- **Estados compuestos/anidados** (un estado contenedor que agrupa sub-estados, modelado como `group` + `umlState` con `container=1`).
- **Transiciones** rotuladas con la sintaxis UML `evento [guarda] /acción`, donde:
  - `evento`: el disparador de la transición (puede omitirse si es automática/de finalización).
  - `[guarda]`: condición booleana entre corchetes que habilita la transición (opcional).
  - `/acción`: efecto o acción ejecutada al disparar la transición (opcional, precedida de `/`).
- **Auto-transiciones** (un estado que se transiciona a sí mismo).
- **Transiciones internas/externas hacia estados compuestos** (entrando o saliendo de un subestado dentro de un contenedor).
- **Rutas de error/excepción** diferenciadas visualmente (color rojo) de las rutas del camino feliz.
- Vacíos de información que requieren validación.

## Formato de salida obligatorio
Entregar siempre:

1. **Resumen textual de la máquina de estados**
2. **Tabla de estados**
3. **Tabla de transiciones en orden de flujo**
4. **Archivo o bloque XML compatible con draw.io**
5. **Instrucciones para importar en diagrams.net**

Cuando sea posible, generar el contenido como archivo `.drawio`.

## Estilo visual requerido
El diagrama debe seguir el formato de referencia compartido por el usuario (`diagrama-maquina-estados.drawio`):

- Archivo raíz en formato XML `<mxfile>`.
- Una página `<diagram>` con `mxGraphModel`.
- **Estado inicial** (pseudo-estado): círculo negro relleno, sin texto: `ellipse;fillColor=#000000;strokeColor=none;` — geometría pequeña (`width=30`, `height=30`).
- **Estado simple**: `UserObject` con `label` = nombre del estado (puede incluir `&lt;br&gt;` para multilínea o para mostrar `do / actividad`), cuya `mxCell` hija usa `shape=umlState;rounded=1;verticalAlign=top;spacingTop=5;umlStateSymbol=collapseState;absoluteArcSize=1;arcSize=10;` — rectángulo redondeado con barra superior tipo pestaña.
- **Estado simple sin barra superior** (variante usada para estados "de tránsito" cortos): `html=1;align=center;verticalAlign=top;rounded=1;absoluteArcSize=1;arcSize=10;` (sin `umlStateSymbol`).
- **Estado de error/excepción**: mismo `shape=umlState`, con `fillColor=none;strokeColor=#b85450;fontColor=#990000;` para diferenciarlo visualmente del camino feliz.
- **Estado compuesto/contenedor**: una celda `group` (`style=group;fillColor=none;strokeColor=none;`) que envuelve un `UserObject`/`mxCell` con `shape=umlState;...;container=1;` y, dentro de ese contenedor (`parent=<id-del-contenedor>`), sus sub-estados (`UserObject` con `shape=umlState`), su propio pseudo-estado inicial (`ellipse;fillColor=default;strokeColor=<color-del-contenedor>;`) y su propio estado final si aplica (`shape=endState`).
- **Estado final**: `ellipse;html=1;shape=endState;fillColor=#000000;strokeColor=#000000;` (círculo relleno con borde, símbolo de "ojo de toro" / bullseye) — geometría pequeña (`width≈30`, `height≈28`).
- **Transición** (camino feliz): `rounded=0;orthogonalLoop=1;jettySize=auto;html=1;endArrow=open;endFill=0;edgeStyle=orthogonalEdgeStyle;` — línea con flecha abierta (no rellena), enrutamiento ortogonal.
- **Transición de error/excepción**: mismo estilo de edge + `fillColor=#f8cecc;strokeColor=#b85450;`, con su etiqueta en `fontColor=#990000;`.
- **Transición hacia/desde un pseudo-estado inicial dentro de un contenedor**: misma línea de transición, sin etiqueta o con etiqueta corta (ej. `invalid key /ignore`).
- **Etiqueta de transición** (`evento [guarda] /acción`): celda hija del edge, `edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;points=[];` con el texto completo de la transición como `value`.
- **Auto-transición**: edge con `source` y `target` apuntando al mismo estado, `edgeStyle=none;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endArrow=open;endFill=0;`.
- **Transición punteada** (usada para indicar una ruta "fuera de banda" o de bajo nivel de detalle, ej. una transición que sale de un sub-estado interno directo a un estado externo): `dashed=1;` agregado al estilo del edge.
- Paleta: estados y transiciones del camino feliz sin color explícito (`default`/negro); estados y transiciones de error en rojo (`strokeColor=#b85450;fontColor=#990000;fillColor=#f8cecc` para edges, `strokeColor=#b85450;fontColor=#990000` para estados).
- Compatible con diagrams.net / draw.io.

## Reglas de análisis
Antes de crear el diagrama:

1. Identifica el **objeto, entidad o sistema** cuyo ciclo de vida se está modelando.
2. Identifica todos los **estados** explícitos mencionados en el chat (incluyendo estados intermedios, de espera, de error, de carga, etc.).
3. Determina si algún estado es en realidad un **estado compuesto** que agrupa sub-estados (ej. un estado "Monitoreando" que internamente puede estar "Verificando acceso" o "Actualizando registros").
4. Identifica el **estado inicial** (disparado por la creación/arranque del objeto/sistema) y el o los **estado(s) final(es)** (si el ciclo de vida termina explícitamente).
5. Para cada transición, identifica:
   - El **evento** que la dispara.
   - La **guarda** `[condición]` que la habilita, si existe.
   - La **acción** `/efecto` que se ejecuta, si existe.
6. Identifica **rutas de error/excepción** (ej. pérdida de energía, servidor no responde, conexión fallida) y diferéncialas como ruta de error.
7. Identifica **auto-transiciones** (eventos que no cambian de estado pero ejecutan una acción).
8. No inventes estados, eventos, guardas ni acciones como hechos confirmados.
9. Si agregas elementos inferidos, márcalos como **hipótesis**.
10. Si falta información (ej. no se sabe qué dispara la salida de un estado), agrega una sección de **preguntas abiertas**, pero no bloquees la generación.

## Marcado de relevancia
Clasifica cada estado o transición como:

- **Núcleo**: estado o transición esencial del ciclo de vida, sin el cual el comportamiento no tiene sentido (ej. camino feliz).
- **Complementario**: enriquece el modelo (estados intermedios de carga, notificaciones) pero no es bloqueante para el camino feliz.
- **Excepción**: ruta de error, timeout o fallo (ej. pérdida de energía, servidor no responde).
- **Hipótesis**: posible estado, transición, guarda o acción no confirmado por el chat.

En el diagrama:

- No saturar con demasiados estados visibles a la vez; si hay más de 8-10 estados en el camino feliz, agrupar en un estado compuesto y detallar el contenido en una tabla o en un diagrama anidado.
- Reservar el color rojo (`#b85450` / `#990000` / `#f8cecc`) exclusivamente para rutas de error/excepción, para que resalten frente al camino feliz.

## Estructura de respuesta esperada

### 1. Alcance de la máquina de estados
Describe en una frase el objeto/sistema modelado y su propósito principal.

### 2. Lectura ejecutiva
Resume en 3 a 6 líneas cuáles son los estados principales y cómo fluye el ciclo de vida en el camino feliz.

### 3. Tabla de estados

| Estado | Tipo (inicial/simple/compuesto/final) | Estado padre (si es sub-estado) | Actividad asociada (entry/do/exit) | Relevancia |
|---|---|---|---|---|

### 4. Tabla de transiciones

| # | Origen | Destino | Evento | Guarda `[condición]` | Acción `/efecto` | Relevancia |
|---|---|---|---|---|---|---|

### 5. Diagrama draw.io
Genera XML válido con esta estructura base:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram name="Diagrama de Máquina de Estados" id="maquina-estados-001">
    <mxGraphModel dx="1064" dy="779" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" math="0" shadow="0">
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

- `UserObject` (con atributo `label`) envolviendo una `mxCell` hija (`vertex="1"`) para representar **estados** (simples y compuestos), siguiendo el patrón del archivo de referencia.
- `mxCell` simple (`vertex="1"`) para el **pseudo-estado inicial** (círculo negro), el **estado final** (`shape=endState`) y para estados de tránsito sin barra superior.
- `mxCell` (`edge="1"`) para las **transiciones**, con `source` y `target` apuntando a los IDs de los estados/pseudo-estados que conecta.
- Cada **etiqueta de transición** es una celda hija del edge: `vertex="1" connectable="0" parent="<id-del-edge>"`, con `style=edgeLabel;...` y `value` = texto completo `evento [guarda] /acción`.
- El **estado inicial** (pseudo-estado) y el **estado final** son `parent="1"` si están en el nivel raíz, o `parent="<id-del-contenedor>"` si pertenecen a un estado compuesto.
- Para un **estado compuesto**, usa una celda `group` (`vertex="1" connectable="0"`) que envuelve al `UserObject` del contenedor; los sub-estados, su pseudo-estado inicial y su estado final tienen `parent="<id-del-UserObject-contenedor>"` (no del `group`), y sus transiciones internas también usan ese mismo `parent`.
- Las transiciones que **entran o salen** de un estado compuesto desde/hacia el nivel raíz usan `parent="1"` y apuntan con `source`/`target` directamente al ID del contenedor (no a un sub-estado).
- `mxGeometry` con coordenadas explícitas (`x`, `y`, `width`, `height`) para estados, pseudo-estados y estados finales; geometría relativa (`relative="1"`) con `Array as="points"` para las rutas de las transiciones cuando deban evitar cruces; geometría relativa con `offset` para las etiquetas (celdas hijas de un edge).
- IDs únicos, simples y consistentes (ej. `estado-inicial`, `estado-1`, `estado-final`, `trans-1`, `compuesto-1`).
- Escapar caracteres especiales XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique

### Estilos de referencia (tomados de diagrama-maquina-estados.drawio)

Pseudo-estado inicial:
```
ellipse;fillColor=#000000;strokeColor=none;
```
Geometría: `width=30`, `height=30`.

Estado simple (con barra superior tipo "collapse state"):
```
shape=umlState;rounded=1;verticalAlign=top;spacingTop=5;umlStateSymbol=collapseState;absoluteArcSize=1;arcSize=10;
```
Geometría sugerida: `width=140`, `height=60`. El `label` del `UserObject` lleva el nombre del estado (puede incluir `&lt;br&gt;` para mostrar `do / actividad` en una segunda línea).

Estado simple (de tránsito, sin barra superior):
```
html=1;align=center;verticalAlign=top;rounded=1;absoluteArcSize=1;arcSize=10;
```
Geometría sugerida: `width=140`, `height=40`.

Estado de error/excepción:
```
html=1;align=center;verticalAlign=top;rounded=1;absoluteArcSize=1;arcSize=10;dashed=0;fillColor=none;strokeColor=#b85450;fontColor=#990000;
```
Geometría sugerida: `width=140`, `height=40`.

Estado compuesto (contenedor):
```
shape=umlState;rounded=1;verticalAlign=top;spacingTop=5;umlStateSymbol=collapseState;absoluteArcSize=1;arcSize=10;container=1;fillColor=none;strokeColor=<color>;fontColor=<color>;
```
Envuelto en una celda `group` (`style=group;fillColor=none;strokeColor=none;`). Geometría del contenedor: suficiente para alojar sus sub-estados apilados (ej. `width≈260`, `height≈260`).

Estado final:
```
ellipse;html=1;shape=endState;fillColor=#000000;strokeColor=#000000;
```
Geometría: `width≈30`, `height≈28`.

Transición (camino feliz):
```
rounded=0;orthogonalLoop=1;jettySize=auto;html=1;endArrow=open;endFill=0;edgeStyle=orthogonalEdgeStyle;
```
Agrega `strokeWidth=1;` y, opcionalmente, `fontSize=17;fontColor=#666666;` si la etiqueta debe resaltar en gris.

Transición de error/excepción:
```
rounded=0;orthogonalLoop=1;jettySize=auto;html=1;endArrow=open;endFill=0;edgeStyle=orthogonalEdgeStyle;fillColor=#f8cecc;strokeColor=#b85450;
```
La etiqueta hija usa `fontColor=#990000;`.

Auto-transición:
```
edgeStyle=none;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endArrow=open;endFill=0;
```
`source` y `target` apuntan al mismo ID de estado.

Transición punteada (ruta de bajo detalle / fuera de banda):
```
edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;endArrow=none;endFill=0;dashed=1;fontColor=#990000;fillColor=#f8cecc;strokeColor=#b85450;
```

Etiqueta de transición:
```
edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;points=[];
```
`value` con el texto completo `evento [guarda] /acción` (ej. `"access permitted [valid-key] /unlock"`, `"5 seconds unlocked [server unresponsive] /lock"`).

## Layout sugerido
Usa coordenadas base (replicando la disposición del archivo de referencia):

- Pseudo-estado inicial en la esquina superior izquierda del diagrama (ej. `x≈60, y≈215`), con su transición hacia el primer estado real.
- Estados del camino feliz distribuidos de izquierda a derecha y de arriba hacia abajo según el orden temporal del ciclo de vida.
- Estados compuestos a la derecha o debajo del flujo principal, con su propio pseudo-estado inicial y estado final internos.
- Estados/transiciones de error desplazados hacia un costado (ej. a la derecha del flujo principal) y conectados mediante líneas rojas, para no interrumpir visualmente el camino feliz.
- Auto-transiciones dibujadas como un pequeño lazo sobre el borde derecho o superior del propio estado.
- Etiquetas de transición ubicadas cerca del punto medio del recorrido del edge, con `offset` ajustado para no superponerse con otras etiquetas o líneas.

## Paleta sugerida

- Negro (`#000000`): pseudo-estado inicial, estado final, camino feliz por defecto.
- Gris (`fontColor=#666666`): etiquetas de transición de bajo énfasis.
- Rojo (`strokeColor=#b85450;fontColor=#990000;fillColor=#f8cecc`): estados y transiciones de error/excepción.
- Sin relleno (`fillColor=none` / `default`): estados del camino feliz, para mantener el foco en la forma y el texto.

## Ejemplo de invocación
Usuario:

`$diagrama-maquina-estados genera la máquina de estados de una cerradura inteligente con verificación de acceso por RFID`

Respuesta esperada:

- Identificar estados (ej. `Verificando Acceso, Bloqueado`, `Monitoreando, Bloqueado`, `Actualizando Registros Internos`, `Desbloqueado`) y, si aplica, un estado compuesto de error (ej. `Reconectando, Bloqueado`).
- Listar transiciones en orden de flujo, con su evento, guarda y acción (ej. `smart key presented [valid RFID code]`, `access permitted [valid-key] /unlock`).
- Diferenciar las rutas de error (ej. `battery empty`, `server unresponsive`) en rojo.
- Identificar el pseudo-estado inicial y, si existe, el estado final.
- Entregar XML `.drawio`.

## Prompt interno recomendado
Cuando se active `$diagrama-maquina-estados`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica el objeto, entidad o sistema cuyo ciclo de vida se está modelando, sus estados (simples, compuestos, inicial y final), y las transiciones entre ellos con su evento, guarda `[condición]` y acción `/efecto`. Usa únicamente información explícita del chat; si agregas inferencias, márcalas como hipótesis. Diferencia las rutas de error/excepción del camino feliz. Identifica auto-transiciones y estados compuestos que agrupen sub-estados. Genera una tabla de estados y una tabla de transiciones. Luego genera un archivo XML `.drawio` compatible con diagrams.net, con estructura `<mxfile>`, una página `<diagram>`, `mxGraphModel`, un pseudo-estado inicial (`ellipse;fillColor=#000000`), estados como `UserObject` con `shape=umlState;umlStateSymbol=collapseState`, estados compuestos como `group` + `umlState;container=1` con sub-estados anidados (`parent` apuntando al ID del contenedor), un estado final (`shape=endState`) si aplica, transiciones con `endArrow=open;endFill=0` y su etiqueta `evento [guarda] /acción` como celda hija `edgeLabel`, y rutas de error en rojo (`strokeColor=#b85450;fontColor=#990000;fillColor=#f8cecc`). El XML debe ser válido, editable e importable en draw.io.

## Validaciones antes de entregar
Antes de responder, verifica:

- La máquina de estados tiene al menos un pseudo-estado inicial.
- Cada estado interviene en al menos una transición (entrante o saliente).
- Los estados y transiciones no están inventados como hechos; lo inferido está marcado como hipótesis.
- Cada transición con guarda `[condición]` está claramente etiquetada y, si existen guardas mutuamente excluyentes desde el mismo estado, cubren los casos relevantes.
- Las rutas de error/excepción están diferenciadas visualmente (rojo) del camino feliz.
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>`, `<root>`.
- Todos los `mxCell`/`UserObject` tienen IDs únicos y `parent` correcto (sub-estados dentro de su estado compuesto contenedor).
- El archivo puede guardarse con extensión `.drawio`.
- El usuario puede importar el contenido en diagrams.net.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `diagrama-maquina-estados.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File → Open From → Device**.
5. Abre el archivo `.drawio`.
6. Edita textos, colores o posiciones si hace falta.

## Variante corta para llamar desde cualquier chat
`$diagrama-maquina-estados: toma el contexto actual, identifica el objeto/sistema cuyo ciclo de vida se está modelando, sus estados (inicial, simples, compuestos y final), y las transiciones entre ellos con evento, guarda `[condición]` y acción `/efecto`, diferenciando rutas de error/excepción del camino feliz, genera las tablas correspondientes, y entrega un archivo draw.io editable con formato de diagrama de máquina de estados UML profesional, usando la paleta y estilos del archivo diagrama-maquina-estados.drawio de referencia. No inventes información; lo inferido márcalo como hipótesis.`
