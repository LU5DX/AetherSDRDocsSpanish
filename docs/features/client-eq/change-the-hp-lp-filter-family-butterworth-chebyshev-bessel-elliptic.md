# Cambiar la familia de filtros HP/LP (Butterworth, Chebyshev, Bessel, Elliptic)

El selector **Filter family** controla las matemáticas utilizadas para las bandas de filtro HP y LP en el ecualizador del cliente. Cambiarlo permite equilibrar la pendiente de atenuación, la planitud de la banda pasante y la linealidad de fase para adaptarse a sus objetivos de audio.

## Antes de comenzar

- La etapa de EQ para la ruta que desea cambiar (TX o RX) debe estar habilitada. Consulte [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md).
- El editor flotante debe estar abierto. El selector **Filter family** solo está disponible en el editor sin marco, no en el mosaico acoplado del applet. Consulte [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).
- Al menos una banda debe estar configurada como un tipo de filtro HP o LP. La configuración no tiene efecto audible si solo hay bandas de pico (peak) y estante (shelf).

## Pasos

1. Abra el editor flotante para la ruta que desea cambiar: haga doble clic en la etapa EQ en el widget CHAIN en el lado TX o RX. El título de la ventana mostrará "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice el cuadro combinado **Filter family** en la barra del encabezado del editor, a la derecha del botón **Peak Hold**.
3. Haga clic en el cuadro combinado y seleccione una de las cuatro opciones: **Butterworth**, **Chebyshev**, **Bessel** o **Elliptic**.
4. La curva del EQ en el lienzo se actualiza inmediatamente. Si hay bandas HP o LP presentes, sus pendientes se redibujarán para reflejar la nueva familia.

La selección se guarda automáticamente. Se almacena por separado para cada ruta: `ClientEqTxFilterFamily` para el editor TX y `ClientEqRxFilterFamily` para el editor RX.

## Qué hace cada control

