# Descripción general del Aetherial Parametric EQ (TX / RX)

El Aetherial Parametric EQ proporciona ecualización paramétrica del lado del cliente tanto para la ruta de audio de transmisión como para la de recepción. Úselo para moldear el audio del micrófono en TX o para adaptar el sonido del audio recibido antes de que llegue a sus altavoces o auriculares, sin modificar ningún procesamiento del lado del radio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión con un radio para configurar el EQ, pero sí se necesita una conexión para que la superposición del analizador FFT en vivo muestre audio real.
- Las fichas (applets) del EQ permanecen ocultas hasta que la etapa de EQ correspondiente se habilite desde el widget CHAIN o el editor flotante. Si no ve "Aetherial TX EQ" o "Aetherial RX EQ" en el contenedor principal Aetherial Audio (TXDSP), habilite primero la etapa de EQ.

## Cómo funciona

AetherSDR instancia dos fichas de EQ independientes dentro del contenedor principal Aetherial Audio (TXDSP):

- **Aetherial TX EQ** — procesa el audio únicamente en la ruta de transmisión.
- **Aetherial RX EQ** — procesa el audio únicamente en la ruta de recepción.

Cada ficha está fija a su ruta. No existe un selector RX/TX dentro de la ficha. La ficha muestra una vista compacta de la curva de respuesta de EQ sumada y una superposición del analizador FFT en vivo para esa ruta. Sobre el analizador en vivo se dibuja una traza de retención de picos (peak-hold) que muestra el nivel máximo observado por frecuencia desde el último reinicio; la traza decae aproximadamente 10 dB/seg durante la operación normal. La edición —agregar, eliminar y ajustar bandas— ocurre en una ventana flotante separada llamada editor **Aetherial Parametric EQ**, que se abre desde el widget CHAIN. La barra de título del editor muestra "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX" según el lado desde el que se abrió. Se reutiliza una única instancia compartida del editor para ambos lados; el título cambia al cambiar de lado.

### Ficha del applet

Cada ficha contiene un área de control:

| Elemento | Descripción |
|---|---|
| Área del analizador / curva | Vista de al menos 80 px de alto que muestra la curva de respuesta de EQ sumada para todas las bandas habilitadas en esa ruta, con una superposición del analizador FFT en vivo y una traza de retención de picos. Esta área es solo de visualización en la ficha del applet. |

La **curva de EQ sumada** muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas. Cuando ninguna banda tiene realce ni corte, la curva es plana; se atenúa a gris cuando la etapa de EQ está en bypass. La **superposición del analizador en vivo** muestra la FFT en tiempo real del audio que pasa por esa ruta como un relleno de degradado cian; está inactiva cuando no hay audio activo y en funcionamiento cuando hay audio presente. La **traza de retención de picos** es una línea blanca suave que registra la energía máxima observada por frecuencia, lo que ayuda a identificar resonancias y picos molestos durante el ajuste. La traza decae aproximadamente 10 dB/seg entre actualizaciones. Puede congelarse desde el editor flotante mediante el botón Peak Hold.

### Editor flotante

Al hacer doble clic en la etapa de EQ en el widget CHAIN se abre el editor flotante para ese lado. El editor proporciona:

