# Descripción general del ecualizador paramétrico Aetherial (TX / RX)

El ecualizador paramétrico Aetherial proporciona ecualización paramétrica del lado del cliente para las rutas de audio de transmisión y recepción. Úselo para dar forma al audio del micrófono TX o para adaptar el sonido del audio recibido antes de que llegue a sus altavoces o auriculares, sin modificar ningún procesamiento del lado del radio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un radio para configurar el ecualizador, pero sí se necesita una conexión para que la superposición del analizador FFT en tiempo real muestre audio real.
- Los mosaicos del applet de EQ están ocultos hasta que la etapa de EQ correspondiente se habilite mediante el widget CHAIN o el editor flotante. Si no ve "Aetherial TX EQ" o "Aetherial RX EQ" en el contenedor principal Aetherial Audio (TXDSP), habilite primero la etapa de EQ.

## Cómo funciona

AetherSDR instancia dos mosaicos de EQ separados dentro del contenedor principal Aetherial Audio (TXDSP):

- **Aetherial TX EQ** — procesa el audio únicamente en la ruta de transmisión.
- **Aetherial RX EQ** — procesa el audio únicamente en la ruta de recepción.

Cada mosaico está fijo a su ruta. No existe un selector RX/TX dentro del mosaico. El mosaico muestra una vista compacta de la curva de respuesta de EQ sumada y una superposición del analizador FFT en tiempo real para esa ruta. Se traza una curva de retención de pico sobre el analizador en vivo, que muestra el nivel máximo por frecuencia observado desde el último reinicio; la curva decae aproximadamente a 10 dB/seg durante el funcionamiento normal. La curva de retención de pico opera sobre los contenedores FFT brutos, por lo que la detección de pico es precisa a nivel de muestra; el suavizado de visualización (cuando está habilitado) se aplica por separado y no afecta los datos de retención de pico. La edición — agregar, eliminar y ajustar bandas — ocurre en una ventana flotante separada llamada editor **Aetherial Parametric EQ**, que se abre desde el widget CHAIN. La barra de título del editor muestra "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX" según el lado desde el que se haya abierto. Se reutiliza una única instancia de editor compartida para ambos lados; el título cambia al cambiar de lado.

### Mosaico del applet

Cada mosaico contiene un área de control:

| Elemento | Descripción |
|---|---|
| Área del analizador / curva | Vista de mínimo 110 px de alto que muestra la curva de respuesta de EQ sumada de todas las bandas habilitadas en esa ruta, con una superposición del analizador FFT en tiempo real y una curva de retención de pico. Las líneas verticales discontinuas amarillas marcan los límites de corte de filtro TX bajo/alto del radio (mosaico TX) o los bordes de la banda de paso RX (mosaico RX). Esta área es solo de visualización en el mosaico del applet. |

La **respuesta de EQ sumada** muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas. Cuando ninguna banda tiene refuerzo ni corte, la curva es plana; se atenúa a gris cuando la etapa de EQ está en bypass. La **superposición del analizador en vivo** muestra la FFT en tiempo real del audio que pasa por esa ruta como un relleno degradado cian; está inactiva cuando no hay audio activo y en funcionamiento cuando hay audio presente. La **curva de retención de pico** es una línea suave de color blanco apagado que rastrea la energía máxima por frecuencia observada, ayudando a identificar resonancias y picos duros durante el ajuste. La curva decae aproximadamente a 10 dB/seg entre actualizaciones. Se puede congelar desde el editor flotante usando el botón Peak Hold. Las **líneas guía de corte de filtro** son líneas verticales discontinuas amarillas que marcan los límites de corte de filtro TX bajo/alto del radio (mosaico TX) o los bordes de la banda de paso RX (mosaico RX) directamente sobre el lienzo. Estas líneas son visibles en el mosaico del applet y son arrastrables en el editor flotante.

### Editor flotante

Hacer doble clic en la etapa de EQ en el widget CHAIN abre el editor flotante para ese lado. El editor proporciona:

