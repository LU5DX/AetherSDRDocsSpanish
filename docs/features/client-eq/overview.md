# Descripción general del Ecualizador Paramétrico Aetherial (TX / RX)

El Ecualizador Paramétrico Aetherial proporciona ecualización paramétrica del lado del cliente tanto para la ruta de audio de transmisión como para la de recepción. Úselo para dar forma al audio de su micrófono de TX o para ajustar el sonido del audio recibido antes de que llegue a sus altavoces o auriculares, sin modificar ningún procesamiento del lado de la radio.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio para configurar el EQ, pero se necesita una conexión para que la superposición del analizador FFT en vivo muestre el audio real.
- Los mosaicos (tiles) del applet del EQ están ocultos hasta que la etapa de EQ correspondiente se habilite mediante el widget CHAIN o el editor flotante. Si no ve "Aetherial TX EQ" o "Aetherial RX EQ" en el contenedor principal Aetherial Audio (TXDSP), primero habilite la etapa de EQ.

## Cómo funciona

AetherSDR crea dos mosaicos de EQ separados dentro del contenedor principal Aetherial Audio (TXDSP):

- **Aetherial TX EQ** — procesa el audio solo en la ruta de transmisión.
- **Aetherial RX EQ** — procesa el audio solo en la ruta de recepción.

Cada mosaico está fijado a su ruta. No hay un selector RX/TX dentro del mosaico. El mosaico muestra una vista compacta de la curva de respuesta del EQ sumada y una superposición del analizador FFT en vivo para esa ruta. Se dibuja una traza de retención de pico (peak-hold) sobre el analizador en vivo, que muestra el nivel máximo por frecuencia visto desde el último restablecimiento; la traza se desvanece a aproximadamente 10 dB/s durante la operación normal. La traza de retención de pico opera sobre los bins FFT sin procesar, por lo que la detección de picos es precisa en términos de muestra; el suavizado de visualización (cuando está habilitado) se aplica por separado y no afecta los datos de retención de pico. La edición — agregar, eliminar y ajustar bandas — ocurre en una ventana flotante separada llamada editor **Aetherial Parametric EQ**, que se abre desde el widget CHAIN. La barra de título del editor muestra "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX", dependiendo de qué lado lo haya abierto. Una misma instancia del editor se reutiliza para ambos lados; el título cambia cuando cambia de lado.

### Mosaico del applet

Cada mosaico contiene un área de control:

| Elemento | Descripción |
|---|---|
| Área del analizador / curva | Una vista de al menos 110 px de alto que muestra la curva de respuesta del EQ sumada para todas las bandas habilitadas en esa ruta, con una superposición del analizador FFT en vivo y una traza de retención de pico. Líneas verticales amarillas discontinuas marcan los cortes actuales del filtro TX bajo/alto de la radio (mosaico TX) o los bordes de la banda de paso RX (mosaico RX). Esta área es solo de visualización en el mosaico del applet. |

La **respuesta del EQ sumada** muestra la respuesta de frecuencia acumulada de todas las bandas habilitadas. Cuando no hay bandas realzadas o atenuadas, la curva es plana; se atenúa a gris cuando la etapa de EQ está desviada (bypassed). La **superposición del analizador en vivo** muestra la FFT en tiempo real del audio que pasa por esa ruta como un relleno de degradado cian; está inactiva cuando no hay audio activo y activa cuando hay audio presente. La **traza de retención de pico** es una línea suave de color blanco apagado que rastrea la energía máxima observada por frecuencia, lo que ayuda a identificar resonancias y picos agresivos durante el ajuste. La traza se desvanece a aproximadamente 10 dB/s entre actualizaciones. Se puede congelar desde el editor flotante usando el botón Peak Hold. Las **líneas guía de corte del filtro** son líneas verticales amarillas discontinuas que marcan los cortes actuales del filtro TX bajo/alto de la radio (mosaico TX) o los bordes de la banda de paso RX (mosaico RX) directamente en el lienzo. Estas líneas son visibles en el mosaico del applet y son arrastrables en el editor flotante. Una **barra de plano de bandas de audio** siempre es visible en la parte inferior del lienzo, mostrando las regiones de modulación E-SSB / SSB / AM-FM como referencia; la interacción del cursor en esta área está excluida de la detección de impacto (hit-testing) de los manipuladores de banda.

### Editor flotante
Al hacer doble clic en la etapa de EQ en el widget CHAIN se abre el editor flotante para ese lado. El editor proporciona:

