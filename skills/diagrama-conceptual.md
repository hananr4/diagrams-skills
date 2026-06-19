# Skill: $diagrama-conceptual

## Activador
Cuando el usuario escriba:

`$diagrama-conceptual`

debes generar un **diagrama conceptual** a partir del contexto disponible en el chat o de la informacion explicita que entregue el usuario.

## Objetivo
Transformar una idea, requerimiento, problema, dominio, sistema o conjunto de conceptos en un mapa conceptual editable en draw.io / diagrams.net.

El resultado debe mostrar:

- Concepto central o raiz.
- Categorias principales relacionadas con el concepto central.
- Subconceptos, factores, causas, sintomas, consecuencias, soluciones, aplicaciones o retos, segun el dominio.
- Relaciones claras entre conceptos, preferiblemente con verbo o etiqueta.
- Inferencias marcadas como hipotesis cuando no esten confirmadas por el usuario.

## Referencia visual
Usa como referencia el archivo `diagrama-conceptual.drawio`, que contiene seis patrones de mapa conceptual:

1. **Differential diagnosis**: concepto central con categorias como causas, sintomas, pruebas, tratamientos y mecanismos.
2. **Purchasing factors**: factores que afectan una decision, con relaciones etiquetadas como `affects`.
3. **Customer feedback**: problema principal, causas agrupadas y acciones correctivas.
4. **Energy fault map**: evento raiz, causas de demanda/suministro/infraestructura y consecuencias.
5. **Smart template concept map**: tema raiz con ramas de definicion, tecnicas, herramientas, aplicaciones, retos y futuro.
6. **Mind-body bridging map**: mapa de relaciones entre percepciones, emociones, decisiones, tensiones, requisitos y alternativas.

## Alcance
El diagrama conceptual NO es:

- Diagrama UML de clases.
- Diagrama entidad-relacion.
- Diagrama de secuencia.
- Diagrama C4 de componentes.
- Diagrama de proceso BPMN.

Si el usuario pide explicitamente uno de esos formatos, usa el skill correspondiente. Si solo pide organizar conceptos, causas, factores, decisiones, diagnosticos, problemas o ideas, usa `$diagrama-conceptual`.

## Reglas de analisis
Antes de generar el diagrama:

1. Identifica el **concepto central**. Debe ser una frase corta y concreta.
2. Identifica entre 3 y 7 **categorias principales**. Ejemplos: causas, sintomas, pruebas, tratamientos, factores, problemas, soluciones, aplicaciones, retos, mecanismos, consecuencias.
3. Identifica **subconceptos** bajo cada categoria.
4. Determina el tipo de relacion entre conceptos:
   - `incluye`
   - `causa`
   - `afecta`
   - `resulta en`
   - `requiere`
   - `se evalua con`
   - `se mitiga con`
   - `depende de`
   - `genera`
   - `se relaciona con`
5. No inventes conceptos como hechos confirmados. Si agregas inferencias utiles, marcalas como **hipotesis** en tablas y en el diagrama.
6. Si falta informacion clave, genera el diagrama con `[pendiente]` en el nodo o tabla, en vez de detenerte.
7. Evita saturar el diagrama. Si hay demasiados conceptos, conserva los mas importantes en el dibujo y deja el resto en una tabla de detalle.
8. Mantén etiquetas de nodos breves: idealmente 2 a 6 palabras.
9. Usa relaciones etiquetadas cuando aclaren la lectura. Si la relacion es obvia por la jerarquia, puede omitirse la etiqueta.

## Formato de salida obligatorio
Entrega siempre:

1. **Resumen conceptual** en 2 a 4 lineas.
2. **Tabla de conceptos**.
3. **Tabla de relaciones**.
4. **XML `.drawio`** con una sola pagina.
5. **Instrucciones breves de importacion**.

## Tabla de conceptos
Usa esta estructura:

| Concepto | Tipo | Categoria padre | Relevancia | Evidencia |
|---|---|---|---|---|

Valores sugeridos para `Tipo`:

- Raiz
- Categoria
- Subconcepto
- Causa
- Efecto
- Problema
- Solucion
- Herramienta
- Aplicacion
- Reto
- Hipotesis

