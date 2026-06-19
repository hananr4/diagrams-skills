# diagrama-er — Plantilla y convenciones para diagramas ER en draw.io

Referencia basada en la estructura de [diagrama-e-r.drawio](diagrama-e-r.drawio). Úsala como guía al crear o modificar diagramas entidad-relación con el formato `mxGraphModel` de draw.io.

## Estructura general del archivo

```xml
<mxfile host="app.diagrams.net" ...>
  <diagram name="Page-1" id="...">
    <mxGraphModel dx="1400" dy="763" grid="1" gridSize="10" guides="1" tooltips="1"
                  connect="1" arrows="1" fold="1" page="1" pageScale="1"
                  pageWidth="1100" pageHeight="850" background="none" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- tablas y relaciones aquí, parent="1" -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Cada elemento tiene un `id` único. En el archivo de referencia se usa un prefijo compartido (`2e49270ec7c68f3f-N`) para evitar colisiones; al añadir tablas nuevas, genera un prefijo propio por tabla.

## Anatomía de una tabla (entidad)

Una tabla es un `swimlane` contenedor + una fila por atributo. Patrón mínimo:

```xml
<mxCell id="TBL" parent="1" value="NombreTabla" vertex="1"
        style="swimlane;html=1;fontStyle=0;childLayout=stackLayout;horizontal=1;startSize=26;
               fillColor=#e0e0e0;horizontalStack=0;resizeParent=1;resizeLast=0;collapsible=1;
               marginBottom=0;swimlaneFillColor=#ffffff;align=center;rounded=0;shadow=0;
               comic=0;labelBackgroundColor=none;strokeWidth=1;fontFamily=Verdana;fontSize=14">
  <mxGeometry x="290" y="140" width="160" height="N" as="geometry" />
</mxCell>
```

- `height` del contenedor = `startSize` (26) + suma de `height` de cada fila.
- `width` estándar = 160.

### Filas con clave (PK / FK)

Filas que son PK y/o FK usan `fontStyle=5` (negrita+subrayado) en la fila y `fontStyle=1` (negrita) en la celda de etiqueta, con `spacingLeft=60` (deja espacio a la etiqueta "PK,FK1") o `spacingLeft=34` (deja espacio solo a "PK"):

```xml
<mxCell id="ROW" parent="TBL" value="nombreCampo" vertex="1"
        style="shape=partialRectangle;top=0;left=0;right=0;bottom=0;html=1;align=left;
               verticalAlign=middle;fillColor=none;spacingLeft=60;spacingRight=4;
               whiteSpace=wrap;overflow=hidden;rotatable=0;points=[[0,0.5],[1,0.5]];
               portConstraint=eastwest;dropTarget=0;fontStyle=5">
  <mxGeometry y="26" width="160" height="30" as="geometry" />
</mxCell>
<mxCell id="ROW-LABEL" parent="ROW" value="PK,FK1" connectable="0" vertex="1"
        style="shape=partialRectangle;fontStyle=1;top=0;left=0;bottom=0;html=1;fillColor=none;
               align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;whiteSpace=wrap;
               overflow=hidden;rotatable=0;points=[];portConstraint=eastwest;part=1">
  <mxGeometry width="56" height="30" as="geometry" />
</mxCell>
```

Etiquetas vistas en el archivo: `PK`, `PK,FK1`, `PK,FK2`. `spacingLeft=60`/ancho de etiqueta `56` cuando hay FK; `spacingLeft=34`/ancho `30` cuando es solo PK.

### Filas normales (atributos)

Sin clave: `fontStyle` por defecto (no se especifica = normal), `verticalAlign=top`, etiqueta vacía (`value=""`), altura típica `26` (la última fila decorativa de cierre puede tener `height=10`):

```xml
<mxCell id="ROW" parent="TBL" value="nombreCampo" vertex="1"
        style="shape=partialRectangle;top=0;left=0;right=0;bottom=0;html=1;align=left;
               verticalAlign=top;fillColor=none;spacingLeft=34;spacingRight=4;whiteSpace=wrap;
               overflow=hidden;rotatable=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;
               dropTarget=0">
  <mxGeometry y="56" width="160" height="26" as="geometry" />
