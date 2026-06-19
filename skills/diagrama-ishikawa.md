# Skill: $diagrama-ishikawa

## Activador
Cuando el usuario escriba:

`$diagrama-ishikawa`

debes generar un diagrama Ishikawa / causa-efecto / espina de pescado usando la información disponible en el chat actual.

## Objetivo
Transformar una conversación, análisis, problema, reunión, incidente, proceso o diagnóstico en un diagrama Ishikawa profesional, editable en draw.io / diagrams.net, con formato `.drawio`.

El resultado debe ayudar a identificar:

- Problema central o efecto.
- Categorías principales de causa.
- Causas secundarias.
- Causas críticas o priorizadas.
- Vacíos de información que requieren validación.

## Formato de salida obligatorio
Entregar siempre:

1. **Resumen textual del análisis causal**
2. **Tabla de causas**
3. **Archivo o bloque XML compatible con draw.io**
4. **Instrucciones para importar en diagrams.net**

Cuando sea posible, generar el contenido como archivo `.drawio`.

## Estilo visual requerido
El diagrama debe seguir un formato tipo fishbone similar al ejemplo compartido por el usuario:

- Archivo raíz en formato XML `<mxfile>`.
- Una o más páginas `<diagram>`.
- Estructura `mxGraphModel`.
- Cuerpo principal horizontal apuntando al problema.
- Problema / efecto en una caja rectangular al extremo derecho.
- Categorías principales como cajas de color conectadas a la espina central.
- Ramas superiores e inferiores.
- Subcausas como textos pequeños conectados a cada categoría.
- Uso de colores suaves y profesionales por categoría.
- Líneas limpias, sin cruces innecesarios.
- Texto legible.
- Distribución horizontal en página tipo A4 o landscape.
- Compatible con diagrams.net / draw.io.

## Categorías por defecto
Si el usuario no define categorías, usa una de estas estructuras según el contexto.

### Para procesos, operaciones o negocio
- Personas
- Procesos
- Tecnología / Sistemas
- Datos / Información
- Proveedores / Terceros
- Gestión / Gobierno

### Para software o incidentes técnicos
- Código
- Infraestructura
- Base de datos
- Integraciones
- Seguridad / Configuración
- Operación / Soporte

### Para crédito, cobranzas o procesos financieros
- Cliente
- Asesor / Oficial
- Políticas
- Documentación
- Sistemas / Integraciones
- Riesgo / Cumplimiento

### Para reuniones estratégicas
- Alcance
- Presupuesto
- Responsables
- Riesgos
- Dependencias
- Decisiones pendientes

## Reglas de análisis
Antes de crear el diagrama:

1. Identifica el **problema central**.
2. Extrae causas explícitas mencionadas en el chat.
3. No inventes causas como hechos.
4. Si agregas causas inferidas, márcalas como **hipótesis**.
5. Prioriza causas críticas cuando el usuario haya indicado urgencia, bloqueo, costo, riesgo o impacto.
6. Si falta información, agrega una sección de **preguntas abiertas**, pero no bloquees la generación.
7. Usa lenguaje ejecutivo, claro y breve.
8. Evita textos largos dentro de las cajas; usa frases cortas.

## Marcado de criticidad
Clasifica cada causa como:

- **Alta**: bloquea el proceso, genera riesgo fuerte, costo alto, incumplimiento o conflicto.
- **Media**: afecta eficiencia, calidad o seguimiento.
- **Baja**: mejora deseable, pero no bloqueante.
- **Hipótesis**: posible causa no confirmada por el chat.

En el diagrama:

- Causas críticas pueden usar línea más gruesa.
- No saturar el diagrama con demasiados colores.
- Máximo recomendado: 6 categorías principales.
- Máximo recomendado: 5 causas por categoría.
- Si hay más causas, agrupar o dejar en tabla.

## Estructura de respuesta esperada

### 1. Problema central
Describe el efecto principal en una frase.

### 2. Lectura ejecutiva
Resume en 3 a 6 líneas qué está causando el problema.

### 3. Tabla de causas
Usa esta tabla:

| Categoría | Causa | Tipo | Criticidad | Evidencia del chat | Acción sugerida |
|---|---|---|---|---|---|

Tipo puede ser:

- Explícita
- Inferida
- Hipótesis
- Pendiente de validar