Valores sugeridos para `Relevancia`:

- Nucleo
- Complementario
- Hipotesis
- Pendiente

## Tabla de relaciones
Usa esta estructura:

| Origen | Destino | Relacion | Tipo | Relevancia |
|---|---|---|---|---|

Valores sugeridos para `Tipo`:

- Jerarquia
- Causal
- Influencia
- Dependencia
- Mitigacion
- Evaluacion
- Consecuencia
- Asociacion

## Estructura XML base
Genera XML compatible con diagrams.net:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram id="conceptual-001" name="Diagrama Conceptual">
    <mxGraphModel dx="1322" dy="603" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="0" pageScale="1" pageWidth="1169" pageHeight="827" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Nodos, relaciones y etiquetas generadas aqui -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Estilos de referencia
Los estilos estan tomados del patron visual de `diagrama-conceptual.drawio`.

### Concepto raiz
Usa un nodo redondeado destacado, centrado o arriba:

```text
rounded=1;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontStyle=1;labelBackgroundColor=none;fillColor=#fff2cc;strokeColor=#d6b656;
```

Geometria sugerida: `width=150`, `height=60`.

### Categoria principal
Usa nodos redondeados con color por categoria:

```text
rounded=1;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;labelBackgroundColor=none;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Geometria sugerida: `width=130`, `height=50`.

### Subconcepto
Usa nodos compactos redondeados:

```text
rounded=1;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=11;labelBackgroundColor=none;
```

Geometria sugerida: `width=120`, `height=50`.

### Causa o problema
Usa rojo suave:

```text
rounded=1;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=11;labelBackgroundColor=none;fillColor=#f8cecc;strokeColor=#b85450;
```

### Solucion, oportunidad o alternativa
Usa nube verde cuando represente una opcion, intervencion o idea de mejora:

```text
ellipse;shape=cloud;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=11;labelBackgroundColor=none;fillColor=#d5e8d4;strokeColor=#82b366;
```

### Consecuencia, riesgo o estado
Usa elipse naranja:

```text
ellipse;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=11;labelBackgroundColor=none;fillColor=#ffe6cc;strokeColor=#d79b00;
```

### Decision o accion
Usa hexagono rojo suave:

```text
shape=hexagon;perimeter=hexagonPerimeter2;whiteSpace=wrap;html=1;fixedSize=1;fontFamily=Helvetica;fontSize=11;labelBackgroundColor=none;rounded=1;fillColor=#f8cecc;strokeColor=#b85450;
```

### Texto explicativo
Para notas o bloques tipo lista:

```text
text;html=1;whiteSpace=wrap;overflow=hidden;rounded=0;fontFamily=Helvetica;fontSize=11;fontColor=default;labelBackgroundColor=none;
```

### Relacion principal
Usa conectores curvos con flecha:

```text
edgeStyle=none;shape=connector;curved=1;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;strokeColor=default;align=center;verticalAlign=middle;fontFamily=Helvetica;fontSize=11;fontColor=default;labelBackgroundColor=none;endArrow=classic;
```

### Relacion asociativa o inferida
Usa linea punteada:

```text
edgeStyle=none;shape=connector;curved=1;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;strokeColor=default;align=center;verticalAlign=middle;fontFamily=Helvetica;fontSize=11;fontColor=default;labelBackgroundColor=none;endArrow=classic;dashed=1;
```

## Paleta sugerida
Usa colores para distinguir significado, no solo decoracion:

- Raiz o concepto central: `fillColor=#fff2cc;strokeColor=#d6b656`
- Categoria informativa: `fillColor=#dae8fc;strokeColor=#6c8ebf`
- Causa, problema o dolor: `fillColor=#f8cecc;strokeColor=#b85450`
- Solucion, alternativa u oportunidad: `fillColor=#d5e8d4;strokeColor=#82b366`
- Consecuencia, riesgo o mecanismo: `fillColor=#ffe6cc;strokeColor=#d79b00`
- Concepto secundario o neutro: sin `fillColor` explicito o `fillColor=#ffffff;strokeColor=#666666`
- Hipotesis: mismo color de su categoria, pero con `dashed=1`