</mxCell>
<mxCell id="ROW-LABEL" parent="ROW" value="" connectable="0" vertex="1"
        style="shape=partialRectangle;top=0;left=0;bottom=0;html=1;fillColor=none;align=left;
               verticalAlign=top;spacingLeft=4;spacingRight=4;whiteSpace=wrap;overflow=hidden;
               rotatable=0;points=[];portConstraint=eastwest;part=1">
  <mxGeometry width="30" height="26" as="geometry" />
</mxCell>
```

La última fila de cada tabla (`bottom=0` en el contenedor anterior debe pasar a la última) suele recortarse a `height=10` como remate visual.

## Relaciones (edges)

Las relaciones conectan la **fila de clave** de una tabla con la fila correspondiente de otra (`source`/`target` apuntan a los `id` de fila, no de tabla).

Dos estilos de edge usados:

- `edgeStyle=orthogonalEdgeStyle` — para relaciones con tramos en ángulo recto y puntos intermedios (`Array as="points"`).
- `edgeStyle=entityRelationEdgeStyle` — para relaciones rectas simples entre `exitX/exitY` y `entryX/entryY`.

Notación de cardinalidad (extremos `startArrow`/`endArrow`):

| Valor | Significado |
|---|---|
| `ERmandOne` | uno obligatorio (exactamente 1) |
| `ERzeroToOne` | cero o uno |
| `ERzeroToMany` | cero o muchos |
| `ERmany` | muchos |
| `ERoneToMany` | uno a muchos (extremo combinado) |

Ejemplo (uno obligatorio → cero o muchos):

```xml
<mxCell id="EDGE" edge="1" parent="1" source="FILA_PK_ORIGEN" target="FILA_FK_DESTINO" value=""
        style="edgeStyle=orthogonalEdgeStyle;html=1;endArrow=ERzeroToMany;startArrow=ERmandOne;
               labelBackgroundColor=none;fontFamily=Verdana;fontSize=14;
               entryX=0;entryY=0.5;exitX=0;exitY=0.5">
  <mxGeometry height="100" relative="1" width="100" as="geometry">
    <Array as="points">
      <mxPoint x="250" y="401" />
      <mxPoint x="250" y="239" />
    </Array>
    <mxPoint x="100" y="430" as="sourcePoint" />
    <mxPoint x="200" y="330" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

## Layout / espaciado observado

- Separación horizontal entre columnas de tablas: ~280-300px (x: 30, 290, 570/580, 890).
- Separación vertical entre filas de tablas: ~140-220px.
- `pageWidth`/`pageHeight`: 1100x850 (tamaño A4 horizontal aprox.).

## Checklist al crear una entidad nueva

1. Define un prefijo de `id` único para la tabla.
2. Crea el contenedor `swimlane` con `value` = nombre real de la entidad (no dejar "Table").
3. Añade una fila por atributo, con `value` = nombre real del campo (no dejar "row N").
4. Marca con `PK`/`PK,FKn` solo las filas que correspondan, ajustando `spacingLeft`/ancho de etiqueta.
5. Ajusta el `height` del contenedor para que sea coherente con la suma de filas + 26.
6. Conecta relaciones apuntando a los `id` de **fila** (no de tabla), eligiendo la cardinalidad correcta en `startArrow`/`endArrow`.

## Nota sobre el archivo actual

`diagrama-e-r.drawio` contiene 8 tablas y 10 relaciones, pero todas las tablas conservan el nombre placeholder `Table` y los campos sin clave usan `row N` / valor vacío — es decir, es un esqueleto sin nombres de dominio reales. Antes de documentarlo como modelo de datos concreto, hay que completar `value` de tablas y filas con los nombres reales de entidades/atributos.