| Control | Descripción | Notas |
|---|---|---|
| Área del analizador / curva (lienzo) | Lienzo interactivo donde se arrastran los manejadores de banda para establecer frecuencia y ganancia. Arrastre los manejadores de pico/shelf para ajustar frecuencia y ganancia. Arrastre los manejadores HP/LP para ajustar frecuencia y Q. Mantenga presionado Shift mientras arrastra para ajustar Q en cualquier tipo de banda. Haga clic en el ícono de una banda para recorrer los tipos de filtro. La curva de retención de pico también es visible aquí y refleja el estado congelado/decayente establecido por el botón Peak Hold. | |
| Peak Hold | Botón verificable en la tira de encabezado del editor. Cuando está marcado, la curva de retención de pico por contenedor del analizador deja de decaer — el nivel máximo observado de cada frecuencia se retiene hasta que se desactiva el botón. El botón muestra un fondo ámbar cuando está marcado. Desactívelo para reanudar el decaimiento normal a aproximadamente 10 dB/seg. | |
| Smoothing | Cuadro combinado en la tira de encabezado del editor. Aplica promediado de potencia por octava fraccionaria a la traza del analizador para su visualización — no afecta los cálculos del EQ. Opciones: Off (1/96), 1/24, 1/12, 1/6, 1/3. Fracción menor = más suavizado (1/3 es el máximo; 1/96 es efectivamente desactivado). Compartido entre los editores TX y RX. Almacenado como `ClientEqSmoothingFraction`. | Tooltip: "Fractional-octave smoothing applied to the analyzer trace. Lower fraction = smoother (1/3 = most, 1/96 = off). Affects display only — EQ math is unchanged." Ubicado en la tira de encabezado del editor (solo en el editor flotante). El suavizado se calcula después de la actualización de retención de pico en cada fotograma, por lo que tanto la traza en vivo como la traza de retención de pico se suavizan de forma independiente para su visualización. |
| Filter family | Cuadro combinado en la tira de encabezado del editor. Selecciona la familia de filtros aplicada a los cálculos en cascada HP/LP. Opciones: Butterworth (banda de paso máximamente plana), Chebyshev (transición más pronunciada, rizado de 1 dB en la banda de paso), Bessel (fase lineal, caída más suave), Elliptic (transición más pronunciada, rizado en ambas bandas). Predeterminado: Butterworth. Los shelves y picos utilizan su topología nativa de segundo orden independientemente de esta configuración. Almacenado por separado según la ruta: `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. | |
| Reset | Botón de acción en la tira de encabezado del editor. Restaura todas las bandas a sus valores predeterminados, restablece el conteo predeterminado de 10 bandas y reinicia la familia de filtros a Butterworth. Guarda inmediatamente. Tooltip: "Reset all bands to default values". | |
| Output Fader | Fader vertical combinado con medidor de nivel en el borde derecho del editor flotante. Arrastre para establecer la ganancia maestra post-EQ; la rueda del ratón ajusta en pasos de 0.5 dB; doble clic restablece a 0 dB. Rango: -36 a +12 dB. La barra de nivel detrás del manejador muestra el pico post-EQ suavizado en tiempo real con el mismo degradado verde-ámbar-rojo que el medidor de nivel Tube. Ubicado solo en el editor flotante — no en el mosaico del applet acoplado. | Almacenado por separado según la ruta: `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. Tooltip: "Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB." |
| Fila de íconos de tipo de filtro | Una fila de 8 íconos dibujados de forma personalizada (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada ícono dibuja la forma del filtro actual (campana de pico, rampa de shelf, pendiente HP/LP) en el color de paleta de su banda. Haga clic en un ícono para recorrer los tipos de filtro de esa banda; al hacer clic también se selecciona la banda, resaltando su manejador en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los íconos se atenúan al 35 % de opacidad cuando la banda está en bypass. Implementado por ClientEqIconRow. |
| Fila de texto de parámetros | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores de Freq, Gain y Q de cada banda. Los valores se actualizan en tiempo real durante los arrastres en el lienzo. Hacer clic en una columna selecciona esa banda. | Ubicado solo en el editor flotante. Implementado por ClientEqParamRow. |
| Líneas guía de corte de filtro (TX / RX) | Líneas verticales discontinuas amarillas superpuestas en el lienzo en el corte de filtro TX bajo/alto actual del radio (mosaico TX) o en los bordes de la banda de paso RX (mosaico RX). Colocar el cursor cerca de una línea cambia el cursor a una flecha de cambio de tamaño horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente del radio en tiempo real. | Arrastrar las guías de corte TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía. El mosaico del applet muestra las líneas guía como referencia visual; el arrastre solo está disponible en el editor flotante. |

El bypass se gestiona desde el widget CHAIN, no desde dentro del editor. Consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).

