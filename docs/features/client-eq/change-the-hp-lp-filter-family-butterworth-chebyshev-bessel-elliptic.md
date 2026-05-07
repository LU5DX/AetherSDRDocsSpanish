# Cambiar la familia de filtros HP/LP (Butterworth, Chebyshev, Bessel, Elíptico)

El selector **Filter family** controla la función matemática utilizada para las bandas de filtro HP y LP en el ecualizador del cliente. Cambiarlo permite compensar la pendiente de atenuación, la planitud de la banda pasante y la linealidad de fase para adaptarse a sus objetivos de audio.

## Antes de comenzar

- La etapa de EQ para la ruta que desea cambiar (TX o RX) debe estar habilitada. Consulte [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md).
- El editor flotante debe estar abierto. El selector **Filter family** solo está disponible en el editor sin marco, no en el mosaico del applet acoplado. Consulte [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).
- Al menos una banda debe estar configurada como tipo de filtro HP o LP. La configuración no tiene efecto audible si solo hay bandas de pico (peak) y estantería (shelf).

## Pasos

1. Abra el editor flotante para la ruta que desea cambiar: haga doble clic en la etapa EQ en el widget CHAIN del lado TX o RX. El título de la ventana mostrará "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice el cuadro combinado **Filter family** en la barra de encabezado del editor, a la derecha del botón **Peak Hold**.
3. Haga clic en el cuadro combinado y seleccione una de las cuatro opciones: **Butterworth**, **Chebyshev**, **Bessel** o **Elliptic**.
4. La curva del EQ en el lienzo se actualiza inmediatamente. Si hay bandas HP o LP presentes, sus pendientes se redibujarán para reflejar la nueva familia.

La selección se guarda automáticamente. Se almacena por separado para cada ruta: `ClientEqTxFilterFamily` para el editor TX y `ClientEqRxFilterFamily` para el editor RX.

## Qué hace cada control

| Control                             | Predeterminado                                                                                                                                                                                                                                                                                                                                                                    | Valores válidos                                                                                                                                                                                                                   |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Filter family** (editor TX)       | Butterworth                                                                                                                                                                                                                                                                                                                                                                      | Butterworth, Chebyshev, Bessel, Elliptic                                                                                                                                                                                          |
| **Filter family** (editor RX)       | Butterworth                                                                                                                                                                                                                                                                                                                                                                      | Butterworth, Chebyshev, Bessel, Elliptic                                                                                                                                                                                          |
| Smoothing                           | Aplica un promedio de potencia de fracción de octava a la traza del analizador para su visualización; no afecta el cálculo del EQ. Fracción más baja = trazo más suave (1/3 es el más suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX.                                                                                                    | Tooltip: 'Fractional-octave smoothing applied to the analyzer trace. Lower fraction = smoother (1/3 = most, 1/96 = off). Affects display only — EQ math is unchanged.' Ubicado en la barra de encabezado del editor (solo editor flotante). |
| Fila de iconos de tipo de filtro    | Una fila de 8 iconos personalizados (uno por espacio de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana de pico, rampa de estantería, pendiente HP/LP) en el color de la paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro para esa banda; al hacer clic también se selecciona la banda, resaltando su control en el lienzo y su columna en la fila de parámetros. | Ubicada solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está desviada (bypassed). Implementado por ClientEqIconRow.                                                                     |
| Fila de texto de parámetros         | Una fila de 8 columnas de texto (una por espacio de banda) debajo del lienzo que muestra los valores de Frecuencia, Ganancia y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. Las etiquetas están alineadas en la parte inferior de cada columna y el fondo de la fila es transparente para que no se superponga a la tira de bandas superior. | Ubicada solo en el editor flotante. Implementado por ClientEqParamRow.                                                                                                                                                            |
| Líneas guía de corte del filtro (TX / RX) | Líneas amarillas discontinuas verticales superpuestas en el lienzo en los cortes de filtro bajo/alto actuales de la radio (mosaico TX) o en los bordes de la banda pasante de RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real. | Arrastrar las guías de corte TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía. |

**Butterworth** — banda pasante máxima plana; sin rizado en la banda pasante ni en la banda suprimida. La opción predeterminada para uso general.

**Chebyshev** — transición más pronunciada que Butterworth, con 1 dB de rizado en la banda pasante.

**Bessel** — respuesta de fase lineal y la pendiente más suave de las cuatro familias. Preserva la forma de las señales transitorias.

**Elliptic** — la transición más pronunciada de todas las opciones, con rizado tanto en la banda pasante como en la banda suprimida.

Estas opciones se aplican solo a los tipos de banda HP y LP. Las bandas de pico (peak) y estantería (shelf) usan su propia topología fija de segundo orden independientemente de esta configuración.

## Consejos

- Si no tiene bandas HP o LP en el EQ actual, cambiar la familia de filtros no cambia nada audible. Agregue primero una banda HP o LP a través de la fila de iconos de tipo de filtro.
- La familia de filtros se configura de forma independiente para TX y RX. Cambiarla en el editor TX no afecta al editor RX, y viceversa.
- Hacer clic en **Reset** en la barra de encabezado del editor restablece la familia de filtros a **Butterworth** junto con todos los parámetros de las bandas.

## Solución de problemas

- **El cuadro combinado Filter family no es visible** — El cuadro combinado solo está presente en el editor flotante, no en el mosaico del applet acoplado. Haga doble clic en la etapa EQ en el widget CHAIN para abrir el editor.
- **Cambiar la familia no tiene efecto en la curva** — No hay bandas HP o LP activas. La configuración solo afecta la matemática en cascada de HP y LP. Verifique el tipo de cada banda usando la fila de iconos de tipo de filtro.
- **La fila de texto de parámetros parece superponerse a la tira de bandas** — Este fue un problema de visualización en versiones anteriores a v0.9.7 donde el fondo oscuro de la fila se desbordaba hacia arriba sobre el lienzo. Actualice a v0.9.7 o posterior; la fila ahora es transparente y sus etiquetas están alineadas en la parte inferior de cada columna.

## Relacionado

- [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Change a band's filter type by clicking its icon in the icon row](change-a-band-s-filter-type-by-clicking-its-icon-in-the-icon-row.md)
- [Reset all EQ bands to the default 10-band template](reset-all-eq-bands-to-the-default-10-band-template.md)
- [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md)
- [Aetherial Parametric EQ (TX / RX) overview](overview.md)
