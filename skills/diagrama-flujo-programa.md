# Skill: $diagrama-flujo-programa

## Activador

Cuando el usuario escriba:

`$diagrama-flujo-programa`

analiza el código fuente proporcionado o disponible en el contexto y genera un diagrama de flujo que explique, en lenguaje cotidiano, qué realiza el programa.

Admite, entre otros:

- Scripts y objetos de SQL, como procedimientos almacenados, funciones y disparadores.
- Código C# y otros lenguajes de backend.
- Código TypeScript o JavaScript.
- Código PowerBuilder.
- Scripts, funciones, métodos o programas de otros lenguajes.

## Objetivo

Convertir la lógica del código en una explicación visual comprensible para una persona que no programa. El resultado debe mostrar qué información recibe, qué decisiones toma, qué acciones realiza, qué resultados produce y en qué situaciones termina o informa un problema.

No documentar el código línea por línea. Resumir su intención y comportamiento desde el punto de vista del negocio o de la persona usuaria.

## Fuente de análisis

1. Usar el archivo, bloque de código o programa indicado por el usuario.
2. Si el usuario no señala un archivo concreto, usar el código disponible en el contexto actual.
3. Revisar funciones, procedimientos o archivos auxiliares llamados directamente cuando sean necesarios para comprender el flujo.
4. No asumir el comportamiento de dependencias cuyo contenido no esté disponible. Marcarlo como **por confirmar**.
5. Si no hay código suficiente para identificar ningún flujo, solicitar el archivo o bloque de código necesario.

## Reglas de lenguaje no técnico

- Escribir para una persona sin conocimientos de programación.
- Expresar cada paso como una acción o decisión de negocio: `Busca la información del cliente`, `Calcula la tasa`, `¿La solicitud cumple los requisitos?`.
- No mostrar nombres de variables, parámetros, tablas, columnas, clases, métodos ni detalles de sintaxis en el diagrama.
- Eliminar prefijos, símbolos y convenciones técnicas. Ejemplos:
  - `@AS_TIPO_TABLA` se convierte en `tipo de tabla`.
  - `@ADEC_TASA` se convierte en `tasa`.
  - `lstCliente`, `customerList` o `ClientesDTO` se convierten en `clientes`.
  - `fn_calcular_mora()` se convierte en `calcula el recargo por atraso`.
- Traducir operaciones técnicas a su efecto comprensible:
  - `SELECT` → `consulta` o `busca información`.
  - `INSERT` → `registra`.
  - `UPDATE` → `actualiza`.
  - `DELETE` → `elimina`.
  - `COMMIT` → `confirma los cambios`.
  - `ROLLBACK` → `cancela los cambios realizados`.
  - `TRY/CATCH` o manejo de excepciones → `si ocurre un problema`.
  - Bucle → `repite el proceso para cada elemento`.
- Evitar siglas y términos técnicos cuando exista una frase cotidiana equivalente.
- Usar textos breves: idealmente entre 3 y 9 palabras por figura.

## Regla sobre el nombre técnico de origen

El nombre real del programa, archivo, función, método, procedimiento almacenado u objeto de base de datos se puede mencionar **únicamente en la descripción textual del proceso**.

No incluir ese nombre técnico en:

- El título visible del diagrama.
- Las figuras o decisiones.
- Las flechas o etiquetas de ruta.
- Las tablas de pasos o decisiones.
- El nombre visible de la página del diagrama.

Usar un título genérico y funcional, por ejemplo: `Flujo para calcular una cuota` o `Proceso para registrar una solicitud`.

## Reglas de análisis

Antes de dibujar:

1. Identificar el propósito principal del programa.
2. Determinar qué evento o solicitud inicia el proceso.
3. Identificar la información de entrada y traducir sus nombres a lenguaje cotidiano.
4. Agrupar instrucciones consecutivas que persigan el mismo resultado en un solo paso funcional.
5. Identificar decisiones y redactarlas como preguntas claras con rutas `Sí` y `No`, o con opciones igualmente comprensibles.
6. Identificar repeticiones y representarlas como un ciclo solo cuando sean importantes para entender el proceso.
7. Identificar consultas, registros, cálculos, validaciones, comunicaciones y resultados.
8. Diferenciar el camino principal de las rutas alternativas y de problema.
9. Identificar todos los finales relevantes: resultado exitoso, sin información, rechazo o problema.
10. No inventar reglas de negocio. Marcar cualquier inferencia necesaria como **por confirmar**.

## Nivel de detalle

- Priorizar entre 6 y 15 figuras en el flujo principal.
- Agrupar detalles repetitivos o puramente técnicos en una sola acción comprensible.
- Si existen varios procesos claramente independientes, crear una página por proceso dentro del mismo archivo `.drawio`.
- Si una sección supera 10 pasos, resumirla como un subproceso con un nombre funcional.
- Mostrar una decisión únicamente cuando cambie el camino o el resultado visible del proceso.

## Formato de salida obligatorio

Entregar siempre:

1. **Descripción del proceso**: 1 a 3 párrafos en lenguaje cotidiano. Esta es la única sección donde se permite indicar el nombre técnico exacto del programa, función, método, archivo, procedimiento almacenado u objeto de base de datos analizado.
2. **Entradas y resultados**: lista breve con nombres comprensibles, sin identificadores técnicos.
3. **Pasos del proceso**: tabla ordenada con columnas `#`, `Paso`, `Tipo` y `Ruta`.
4. **Supuestos o puntos por confirmar**, solo cuando correspondan.
5. **Diagrama editable**: archivo [`diagrama-flujo-programa.drawio`](../diagrama-ejemplo/diagrama-flujo-programa.drawio), actualizado con el flujo analizado.

