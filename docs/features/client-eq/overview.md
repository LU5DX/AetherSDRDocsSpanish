# Descripción general del Ecualizador Paramétrico Aetherial (TX / RX)

El Ecualizador Paramétrico Aetherial proporciona ecualización paramétrica del lado del cliente para las rutas de audio de transmisión y recepción. Úselo para dar forma al audio del micrófono en TX, o para adaptar el sonido del audio recibido antes de que llegue a sus parlantes o auriculares, sin modificar ningún procesamiento del lado del radio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar el EQ, pero sí es necesaria para que la superposición del analizador FFT en vivo muestre audio real.
- Los tiles del applet de EQ están ocultos hasta que la etapa de EQ correspondiente se habilite mediante el widget CHAIN o el editor flotante. Si no ve "Aetherial TX EQ" o "Aetherial RX EQ" en el contenedor principal Aetherial Audio (TXDSP), habilite primero la etapa de EQ.

## Cómo funciona

AetherSDR instancia dos tiles de EQ independientes dentro del contenedor principal Aetherial Audio (TXDSP):

- **Aetherial TX EQ** — procesa el audio únicamente en la ruta de transmisión.
- **Aetherial RX EQ** — procesa el audio únicamente en la ruta de recepción.

Cada tile está fijo a su ruta. No existe un selector RX/TX dentro del tile. El tile muestra una vista compacta de la curva de respuesta de EQ sumada y una superposición del analizador FFT en vivo para esa ruta. La edición —agregar, eliminar y ajustar bandas— ocurre en una ventana flotante separada llamada el editor **Aetherial Parametric EQ**, que se abre desde el widget CHAIN. La barra de título del editor muestra "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX" según el lado desde el que lo haya abierto. Se reutiliza una única instancia compartida del editor para ambos lados; el título cambia al cambiar de lado.

### Tile del applet

Cada tile contiene un área de control:

| Elemento | Descripción |
|---|---|
| Área del analizador / curva | Vista de 110 px de alto que muestra la curva de respuesta de EQ sumada para todas las bandas habilitadas en esa ruta, con una superposición del analizador FFT en vivo. Esta área es solo de visualización en el tile del applet. |

La **respuesta de EQ sumada** muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas. Cuando ninguna banda tiene refuerzo ni corte, la curva es plana. La **superposición del analizador en vivo** muestra la FFT en tiempo real del audio que pasa por esa ruta; permanece inactiva cuando no hay audio y se activa cuando hay audio presente.

### Editor flotante

Al hacer doble clic en la etapa de EQ en el widget CHAIN se abre el editor flotante para ese lado. El editor proporciona:

| Control | Descripción |
|---|---|
| Área del analizador / curva (lienzo) | Lienzo interactivo donde se arrastran los manejadores de banda para establecer la frecuencia y la ganancia. Arrastre los manejadores de pico/shelving para ajustar frecuencia y ganancia. Arrastre los manejadores HP/LP para ajustar frecuencia y Q. Mantenga presionado Shift mientras arrastra para ajustar Q en cualquier tipo de banda. Haga clic en el ícono de una banda para ciclar entre los tipos de filtro. |
| Peak Hold | Botón seleccionable. Cuando está activado, la traza de pico por bin del analizador deja de decaer, de modo que el nivel más alto visto en cada frecuencia permanece visible. Desactívelo para reanudar el decaimiento normal. |
| Selector de familia de filtros | Selecciona la familia de filtros aplicada a la matemática de cascada HP/LP. Opciones: Butterworth (banda de paso máximamente plana), Chebyshev (transición más pronunciada, rizado de 1 dB en la banda de paso), Bessel (fase lineal, rolloff más suave), Elliptic (transición más pronunciada, rizado en ambas bandas). Valor predeterminado: Butterworth. Los shelves y picos utilizan su topología nativa de segundo orden independientemente de esta configuración. |
| Reset | Devuelve todas las bandas a sus valores predeterminados, restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Se guarda de inmediato. |
| Fader de salida | Medidor vertical, deslizador y lectura en dB en el lado derecho del editor. Controla el nivel de salida de la etapa de EQ. |

El bypass se gestiona desde el widget CHAIN, no desde el interior del editor. Consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).

### Configuraciones guardadas

| Clave de configuración | Qué almacena |
|---|---|
| `ClientEqRxEnabled` | Si la etapa de EQ de RX está habilitada. |
| `ClientEqTxEnabled` | Si la etapa de EQ de TX está habilitada. |
| `ClientEqRxBands` | Parámetros de banda para el EQ de RX. |
| `ClientEqTxBands` | Parámetros de banda para el EQ de TX. |

## Consejos

- Los tiles del applet están ocultos de forma predeterminada. Si desea una referencia visual persistente de su curva de EQ durante la operación, habilite la etapa de EQ mediante el widget CHAIN para que el tile quede visible en el contenedor Aetherial Audio (TXDSP).
- El editor flotante es compartido entre TX y RX. Abrirlo desde el tile de la cadena TX y luego abrirlo desde el tile de la cadena RX cambia el editor al lado RX; su configuración de TX no se ve afectada.
- Haga clic derecho en la barra de título del subcontenedor "Aetherial TX EQ" o "Aetherial RX EQ" para flotar, extraer u ocultar el tile.

## Relacionado

- [Inspeccionar la curva de EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Abrir el editor sin marco para agregar, eliminar y ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