### Configuración almacenada

| Clave de configuración | Qué almacena | Notas |
|---|---|---|
| `ClientEqRxEnabled` | Si la etapa de EQ RX está habilitada. | |
| `ClientEqTxEnabled` | Si la etapa de EQ TX está habilitada. | |
| `ClientEqRxBands` | Parámetros de banda para el EQ RX. | |
| `ClientEqTxBands` | Parámetros de banda para el EQ TX. | |
| `ClientEqTxFilterFamily` | Selección de familia de filtros para el EQ TX. | Almacenado por ruta junto con `ClientEqRxFilterFamily`. |
| `ClientEqRxFilterFamily` | Selección de familia de filtros para el EQ RX. | Almacenado por ruta junto con `ClientEqTxFilterFamily`. |
| `ClientEqTxMasterGain` | Ganancia maestra de salida post-EQ para el EQ TX (-36 a +12 dB). | Tooltip en el Output Fader: "Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB." Predeterminado: 0 dB. |
| `ClientEqRxMasterGain` | Ganancia maestra de salida post-EQ para el EQ RX (-36 a +12 dB). | Tooltip en el Output Fader: "Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB." Predeterminado: 0 dB. |
| `ClientEqSmoothingFraction` | Nivel de suavizado por octava fraccionaria aplicado a la visualización de la traza del analizador. | Compartido entre los editores TX y RX. Predeterminado: Off (1/96). |

## Consejos

- Los mosaicos del applet están ocultos de forma predeterminada. Si desea una referencia visual permanente de su curva de EQ mientras opera, habilite la etapa de EQ mediante el widget CHAIN para que el mosaico se vuelva visible en el contenedor Aetherial Audio (TXDSP).
- El editor flotante es compartido entre TX y RX. Abrirlo desde el mosaico de cadena TX y luego abrirlo desde el mosaico de cadena RX cambia el editor al lado RX; su configuración TX no se ve afectada.
- Use Peak Hold para congelar la traza del analizador mientras ajusta una banda. Las resonancias que solo aparecen brevemente son fáciles de identificar porque la traza no decae mientras el botón está marcado. Desactive Peak Hold cuando haya terminado para reanudar el decaimiento normal.
- El control Smoothing promedia la traza del analizador mostrada utilizando promediado de potencia por octava fraccionaria. Use 1/3 para una traza más suave y fácil de leer al evaluar respuestas amplias; use Off (1/96) cuando necesite ver picos individuales estrechos con precisión. El suavizado no afecta la forma en que el EQ procesa el audio.
- Las líneas guía discontinuas amarillas de corte de filtro en el lienzo del editor muestran exactamente dónde el radio está atenuando la señal. Arrastre una línea guía directamente en el editor para mover la banda de paso del radio en tiempo real sin salir de la ventana del EQ.
- Haga clic en Reset para devolver el EQ a un estado conocido antes de construir un nuevo preset desde cero. El reinicio se guarda inmediatamente y persiste tras un reinicio del programa.
- Haga clic derecho en la barra de título del subcontenedor "Aetherial TX EQ" o "Aetherial RX EQ" para flotar, extraer u ocultar el mosaico.

## Relacionados

- [Inspeccionar la curva de EQ TX y el