No entregar únicamente una imagen. El archivo `.drawio` editable es obligatorio.

## Estructura de la respuesta

### Descripción del proceso

Explicar el propósito y el resultado. Incluir aquí, y solo aquí, una frase como:

`Este diagrama se elaboró a partir del procedimiento almacenado spPrcCalcularCuota.`

### Entradas y resultados

- **Recibe:** información expresada con nombres cotidianos.
- **Entrega:** resultado principal y resultados alternativos relevantes.

### Pasos del proceso

| # | Paso | Tipo | Ruta |
|---|---|---|---|
| 1 | Recibe la solicitud | Inicio | Principal |
| 2 | Verifica la información | Acción | Principal |
| 3 | ¿La información está completa? | Decisión | Sí / No |

No incluir identificadores técnicos en esta tabla.

### Supuestos o puntos por confirmar

Incluir esta sección solo si el código no permite confirmar una regla, una dependencia o un resultado.

### Diagrama

Entregar o actualizar:

[`diagrama-flujo-programa.drawio`](../diagrama-ejemplo/diagrama-flujo-programa.drawio)

## Estilo visual requerido

Tomar como plantilla el archivo `diagrama-ejemplo/diagrama-flujo-programa.drawio`.

- Orientar el flujo principal de arriba hacia abajo.
- Usar una figura de inicio naranja y una figura de fin roja suave.
- Usar rectángulos azules para acciones.
- Usar rombos verdes para decisiones.
- Etiquetar las rutas de decisión con `Sí`, `No` u opciones breves y naturales.
- Usar conectores ortogonales con flecha y evitar cruces.
- Colocar las rutas alternativas a los lados del camino principal.
- Incluir dentro del lienzo un título funcional genérico y una descripción de una línea, ambos sin el nombre técnico del objeto analizado.
- Mantener tipografía legible, contraste suficiente y espacio uniforme entre figuras.

## Reglas técnicas del archivo draw.io

Generar XML válido e importable en diagrams.net con:

- Raíz `<mxfile>`.
- Una o más páginas `<diagram>`.
- Un `<mxGraphModel>` y su `<root>` por página.
- IDs únicos en todos los `mxCell`.
- Figuras con `vertex="1"` y conectores con `edge="1"`.
- Conectores con `source` y `target` válidos.
- Texto escapado correctamente para XML.
- Extensión final `.drawio`.

Usar preferentemente estos estilos de la plantilla:

Inicio y fin:

```text
html=1;dashed=0;whiteSpace=wrap;shape=mxgraph.dfd.start;
```

Acción:

```text
whiteSpace=wrap;html=1;dashed=0;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Decisión:

```text
rhombus;whiteSpace=wrap;html=1;dashed=0;fillColor=#d5e8d4;strokeColor=#82b366;
```

Conector:

```text
edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;
```

## Validaciones antes de entregar

Comprobar que:

- La descripción indica el propósito y menciona el nombre técnico de la fuente solo allí.
- El diagrama tiene al menos un inicio y un fin.
- Todas las decisiones tienen sus rutas etiquetadas.
- No quedan nombres de variables, parámetros, tablas, columnas, clases, métodos, funciones u objetos técnicos dentro del diagrama ni de las tablas.
- Cada texto puede ser entendido sin leer el código fuente.
- El flujo refleja el comportamiento real del programa y no reglas inventadas.
- Las rutas de problema o resultados alternativos importantes están representadas.
- El XML es válido y el archivo abre en diagrams.net.
- El resultado final existe en `diagrama-ejemplo/diagrama-flujo-programa.drawio`.

## Ejemplo de invocación

`$diagrama-flujo-programa analiza el procedimiento almacenado adjunto y documenta lo que realiza para una persona de negocio.`

Resultado esperado:

- Una descripción que identifica el procedimiento analizado y explica su finalidad.
- Entradas, resultados y pasos con términos como `tipo de tabla` y `tasa`, nunca `@AS_TIPO_TABLA` ni `@ADEC_TASA`.
- Un archivo `diagrama-ejemplo/diagrama-flujo-programa.drawio` editable, con un título funcional y sin identificadores técnicos.

## Prompt interno recomendado

> Analiza el código indicado y reconstruye su comportamiento de principio a fin. Explica el propósito para una persona que no programa. Agrupa los detalles de implementación en acciones de negocio, convierte las condiciones en preguntas claras y representa las rutas principales, alternativas y de problema. No muestres nombres de variables, parámetros, tablas, columnas, clases, métodos ni sintaxis. Sustituye cada identificador por una expresión cotidiana; por ejemplo, `@AS_TIPO_TABLA` por `tipo de tabla` y `@ADEC_TASA` por `tasa`. Menciona el nombre técnico exacto del programa, función, método, archivo, procedimiento almacenado u objeto de base de datos únicamente en la descripción textual del proceso. Genera o actualiza `diagrama-ejemplo/diagrama-flujo-programa.drawio` usando la plantilla visual existente y verifica que el XML sea válido, editable y comprensible sin conocimientos de programación.