| Control | Descripción | Notas |
|---|---|---|
| Área del analizador / curva (lienzo) | Lienzo interactivo donde arrastra los manipuladores de banda para establecer frecuencia y ganancia. Arrastre los manipuladores de pico/estante (peak/shelf) para ajustar frecuencia y ganancia. Arrastre los manipuladores HP/LP para ajustar frecuencia y Q. Mantenga presionada la tecla Shift mientras arrastra para ajustar Q en cualquier tipo de banda. Haga clic en un icono de banda para recorrer los tipos de filtro. La traza de retención de pico también es visible aquí y refleja el estado congelado/en descomposición establecido por el botón Peak Hold. El lienzo también muestra una superposición de curva de referencia ámbar semitransparente (consulte Preajustes de curva de referencia a continuación). | |
| Peak Hold | Botón seleccionable en la barra de encabezado del editor. Cuando está marcado, la traza de retención de pico por bin del analizador deja de desvanecerse: el nivel más alto observado para cada frecuencia se mantiene hasta que desactiva el botón. El botón muestra un fondo ámbar cuando está marcado. Desmárquelo para reanudar el desvanecimiento normal a aproximadamente 10 dB/s. | Ubicado en la barra de encabezado del editor (solo editor flotante). |
| Smoothing | Cuadro combinado en la barra de encabezado del editor. Aplica un promediado de potencia de octava fraccional a la traza del analizador para la visualización; no afecta los cálculos del EQ. Opciones: Off (1/96), 1/24, 1/12, 1/6, 1/3. Fracción más baja = más suavizado (1/3 es el más suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX. Persistido como `ClientEqSmoothingFraction`. | Información sobre herramientas: "Suavizado de octava fraccional aplicado a la traza del analizador. Fracción más baja = más suavizado (1/3 = máximo, 1/96 = desactivado). Afecta solo la visualización; los cálculos del EQ no cambian." Ubicado en la barra de encabezado del editor (solo editor flotante). El suavizado se calcula después de la actualización de retención de pico en cada fotograma, por lo que tanto la traza en vivo como la traza de retención de pico se suavizan de forma independiente para la visualización. |
| Filter family | Cuadro combinado en la barra de encabezado del editor. Selecciona la familia de filtros aplicada a los cálculos en cascada HP/LP. Opciones: Butterworth (banda de paso máximamente plana), Chebyshev (transición más pronunciada, 1 dB de ondulación en la banda de paso), Bessel (fase lineal, caída más suave), Elliptic (transición más pronunciada, ondulación en ambas bandas). Predeterminado: Butterworth. Los estantes y picos usan su topología nativa de segundo orden independientemente de esta configuración. Persistido por separado por ruta: `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. |
| Reset | Botón pulsador en la barra de encabezado del editor. Restablece todas las bandas a sus valores predeterminados, restaura el conteo predeterminado de 10 bandas y restablece la familia de filtros a Butterworth. Guarda inmediatamente. Información sobre herramientas: "Restablecer todas las bandas a los valores predeterminados". | Ubicado en la barra de encabezado del editor (solo editor flotante). |
| Reference curve preset | Cuadro combinado en la barra de encabezado del editor. Superpone una curva objetivo ámbar semitransparente en el lienzo, que representa la respuesta de frecuencia de un micrófono clásico o estándar de audio. Seleccione "Off" para ocultar la curva de referencia. Opciones: Off, AT&T 1959, Heil DX, Astatic D-104, Shure 444, Heil HC-5. | La curva de referencia es solo una guía visual; no afecta los cálculos del EQ ni el procesamiento de audio. Úsela como objetivo para dar forma a sus bandas de EQ paramétrico hacia una respuesta deseada. |
| Output Fader | Mezclador/medidor de nivel vertical combinado en el borde derecho del editor flotante. Arrastre para establecer la ganancia maestra posterior al EQ; la rueda de desplazamiento ajusta en pasos de 0.5 dB; doble clic restablece a 0 dB. Rango: -36 a +12 dB. La barra de nivel detrás del manipulador muestra el pico posterior al EQ suavizado en tiempo real con el mismo degradado verde-ámbar-rojo que el medidor de nivel Tube. Haga clic en la visualización del valor numérico en la parte inferior para editarlo directamente: escriba un valor en dB y presione Enter para confirmar (limitado al rango). Presione Escape para cancelar la edición. Ubicado solo en el editor flotante, no en el mosaico acoplado del applet. | Persistido por separado por ruta: `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. Información sobre herramientas: "Ganancia de salida (dB). Arrastre para ajustar, rueda para paso fino, doble clic para restablecer a 0 dB." La visualización del valor numérico es un `QLineEdit` que parece idéntico a una etiqueta hasta que se enfoca. Al enfocarse, muestra el número simple con un borde cian; escriba un valor y presione Enter o haga clic fuera para confirmar. El valor se limita al rango de -36 a +12 dB. |
| Fila de iconos de tipo de filtro | Una fila de 8 iconos pintados personalizados (uno por espacio de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana de pico, rampa de estante, pendiente HP/LP) en el color de la paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro para esa banda; al hacer clic también se selecciona la banda, resaltando su manipulador en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está desviada. Implementado por `ClientEqIconRow`. |
| Fila de texto de parámetros | Una fila de 8 columnas de texto (una por espacio de banda) debajo del lienzo que muestra los valores de Freq, Gain y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. Haga clic derecho en una columna para abrir un menú contextual para la entrada numérica de los valores de Freq, Gain o Q. Al confirmar una entrada numérica se guarda y redibuja el lienzo y la fila de iconos inmediatamente. El fondo de la fila es transparente para que ya no se superponga con la barra de plano de bandas de audio en la parte inferior del lienzo sobre ella. | Ubicado solo en el editor flotante. Implementado por `ClientEqParamRow`. La entrada numérica a través del menú de clic derecho se agregó en v26.5.2.1 para persistir las ediciones inmediatamente (problema #2655). |
| Líneas guía de corte del filtro (TX / RX) | Líneas verticales amarillas discontinuas superpuestas en el lienzo en los cortes actuales del filtro TX bajo/alto de la radio (mosaico TX) o los bordes de la banda de paso RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte del filtro correspondiente de la radio en tiempo real. | Arrastrar las guías de corte TX emite `cutoffsDragRequested(Tx, lo, hi)`, que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía. Las guías de banda de paso RX se almacenan en caché internamente; al cambiar de TX a RX, las guías RX correctas se restauran automáticamente. El mosaico del applet muestra las líneas guía como referencia visual; el arrastre está disponible solo en el editor flotante. |

El desvío (bypass) se maneja desde el widget CHAIN, no desde el interior del editor. Consulte [Desviar la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).

### Preajustes de curva de referencia

La función de preajuste de curva de referencia superpone una curva objetivo visual en el lienzo del EQ, lo que le permite dar forma a sus bandas de EQ paramétrico hacia la respuesta de frecuencia de micrófonos clásicos o estándares de audio. La curva se dibuja como una línea ámbar semitransparente detrás de las curvas de su banda de EQ. Seleccionar un preajuste no cambia el procesamiento de audio; es solo una guía visual.

Preajustes de curva de referencia disponibles:

| Preajuste | Descripción |
|---|---|
| Off | No se muestra ninguna curva de referencia. |
| AT&T 1959 | El objetivo canónico de Bell Labs de "respuesta de frecuencia de transmisión óptima para el habla". Pico de +5 dB a 2.5 kHz, se atenúa por debajo de 300 Hz y por encima de 3.4 kHz. |
| Heil DX | La recomendación publicada de Bob Heil para máxima potencia de habla en pile-ups. Pico más pronunciado de +6 dB a 2.7 kHz con corte de graves más agresivo que AT&T 1959. |
| Astatic D-104 | La respuesta clásica del micrófono de cristal "lollipop". Realce de presencia extremadamente puntiagudo alrededor de 3 kHz con una fuerte atenuación de graves. |
| Shure 444 | Micrófono de escritorio clásico de estilo broadcast con respuesta más amplia y realce de presencia más suave: la más suave de las curvas de micrófono legendarias. |
| Heil HC-5 | Forma objetivo moderna de micrófono dinámico para SSB. El realce de presencia media alcanza su punto máximo a 3 kHz a +5 dB. |

Para seleccionar una curva de referencia:
1. Abra el editor flotante para la ruta deseada (TX o RX).
2. Haga clic en el cuadro combinado **Reference curve** en la barra de encabezado del editor.
3. Seleccione el preajuste deseado de la lista desplegable.
4. La curva ámbar semitransparente aparece en el lienzo inmediatamente.
5. Dé forma a sus bandas de EQ paramétrico para que coincidan con la referencia visual.
6. Seleccione "Off" para ocultar la curva de referencia.

La selección de la curva de referencia es solo visual y no se persiste entre sesiones.

### Configuraciones persistidas

| Clave de configuración | Qué almacena | Notas |
|---|---|---|
| `ClientEqRxEnabled` | Si la etapa de EQ de RX está habilitada. | |
| `ClientEqTxEnabled` | Si la etapa de EQ de TX está habilitada. | |
| `ClientEqRxBands` | Parámetros de banda para el EQ de RX. | |
| `ClientEqTx