### 4. Diagrama draw.io
Genera XML válido con esta estructura base:

```xml
<mxfile host="app.diagrams.net" modified="AUTO" agent="ChatGPT" version="24.0.0" pages="1">
  <diagram name="Ishikawa" id="ishikawa-001">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" math="0" shadow="0">
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
- `vertex="1"` para cajas y textos.
- `edge="1"` para líneas.
- `mxGeometry` con coordenadas explícitas.
- IDs únicos, simples y consistentes.
- Escapar caracteres especiales XML:
  - `&` como `&amp;`
  - `<` como `&lt;`
  - `>` como `&gt;`
  - `"` como `&quot;` cuando aplique

## Layout sugerido
Usa coordenadas base:

- Espina central: desde `x=120, y=400` hasta `x=900, y=400`.
- Problema: caja en `x=920, y=360, width=210, height=80`.
- Categorías superiores:
  - Categoría 1: `x=120, y=80`
  - Categoría 2: `x=380, y=80`
  - Categoría 3: `x=640, y=80`
- Categorías inferiores:
  - Categoría 4: `x=120, y=620`
  - Categoría 5: `x=380, y=620`
  - Categoría 6: `x=640, y=620`

Cada categoría debe conectarse con una rama diagonal hacia la espina central.

## Paleta sugerida
Usa colores suaves:

- Verde: `fillColor=#d5e8d4;strokeColor=#82b366`
- Amarillo: `fillColor=#fff2cc;strokeColor=#d6b656`
- Rojo suave: `fillColor=#f8cecc;strokeColor=#b85450`
- Azul: `fillColor=#dae8fc;strokeColor=#6c8ebf`
- Morado: `fillColor=#e1d5e7;strokeColor=#9673a6`
- Gris: `fillColor=#f5f5f5;strokeColor=#666666`

La espina central puede usar:

`strokeColor=#D1C6A7;strokeWidth=4`

El problema central puede usar:

`fillColor=#f9f7ed;strokeColor=#D1C6A7;strokeWidth=3`

## Ejemplo de invocación
Usuario:

`$diagrama-ishikawa analiza la reunión anterior y genera un drawio del problema de retraso en implementación`

Respuesta esperada:

- Identificar el problema central.
- Agrupar causas.
- Marcar causas críticas.
- Entregar XML `.drawio`.

## Prompt interno recomendado
Cuando se active `$diagrama-ishikawa`, usa este prompt internamente:

> Analiza todo el contexto disponible del chat. Identifica el problema central y construye un diagrama Ishikawa profesional. Usa únicamente información explícita del chat; si agregas inferencias, márcalas como hipótesis. Genera una tabla de causas con categoría, causa, tipo, criticidad, evidencia y acción sugerida. Luego genera un archivo XML `.drawio` compatible con diagrams.net, con estructura `<mxfile>`, una página `<diagram>`, `mxGraphModel`, espina central horizontal, problema a la derecha, seis categorías principales como ramas superiores e inferiores, subcausas como textos conectados y estilo visual profesional con colores suaves. El XML debe ser válido, editable e importable en draw.io.

## Validaciones antes de entregar
Antes de responder, verifica:

- El problema central está claro.
- No hay más de 6 categorías principales.
- Las causas no están inventadas como hechos.
- Las hipótesis están marcadas.
- El XML tiene `<mxfile>`, `<diagram>`, `<mxGraphModel>`, `<root>`.
- Todos los `mxCell` tienen IDs únicos.
- El archivo puede guardarse con extensión `.drawio`.
- El usuario puede importar el contenido en diagrams.net.

## Instrucciones para el usuario
Para usar el resultado:

1. Copia el XML generado.
2. Guarda el archivo como `diagrama-ishikawa.drawio`.
3. Abre https://app.diagrams.net/
4. Selecciona **File → Open From → Device**.
5. Abre el archivo `.drawio`.
6. Edita textos, colores o posiciones si hace falta.

## Variante corta para llamar desde cualquier chat
`$diagrama-ishikawa: toma el contexto actual, identifica el problema central, agrupa causas en máximo seis categorías, marca criticidad, genera tabla de causas y entrega un archivo draw.io editable con formato Ishikawa profesional. No inventes información; lo inferido márcalo como hipótesis.`
