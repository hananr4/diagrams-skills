# Skill: $diagrama-arquitectura-sistema

## Activador
`$diagrama-arquitectura-sistema`

Genera un diagrama **C4 — nivel Componente** (solo ese nivel) a partir del contexto del chat. No generes Context, Container ni Class salvo que el usuario lo pida explícitamente en otro momento.

## Objetivo
Mostrar, dentro de **un contenedor**, sus componentes internos, sus tecnologías, sus relaciones entre sí y con bases de datos/sistemas externos que ese contenedor consume directamente.

## Alcance (qué NO incluir)
- No dibujes actores externos al sistema salvo el(los) que disparan directamente al contenedor (máx. 1-2).
- No dibujes otros contenedores como cajas grandes "Container"; si un componente llama a otro contenedor, represéntalo como una caja gris simple (System/Container externo) sin desglosar.
- No generes página de Contexto ni de Clase. Una sola página: `C4 Component`.
- No saturar: 4-8 componentes por diagrama. Si hay más, agrupa o señala que se requiere una segunda página (pero no la generes sin que te lo pidan).

## Reglas de análisis
1. Identifica el **contenedor** que se está detallando (nombre + tecnología).
2. Identifica los **componentes** dentro de ese contenedor: nombre, tecnología, responsabilidad (una frase).
3. Identifica relaciones componente→componente, componente→base de datos, componente→sistema/contenedor externo, con **verbo** y **tecnología/protocolo**.
4. No inventes componentes ni relaciones. Si infieres algo, márcalo `[hipótesis]` en la tabla y en el diagrama (texto en cursiva o nota), nunca como hecho.
5. Si falta información clave (ej. no se sabe la tecnología de un componente), pregúntalo o márcalo como `[pendiente]`; no lo omitas en silencio.

## Salida obligatoria
1. Resumen en 2-3 líneas: qué contenedor se modela y qué hacen sus componentes en conjunto.
2. Tabla de componentes:

| Componente | Tecnología | Responsabilidad | Relevancia (núcleo/complementario/hipótesis) |
|---|---|---|---|

3. Tabla de relaciones:

| Origen | Destino | Verbo/descripción | Tecnología | Relevancia |
|---|---|---|---|---|

4. XML `.drawio` con **una sola página** `C4 Component`.

## Estructura XML
```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram id="component-001" name="C4 Component">
    <mxGraphModel dx="1131" dy="761" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="827" pageHeight="1169" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Componentes, relaciones, y opcionalmente caja envolvente del contenedor -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Estilos (tomados de diagrama-arquitectura-sistema.drawio)

Componente (azul claro):
```
rounded=1;whiteSpace=wrap;html=1;labelBackgroundColor=none;fillColor=#85BBF0;fontColor=#ffffff;align=center;arcSize=10;strokeColor=#78A8D8;metaEdit=1;
```
Geometría: `width=160`, `height=110`.

Sistema/contenedor externo referenciado pero no desglosado (gris):
```
rounded=1;whiteSpace=wrap;html=1;labelBackgroundColor=none;fillColor=#999999;fontColor=#ffffff;align=center;arcSize=10;strokeColor=#8A8A8A;metaEdit=1;
```

Actor/persona (si aplica, máx. 1-2):
```
html=1;dashed=0;whitespace=wrap;fillColor=#08427b;strokeColor=none;fontColor=#ffffff;shape=mxgraph.c4.person;align=center;metaEdit=1;
```
Geometría: `width=110`, `height=140`.

Base de datos:
```
shape=cylinder;whiteSpace=wrap;html=1;boundedLbl=1;rounded=0;labelBackgroundColor=none;fillColor=#438DD5;fontColor=#ffffff;align=center;strokeColor=#3C7FC0;metaEdit=1;
```

Relación (línea punteada gris, con verbo + tecnología):
```
edgeStyle=none;rounded=0;html=1;jettySize=auto;orthogonalLoop=1;strokeColor=#707070;strokeWidth=2;fontColor=#707070;dashed=1;metaEdit=1;
```
Etiqueta: `<b>%verbo%</b>` arriba, `[%tecnología%]` abajo, ambos centrados.

Caja envolvente del contenedor (opcional, blanca):
```
rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#666666;align=left;verticalAlign=bottom;
```

## Layout
- Componentes en 2-3 columnas, separación `~190px` en `x`, `~150px` en `y`.
- Actor (si existe) arriba, fuera de la caja del contenedor.
- Bases de datos y sistemas externos en los bordes (izquierda/derecha o abajo), no en el centro.
- Sin leyenda salvo que el usuario la pida explícitamente.

## Validaciones antes de entregar
- Hay un solo `<diagram>` y es `C4 Component`.
- Cada componente tiene tecnología y responsabilidad; si no se sabe, dice `[pendiente]`, no se inventa.
- Cada relación tiene verbo y tecnología.
- No aparecen cajas "Container" grandes para sistemas externos (solo cajas simples grises).
- IDs únicos, `source`/`target` válidos, XML bien formado e importable en draw.io.

## Instrucciones para el usuario
1. Copia el XML.
2. Guarda como `diagrama-arquitectura-sistema.drawio`.
3. Ábrelo en https://app.diagrams.net/ (File → Open From → Device).
