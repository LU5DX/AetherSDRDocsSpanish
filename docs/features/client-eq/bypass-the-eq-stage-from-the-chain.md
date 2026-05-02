# Omitir la etapa de EQ de la cadena

Esta página explica cómo omitir el EQ paramétrico del lado del cliente para la ruta de audio TX o RX. Al omitirlo, se elimina el EQ de la cadena de señal sin borrar la configuración de bandas.

## Antes de comenzar

- AetherSDR debe estar abierto. No se requiere conexión a una radio para omitir el EQ.
- La etapa de EQ ya debe estar presente en el widget CHAIN para la ruta que desea omitir (TX o RX).

## Pasos

1. Localice el widget CHAIN para la ruta que desea omitir: ya sea la cadena TX o la cadena RX.
2. Haga clic una sola vez sobre la etapa de EQ en el widget CHAIN de esa ruta.

La etapa de EQ queda omitida para esa ruta. La configuración `ClientEqTxEnabled` o `ClientEqRxEnabled` se actualiza de inmediato y se conserva entre reinicios.

Para volver a activar el EQ, haga clic una sola vez sobre la etapa de EQ en el widget CHAIN nuevamente.

## Qué hace cada control

| Control | Ruta | Clave persistida |
|---|---|---|
| Etapa de EQ (cadena TX) | TX | `ClientEqTxEnabled` |
| Etapa de EQ (cadena RX) | RX | `ClientEqRxEnabled` |
| Output Fader | Fader vertical combinado con medidor de nivel en el borde derecho del editor flotante. Arrástrelo para ajustar la ganancia maestra post-EQ; la rueda de desplazamiento ajusta en pasos de 0.5 dB; doble clic restablece a 0 dB. La barra de nivel detrás del control muestra el pico post-EQ suavizado en tiempo real con el mismo degradado verde-ámbar-rojo que el medidor de nivel Tube. | Persistido por separado según la ruta: `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. Información emergente: 'Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB.' El rango de ganancia es lineal de 0.0 a ~4.0; las etiquetas de la escala van de -40 a 0 dB. Se encuentra únicamente en el editor flotante, no en el panel acoplado del applet. |
| Peak Hold | Se encuentra únicamente en la barra de encabezado del editor flotante. Cuando está marcado, la traza de pico máximo por bin en el analizador deja de decaer: el nivel más alto observado en cada frecuencia se retiene hasta que se desactiva el botón. El fondo del botón se vuelve ámbar cuando está marcado. | Ninguna (no se persiste). |
| Familia de filtros (Filter family) | Se encuentra en la barra de encabezado del editor flotante. Selecciona la matemática de la cascada HP/LP: Butterworth (banda de paso maximalmente plana), Chebyshev (caída más pronunciada con rizado de 1 dB en la banda de paso), Bessel (fase lineal / caída más suave) o Elliptic (transición más pronunciada con rizado en ambas bandas). Se aplica únicamente a los tipos de filtro HP y LP; las bandas pico y de estante utilizan su propia topología fija de segundo orden independientemente. Valor predeterminado: Butterworth. | Persistido por separado según la ruta: `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. |
| Reset | Se encuentra en la barra de encabezado del editor flotante. Restablece todas las bandas a la plantilla predeterminada de 10 bandas, restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Guarda de inmediato. Información emergente: 'Reset all bands to default values'. | Afecta a `ClientEqTxBands` / `ClientEqRxBands` y `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. |
| Smoothing | Aplica promediado de potencia por octava fraccionaria a la traza del analizador para visualización; no afecta el cálculo del EQ. Fracción menor = más suavizado (1/3 es el más suavizado; 1/96 equivale a desactivado). Compartido entre los editores TX y RX. El suavizado se aplica después de la actualización de pico máximo en cada fotograma, por lo que tanto la traza en vivo del analizador como la traza de pico máximo se suavizan para su visualización, mientras que la detección de pico opera con precisión de muestra. | `ClientEqSmoothingFraction`. Información emergente: 'Fractional-octave smoothing applied to the analyzer trace. Lower fraction = smoother (1/3 = most, 1/96 = off). Affects display only — EQ math is unchanged.' Se encuentra en la barra de encabezado del editor (únicamente en el editor flotante). |
| Fila de iconos de tipo de filtro (Filter-type icon row) | Fila de 8 iconos personalizados (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana pico, rampa de estante, pendiente HP/LP) en el color de paleta de su banda. Haga clic en un icono para ciclar por los tipos de filtro de esa banda; al hacer clic también se selecciona la banda, resaltando su control en el lienzo y su columna en la fila de parámetros. | Se encuentra únicamente en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está omitida. Implementado por ClientEqIconRow. |
| Fila de parámetros de texto (Parameter text row) | Fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo, que muestra los valores de Freq, Gain y Q de cada banda. Los valores se actualizan en tiempo real durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. | Se encuentra únicamente en el editor flotante. Implementado por ClientEqParamRow. |
| Líneas guía de frecuencia de corte del filtro (TX / RX) | Líneas verticales amarillas discontinuas superpuestas en el lienzo en las frecuencias de corte bajas/altas del filtro TX actual de la radio (panel TX) o en los bordes de la banda de paso RX (panel RX). Al acercar el cursor a una línea, este cambia a una flecha de redimensionado horizontal. Arrastrar una línea en el editor mueve la frecuencia de corte correspondiente de la radio en tiempo real. Los paneles de applet acoplados también muestran estas líneas guía: el panel TX recibe las frecuencias de corte mediante `setTxFilterCutoffs`, y el panel RX las recibe mediante `setRxFilterCutoffs`. | Arrastrar las guías de corte TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 en un borde para suprimir esa guía. |

Los datos de banda se almacenan por separado en `ClientEqTxBands` y `ClientEqRxBands` y no se ven afectados por la omisión.

## Consejos

- El estado de omisión es por ruta. Omitir el EQ de TX no afecta el EQ de RX, y viceversa.
- Los paneles de applet "Aetherial TX EQ" y "Aetherial RX EQ" se ocultan cuando su etapa de EQ correspondiente no está habilitada. Si un panel desaparece después de omitir el EQ, este es el comportamiento esperado.
- El editor flotante ("Aetherial Parametric EQ — TX" o "— RX") puede abrirse mediante doble clic en la etapa del widget CHAIN incluso cuando está omitido, de modo que puede continuar editando bandas sin volver a activar el EQ.
- La traza de pico máximo en el analizador decae a aproximadamente 10 dB/seg durante la operación normal. La detección de pico siempre opera sobre bins sin suavizar, por lo que es precisa a nivel de muestra; el suavizado se aplica por separado únicamente para la visualización. Active **Peak Hold** en el editor flotante para congelar la traza en su nivel más alto observado por bin de frecuencia, lo cual es útil para identificar resonancias al ajustar las bandas.
- Hacer clic en **Reset** en el editor flotante es permanente y tiene efecto de inmediato. No hay función de deshacer. El restablecimiento también devuelve la familia de filtros a Butterworth para esa ruta.

## Relacionados

- [Descripción general del Aetherial Parametric EQ (TX / RX)](overview.md)
- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier ruta](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspeccionar la curva del EQ TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva del EQ RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