## Layout recomendado
Elige el layout segun el tipo de informacion:

### Layout radial
Para temas generales, factores, aplicaciones o conocimiento:

- Concepto raiz al centro o arriba.
- Categorias principales alrededor en semicirculo o filas.
- Subconceptos debajo o alrededor de cada categoria.
- Relaciones desde raiz hacia categorias y de categorias hacia subconceptos.

### Layout causal
Para problemas, fallas, diagnosticos o feedback:

- Problema o evento principal a la izquierda o arriba.
- Causas agrupadas por familia en el centro.
- Consecuencias a la derecha o abajo.
- Soluciones en verde cerca de la causa que mitigan.

### Layout jerarquico
Para mapas generados desde texto o conocimiento estructurado:

- Raiz arriba.
- Categorias en segunda fila.
- Subconceptos en tercera y cuarta fila.
- Evitar mas de 4 niveles visibles en una sola pagina.

## Reglas tecnicas para XML draw.io

- Usa una sola pagina `<diagram>`.
- Usa `mxCell` con `vertex="1"` para nodos.
- Usa `mxCell` con `edge="1"` para conectores.
- Todos los IDs deben ser unicos y legibles, por ejemplo `node-root`, `node-causas`, `edge-root-causas`.
- Cada nodo debe tener `parent="1"`.
- Cada conector debe tener `source` y `target` validos.
- Cada nodo debe tener `mxGeometry` con `x`, `y`, `width`, `height`.
- Escapa caracteres XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique
- Si una etiqueta contiene saltos visuales, usa HTML simple compatible con draw.io, por ejemplo `Concepto&lt;div&gt;secundario&lt;/div&gt;`.

## Ejemplo de invocacion
Usuario:

`$diagrama-conceptual genera un mapa conceptual sobre los factores que afectan la aprobacion de creditos`

Respuesta esperada:

- Concepto raiz: `Aprobacion de creditos`.
- Categorias: `Perfil del cliente`, `Capacidad de pago`, `Garantias`, `Politicas internas`, `Riesgo`, `Documentacion`.
- Subconceptos por categoria.
- Relaciones etiquetadas como `afecta`, `requiere`, `se evalua con`, `mitiga`.
- XML `.drawio` editable.

## Prompt interno recomendado
Cuando se active `$diagrama-conceptual`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica el concepto central y organiza los conceptos relacionados en categorias y subconceptos. Distingue causas, efectos, problemas, soluciones, herramientas, aplicaciones, retos e hipotesis. No inventes informacion como hecho; marca lo inferido como hipotesis. Genera una tabla de conceptos y una tabla de relaciones. Luego crea un XML `.drawio` importable en diagrams.net con una sola pagina, usando nodos redondeados para conceptos, colores semanticos por tipo, conectores curvos o jerarquicos con etiquetas cuando ayuden a entender la relacion, IDs unicos y layout limpio.

## Validaciones antes de entregar
Antes de responder, verifica:

- Existe un concepto raiz claro.
- Hay entre 3 y 7 categorias principales, salvo que el usuario pida algo mas pequeño.
- Cada subconcepto pertenece a una categoria o se marca como asociado.
- Las relaciones importantes tienen verbo o etiqueta.
- Las hipotesis estan marcadas.
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>` y `<root>`.
- Hay una sola pagina.
- Todos los `source` y `target` de conectores existen.
- El diagrama no esta saturado: si hay exceso de conceptos, se prioriza y se documenta el resto en tabla.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `diagrama-conceptual.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File -> Open From -> Device**.
5. Abre el archivo `.drawio`.
6. Ajusta posiciones o textos si necesita refinamiento visual.

## Variante corta para llamar desde cualquier chat
`$diagrama-conceptual: toma el contexto actual, identifica el concepto raiz, categorias, subconceptos y relaciones; clasifica causas, efectos, problemas, soluciones, aplicaciones, retos e hipotesis; genera tablas de conceptos y relaciones; entrega XML draw.io editable de una sola pagina usando colores semanticos, conectores claros y layout limpio basado en diagrama-conceptual.drawio.`