| Control | Descripción |
|---|---|
| Área del analizador / curva (canvas) | Canvas interactivo donde se arrastran los manejadores de banda para establecer frecuencia y ganancia. Arrastre los manejadores de pico/shelf para ajustar frecuencia y ganancia. Arrastre los manejadores HP/LP para ajustar frecuencia y Q. Mantenga presionada la tecla Shift mientras arrastra para ajustar Q en cualquier tipo de banda. Haga clic en un ícono de banda para recorrer los tipos de filtro. La traza de retención de picos también es visible aquí y refleja el estado congelado/decayendo establecido por el botón Peak Hold. |
| Peak Hold | Botón seleccionable en la franja de encabezado del editor. Cuando está activado, la traza de retención de picos por bin del analizador deja de decaer: el nivel máximo observado de cada frecuencia se mantiene hasta que se desactiva el botón. El botón muestra un fondo ámbar cuando está activado. Desactívelo para reanudar el decaimiento normal de aproximadamente 10 dB/seg. |
| Filter family | Cuadro combinado en la franja de encabezado del editor. Selecciona la familia de filtros aplicada al cálculo de la cascada HP/LP. Opciones: Butterworth (banda de paso máximamente plana), Chebyshev (transición más pronunciada, 1 dB de rizo en banda de paso), Bessel (fase lineal, caída más suave), Elliptic (transición más pronunciada, rizo en ambas bandas). Predeterminado: Butterworth. Los shelves y picos usan su topología nativa de segundo orden independientemente de este ajuste. Se persiste de forma independiente por ruta: `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. |
| Reset | Botón de acción en la franja de encabezado del editor. Restaura todas las bandas a sus valores predeterminados, restablece el número de bandas predeterminado de 10 y reinicia la familia de filtros a Butterworth. Se guarda de inmediato. Información emergente: "Reset all bands to default values". |
| Output Fader | Fader vertical combinado con medidor de nivel en el borde derecho del editor flotante. Arrastre para establecer la ganancia maestra post-EQ; la rueda del ratón ajusta en pasos de 0,5 dB; doble clic restablece a 0 dB. Rango: -36 a +12 dB. La barra de nivel detrás del manejador muestra el pico post-EQ suavizado en tiempo real con el mismo degradado verde-ámbar-rojo que el medidor de nivel Tube. Se encuentra únicamente en el editor flotante, no en la ficha del applet acoplada. |

El bypass se gestiona desde el widget CHAIN, no desde dentro del editor. Consulte [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).

### Ajustes persistidos

| Clave de ajuste | Qué almacena | Notas |
|---|---|---|
| `ClientEqRxEnabled` | Si la etapa de EQ de RX está habilitada. | |
| `ClientEqTxEnabled` | Si la etapa de EQ de TX está habilitada. | |
| `ClientEqRxBands` | Parámetros de banda para el EQ de RX. | |
| `ClientEqTxBands` | Parámetros de banda para el EQ de TX. | |
| `ClientEqTxFilterFamily` | Selección de familia de filtros para el EQ de TX. | Se persiste por ruta junto con `ClientEqRxFilterFamily`. |
| `ClientEqRxFilterFamily` | Selección de familia de filtros para el EQ de RX. | Se persiste por ruta junto con `ClientEqTxFilterFamily`. |
| `ClientEqTxMasterGain` | Ganancia maestra de salida post-EQ para el EQ de TX (-36 a +12 dB). | Información emergente en el Output Fader: "Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB." Predeterminado: 0 dB. |
| `ClientEqRxMasterGain` | Ganancia maestra de salida post-EQ para el EQ de RX (-36 a +12 dB). | Información emergente en el Output Fader: "Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB." Predeterminado: 0 dB. |

## Consejos

- Las fichas del applet están ocultas de forma predeterminada. Si desea una referencia visual persistente de su curva de EQ durante la operación, habilite la etapa de EQ desde el widget CHAIN para que la ficha quede visible en el contenedor Aetherial Audio (TXDSP).
- El editor flotante es compartido entre TX y RX. Abrirlo desde la ficha de la cadena TX y luego abrirlo desde la ficha de la cadena RX cambia el editor al lado RX; sus ajustes de TX no se ven afectados.
- Use Peak Hold para congelar la traza del analizador mientras ajusta una banda. Las resonancias que aparecen solo brevemente son fáciles de detectar porque la traza no decae mientras el botón está activado. Desactive Peak Hold cuando haya terminado para reanudar el decaimiento normal.
- Haga clic en Reset para devolver el EQ a un estado conocido antes de construir un nuevo preajuste desde cero. El reinicio se guarda de inmediato y se conserva tras un reinicio del programa.
- Haga clic derecho en la barra de título del subcontenedor "Aetherial TX EQ" o "Aetherial RX EQ" para flotarlo, extraerlo u ocultarlo.

## Relacionados

- [Inspeccionar la curva del EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva del EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Verificar que la curva sumada coincida con el objetivo previsto](verify-the-summed-curve-matches-your-mental-target.md)
