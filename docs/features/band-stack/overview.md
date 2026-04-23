# Descripción general del Band Stack

El Band Stack es una franja vertical de marcadores de frecuencia que aparece junto a cada panadapter (visualizador panorámico). Úselo para guardar, recuperar y gestionar posiciones de sintonía sin salir de la vista del panadapter.

## Cómo funciona

El panel Band Stack aparece automáticamente junto a cada panadapter cuando se conecta un radio. No requiere ningún paso adicional para abrirlo.

Cada marcador se muestra como un botón etiquetado con la frecuencia almacenada en MHz. Los colores de los botones reflejan el segmento del plan de banda correspondiente a esa frecuencia, lo que permite identificar de un vistazo a qué banda pertenece cada marcador. Los marcadores se guardan por número de serie del radio bajo la configuración `BandStack_<serial>`, de modo que cada radio conectado mantiene su propia lista independiente.

El panel es desplazable cuando la lista de marcadores supera el área visible. Una fila de tres botones en la parte inferior del panel controla la lista:

| Control | Función |
|---|---|
| Botones de marcador | Haga clic para recuperar la frecuencia almacenada en el panadapter activo. Haga clic derecho para abrir un menú contextual con la opción "Remove". El tooltip muestra la frecuencia completa en MHz, el modo y la antena de recepción. |
| `+` | Agrega un nuevo marcador en la frecuencia actual del slice activo. |
| `×` | Elimina todos los marcadores de la lista. |
| ⚙ (engranaje) | Abre el menú de opciones del band stack (véase más adelante). |

### Menú de opciones del band stack

Al hacer clic en el botón de engranaje se abre un menú con dos categorías de ajustes:

**Group by band** — Opción activable mediante casilla. Cuando está habilitada, los marcadores se ordenan en secciones de banda con un encabezado etiquetado para cada banda (por ejemplo, "40m", "20m"). Al hacer clic derecho sobre un encabezado de banda se ofrece la opción de eliminar todos los marcadores dentro del rango de frecuencias de esa banda. Cuando está deshabilitada, los marcadores aparecen en orden de inserción.

**Auto-expiry** — Define cuánto tiempo se conservan los marcadores antes de eliminarse automáticamente. Las opciones son:

| Opción | Retención |
|---|---|
| Off | Los marcadores nunca caducan automáticamente |
| 5 min | Se eliminan después de 5 minutos |
| 15 min | Se eliminan después de 15 minutos |
| 30 min | Se eliminan después de 30 minutos |
| 60 min | Se eliminan después de 60 minutos |

Solo una opción de caducidad automática puede estar activa a la vez.

## Temas relacionados

- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador guardado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias guardadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