| Control                              | Valor predeterminado                                                                                                                                                                                                                                                                                                                                                             | Valores válidos                                                                                                                                                                                                                    |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Filter family** (editor TX)        | Butterworth                                                                                                                                                                                                                                                                                                                                                                      | Butterworth, Chebyshev, Bessel, Elliptic                                                                                                                                                                                           |
| **Filter family** (editor RX)        | Butterworth                                                                                                                                                                                                                                                                                                                                                                      | Butterworth, Chebyshev, Bessel, Elliptic                                                                                                                                                                                           |
| Smoothing                            | Aplica un promediado de potencia de octava fraccionaria a la traza del analizador para su visualización; no afecta el cálculo del EQ. Fracción más baja = más suave (1/3 es el máximo suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX.                                                                                                      | Tooltip: 'Suavizado de octava fraccionaria aplicado a la traza del analizador. Fracción más baja = más suave (1/3 = máximo, 1/96 = desactivado). Afecta solo la visualización — el cálculo del EQ no cambia.' Ubicado en la barra del encabezado del editor (solo editor flotante). |
| Fila de iconos de tipo de filtro     | Una fila de 8 iconos personalizados (una por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana de pico, rampa de estante, pendiente HP/LP) en el color de la paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro para esa banda; al hacer clic también se selecciona la banda, resaltando su asa en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está desviada. Implementado por ClientEqIconRow.                                                                                  |
| Fila de texto de parámetros          | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores de Freq, Gain y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. Haga clic derecho en una columna para abrir un menú contextual para la entrada numérica de Freq, Gain o Q. | Ubicado solo en el editor flotante. Implementado por ClientEqParamRow.                                                                                                                                                             |
| Líneas guía de corte del filtro (TX / RX) | Líneas amarillas discontinuas verticales superpuestas en el lienzo en los límites de corte del filtro bajo/alto actuales de la radio (panel TX) o los bordes de la banda pasante de RX (panel RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de cambio de tamaño horizontal. Arrastrar una línea en el editor mueve el corte del filtro correspondiente de la radio en tiempo real. | Arrastrar las guías de corte TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía.              |
| Output Fader                         | Mezclador de volumen vertical combinado + medidor de nivel en el borde derecho del editor flotante. Arrastre para establecer la ganancia maestra posterior al EQ; la rueda del ratón ajusta en pasos de 0.5 dB; doble clic restablece a 0 dB. La barra de nivel detrás del asa muestra el pico posterior al EQ suavizado en tiempo real con el mismo gradiente verde-ámbar-rojo que el medidor de nivel del Tube. Haga clic en la lectura de dB en la parte inferior para ingresar un valor directamente mediante el teclado.                               | -36.0 a +12.0 dB. Se conserva por separado por ruta: ClientEqTxMasterGain / ClientEqRxMasterGain. Tooltip: 'Ganancia de salida (dB). Arrastre para ajustar, rueda para paso fino, doble clic para restablecer a 0 dB.' Ubicado solo en el editor flotante. |

**Butterworth** — banda pasante máximamente plana; sin ondulación en la banda pasante ni en la banda de rechazo. La opción predeterminada para uso general.

**Chebyshev** — banda de transición más pronunciada que Butterworth, con 1 dB de ondulación en la banda pasante.

**Bessel** — respuesta de fase lineal y la pendiente más suave de las cuatro familias. Preserva la forma de las señales transitorias.

**Elliptic** — transición más pronunciada de las cuatro opciones, con ondulación tanto en la banda pasante como en la banda de rechazo.

Estas opciones se aplican solo a los tipos de banda HP y LP. Las bandas de pico y estante utilizan su propia topología fija de segundo orden independientemente de esta configuración.

## Consejos

- Si no tiene bandas HP o LP en el EQ actual, cambiar la familia de filtros no altera nada audible. Agregue primero una banda HP o LP a través de la fila de iconos de tipo de filtro.
- La familia de filtros se establece de forma independiente para TX y RX. Cambiarla en el editor TX no afecta al editor RX, y viceversa.
- Al hacer clic en **Reset** en la barra del encabezado del editor, se restablece la familia de filtros a **Butterworth** junto con todos los parámetros de las bandas.
- Para ingresar valores exactos de frecuencia, ganancia o Q para una banda, haga clic derecho en su columna en la fila de texto de parámetros y elija el parámetro que desea editar en el menú contextual. Después de escribir un valor y presionar Enter, el cambio se guarda y la curva del EQ se redibuja inmediatamente.

## Solución de problemas

- **El cuadro combinado Filter family no está visible** — El cuadro combinado solo está presente en el editor flotante, no en el mosaico acoplado del applet. Haga doble clic en la etapa EQ en el widget CHAIN para abrir el editor.
- **Cambiar la familia no tiene efecto en la curva** — No hay bandas HP o LP activas. La configuración solo afecta el cálculo en cascada de HP y LP. Verifique el tipo de cada banda usando la fila de iconos de tipo de filtro.
- **La fila de texto de parámetros parece superponerse a la tira del plan de bandas** — Este fue un problema de visualización en versiones anteriores a v0.9.7 donde el fondo oscuro de la fila se extendía hacia arriba sobre el lienzo. Actualice a v0.9.7 o posterior; la fila ahora es transparente y sus etiquetas están alineadas en la parte inferior de cada columna.
- **La lectura de dB del Output Fader no acepta valores escritos** — Haga clic en la lectura en la parte inferior del fader para enfocarla, luego escriba un valor (ej. "-6.5") y presione Enter. Presione Escape para cancelar la edición y volver al valor anterior.

## Relacionados

- [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Change a band's filter type by clicking its icon in the icon row](change-a-band-s-filter-type-by-clicking-its-icon-in-the-icon-row.md)
- [Enter exact band parameters via the parameter text row right-click menu](enter-exact-band-parameters-via-the-parameter-text-row-right-click-menu.md)
- [Reset all EQ bands to the default 10-band template](reset-all-eq-bands-to-the-default-10-band-template.md)
- [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md)
- [Set the output fader value precisely by typing](set-the-output-fader-value-precisely-by-typing.md)
- [Aetherial Parametric EQ (TX / RX) overview](overview.md)
