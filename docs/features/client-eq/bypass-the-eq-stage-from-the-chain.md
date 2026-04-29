# Omitir la etapa de EQ de la cadena

Esta página explica cómo omitir el ecualizador paramétrico del lado del cliente para la ruta de audio TX o RX. Al omitir la etapa, el EQ se elimina de la cadena de señal sin borrar la configuración de banda.

## Antes de comenzar

- AetherSDR debe estar abierto. No se requiere conexión con la radio para omitir el EQ.
- La etapa de EQ ya debe estar presente en el widget CHAIN para la ruta que desea omitir (TX o RX).

## Pasos

1. Localice el widget CHAIN para la ruta que desea omitir: la cadena TX o la cadena RX.
2. Haga clic una vez sobre la etapa de EQ en el widget CHAIN para esa ruta.

La etapa de EQ queda omitida para esa ruta. El ajuste `ClientEqTxEnabled` o `ClientEqRxEnabled` se actualiza de inmediato y se conserva entre reinicios.

Para reactivar el EQ, haga clic una vez sobre la etapa de EQ en el widget CHAIN nuevamente.

## Qué hace cada control

| Control | Ruta | Clave persistida |
|---|---|---|
| Etapa de EQ (cadena TX) | TX | `ClientEqTxEnabled` |
| Etapa de EQ (cadena RX) | RX | `ClientEqRxEnabled` |
| Output Fader | Fader combinado vertical con medidor de nivel en el borde derecho del editor flotante. Arrastre para ajustar la ganancia maestra post-EQ; la rueda del ratón ajusta en pasos de 0.5 dB; doble clic restablece a 0 dB. La barra de nivel detrás del control muestra el pico post-EQ suavizado en tiempo real con el mismo gradiente verde-ámbar-rojo que el medidor de nivel Tube. | Persistido por separado para cada ruta: `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. Descripción emergente: 'Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB.' El rango de ganancia es lineal de 0.0 a ~4.0; las etiquetas de la escala van de -40 a 0 dB. Se encuentra solo en el editor flotante, no en el tile del applet acoplado. |
| Peak Hold | Se encuentra únicamente en la barra de encabezado del editor flotante. Cuando está marcado, la traza de retención de pico por bin en el analizador deja de decaer: el nivel máximo observado en cada frecuencia se mantiene hasta que el botón se desactiva. El fondo del botón se vuelve ámbar cuando está activado. | Ninguna (no se persiste). |
| Familia de filtros | Se encuentra en la barra de encabezado del editor flotante. Selecciona las matemáticas de la cascada HP/LP: Butterworth (banda de paso maximalmente plana), Chebyshev (corte más pronunciado con rizado de 1 dB en la banda de paso), Bessel (fase lineal / corte más suave) o Elliptic (transición más pronunciada con rizado en ambas bandas). Se aplica únicamente a los tipos de filtro HP y LP; las bandas de pico y de estantería utilizan su propia topología fija de segundo orden independientemente. Predeterminado: Butterworth. | Persistido por separado para cada ruta: `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. |
| Reset | Se encuentra en la barra de encabezado del editor flotante. Restablece todas las bandas a la plantilla predeterminada de 10 bandas, restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Se guarda de inmediato. Descripción emergente: 'Reset all bands to default values'. | Afecta a `ClientEqTxBands` / `ClientEqRxBands` y `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. |

Los datos de banda se almacenan por separado en `ClientEqTxBands` y `ClientEqRxBands` y no se ven afectados al omitir el EQ.

## Consejos

- El estado de omisión es por ruta. Omitir el EQ de TX no afecta el EQ de RX, ni viceversa.
- Los tiles de applet "Aetherial TX EQ" y "Aetherial RX EQ" se ocultan cuando su etapa de EQ correspondiente no está habilitada. Si un tile desaparece tras omitir el EQ, este es el comportamiento esperado.
- El editor flotante ("Aetherial Parametric EQ — TX" o "— RX") puede abrirse igualmente con doble clic sobre la etapa en el widget CHAIN, incluso cuando el EQ está omitido, de modo que puede continuar editando bandas sin reactivarlo.
- La traza de retención de pico en el analizador decae aproximadamente a 10 dB/s durante el funcionamiento normal. Active **Peak Hold** en el editor flotante para congelar la traza en el nivel máximo observado por bin de frecuencia: resulta útil para identificar resonancias mientras se ajustan las bandas.
- Hacer clic en **Reset** en el editor flotante es permanente y tiene efecto de inmediato. No existe función de deshacer. El restablecimiento también devuelve la familia de filtros a Butterworth para esa ruta.

## Relacionado

- [Descripción general del Aetherial Parametric EQ (TX / RX)](overview.md)
- [Abrir el editor sin marco para añadir, eliminar o ajustar bandas en cualquiera de los lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspeccionar la curva del EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva del EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
