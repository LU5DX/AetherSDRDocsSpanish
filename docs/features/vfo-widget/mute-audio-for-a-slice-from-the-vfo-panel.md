# Silenciar el audio de un slice desde el panel VFO

Silencie la salida de audio de un slice individual sin cambiar su configuración de ganancia AF. Úselo cuando desee suprimir un slice temporalmente y restaurar su volumen anterior con un clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO del slice de destino debe estar abierto. Si está contraído a una tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo primero.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea silenciar. El panel VFO se abre anclado al marcador.
2. Haga clic en **Audio** para seleccionar la pestaña Audio dentro del panel VFO. Alternativamente, haga clic derecho en el botón de la pestaña Audio para alternar el silencio directamente sin abrir la pestaña.
3. Haga clic en **Mute**. El botón se activa y la salida de audio del slice se detiene. El valor del control deslizante de ganancia AF no cambia.
4. Para restaurar el audio, haga clic en **Mute** nuevamente. El botón se desactiva y el audio se reanuda en el nivel de ganancia AF anterior.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Notas |
|---------|------|---------|----------|-------|
| Botón de antena RX | Botón pulsador | — | Abre el menú de selección de antena para la antena receptora de este slice. | |
| Botón de antena TX | Botón pulsador | — | Abre el menú de selección de antena para la antena transmisora de este slice. | |
| Pantalla de frecuencia | Indicador | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, la entrada de enteros simples inserta un decimal después del tercer dígito para bandas de 2 m/70 cm (rango de 100-999 MHz). Para bandas de 23 cm y microondas, los enteros simples se tratan como valores completos en MHz. Las entradas de frecuencia con puntos decimales explícitos por encima de 54 MHz se aceptan como valores en MHz en cualquier banda. | Accesibilidad: la etiqueta de frecuencia emite `QAccessibleValueChangeEvent` cuando la frecuencia cambia mediante actualización de la radio, para que los lectores de pantalla puedan anunciar el nuevo valor. |
| Etiqueta de ancho de filtro | Indicador | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de ajustes preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad. | Corrige un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Control deslizante de ganancia AF (pestaña Audio) | Control deslizante | 100 | Establece el nivel de salida de audio para este slice. | No se conserva: refleja el estado en vivo de la radio. |
| Control deslizante de paneo (pestaña Audio) | Control deslizante | 50 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. El relleno del control deslizante se ancla desde el centro hacia afuera, con un pequeño punto de marca central dibujado en la ranura para mostrar la posición neutra. | |
| Botón Mute (pestaña Audio) | Botón de alternancia | Off | Silencia la salida de audio de este slice sin cambiar la configuración de ganancia AF. | Haga clic derecho en la etiqueta de la pestaña Audio para alternar el silencio directamente. |
| Botón + control deslizante de silenciador (pestaña Audio) | Botón de alternancia | Off | Activa el silenciador para este slice. El control deslizante adyacente establece el umbral. | El silenciador está deshabilitado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX y el silenciador no es significativo; también bloquea señales FSK débiles. En modo CW, la radio fija el silenciador activado en un nivel fijo y rechaza cambios. Utiliza la API `setManualSquelch` (v26.8.4). |
| Combo AGC (pestaña Audio) | Cuadro combinado | FAST | Establece la velocidad de ataque/liberación del AGC para este slice. | |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia | Off | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de radio y la compilación. | Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| Botón ADSP (pestaña DSP) | Botón pulsador | — | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un botón de alternancia DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Botón pulsador | — | Alterna la tira de canal de audio Aetherial, la suite unificada de DSP TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combo Mode (pestaña Mode) | Cuadro combinado | USB | Establece el modo de demodulación para este slice. | |
| Botones de ajustes preestablecidos de filtro (pestaña Mode) | Botón pulsador | — | Aplica un ajuste preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Botón de alternancia | Off | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del mouse ajusta en pasos de 10 Hz. | |
| Combo de canal DAX (pestaña DAX) | Cuadro combinado | Off | Asigna un canal de audio DAX a este slice. | |
| Botón de grosor del marcador | Botón pulsador | 1 px | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. | Se conserva por slice en `Slice{N}_MarkerWidth`. |
| Botón de bordes del filtro | Botón de alternancia | Shown | Alterna las líneas de borde del filtro en la banda pasante del espectro. | Se conserva por slice en `Slice{N}_FilterEdgesHidden`. |
| Alternancia de contracción | Botón de alternancia | Expanded | Contrae el panel VFO a una tira compacta de solo frecuencia. | Se conserva por slice en `SliceFlagCollapsed_{N}`. Haga clic derecho en la etiqueta de frecuencia contraída para abrir el menú contextual Add Spot usando la propia frecuencia del VFO (v26.8.4). |

## Cambios en la pestaña DSP en v26.8.4

La pestaña DSP ahora incluye un botón **Manual notch filter (MN)**. Este botón aparece solo cuando la radio conectada reporta soporte para filtrado de muesca manual (`hasManualNotch`). Está oculto en radios que no admiten esta función.

El botón MN:

- Es un botón de alternancia en la cuadrícula de botones DSP, ubicado en la fila 3, columna 2.
- Usa el mismo estilo `kDspToggle` que los demás botones DSP.
- Tiene un nombre accesible de **"Manual notch filter"**.
- Abre un control de nivel DSP relacionado dirigido a `MN` cuando se activa (el control deslizante compartido de nivel DSP se redirige a él).
- Hacer clic derecho abre el diálogo de configuración de AetherDSP para el algoritmo de filtro de muesca manual, consistente con los demás botones de filtro de muesca.

Todos los botones DSP ahora tienen nombres de objeto estables (`dspNRBtn`, `dspNBBtn`, `dspMNBtn`, etc.) además de sus nombres accesibles. Esto proporciona un contrato fijo para que las herramientas de automatización y scripting puedan dirigirse a los botones de manera confiable, independientemente de cualquier cambio futuro en el texto de los nombres accesibles.

## Cambios en la pestaña DSP en v0.9.7 (refinados en v0.9.8)

La pestaña DSP ahora muestra solo los algoritmos de reducción de ruido proporcionados por la radio. Los botones para NR2, RN2, BNR, NR4, MNR y DFNR se han eliminado del panel VFO. Esos algoritmos son módulos del lado del cliente; acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

Los botones presentes en la pestaña DSP son:

| Botón | Algoritmo |
|--------|-----------|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (solo modo CW) |
| MN | Filtro de muesca manual (solo en radios que lo admiten) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

Una fila compartida de **DSP Level** aparece debajo de la cuadrícula de botones. Contiene un control deslizante y una lectura numérica. El control deslizante se redirige automáticamente al algoritmo DSP con nivel activado más recientemente. La etiqueta a la izquierda del control deslizante muestra el objetivo activo (por ejemplo, **NR** o **NB**). Cuando no hay ningún algoritmo DSP con nivel activo — o cuando solo RNN, ANFT o APF están activados — la fila se desvanece y la interacción con el control deslizante no tiene efecto. La fila permanece en el diseño en todo momento; no desplaza la cuadrícula de botones cuando se desvanece o aparece.

Algoritmos que admiten un nivel mediante este control deslizante: NR, NB, ANF, NRL, NRS, NRF, ANFL, MN.

**Nota:** En v0.9.8, el control deslizante de nivel DSP ahora aparece al inicio para cualquier algoritmo DSP que estuviera activado en el perfil guardado de la radio. Anteriormente, faltaba hasta que el usuario alternaba manualmente el botón DSP.

## Comportamiento del silenciador por modo

El botón y el control deslizante del silenciador se deshabilitan automáticamente en ciertos modos:

- **Modos digitales (DIGU, DIGL):** El silenciador está deshabilitado porque el audio alimenta decodificadores externos a través de DAX — el silenciador no es significativo y bloquea señales FSK débiles.
- **RTTY:** El silenciador está deshabilitado por las mismas razones que en modos digitales, resolviendo un problema donde el silenciador bloqueaba señales FSK débiles (#2504).
- **CW:** El silenciador está deshabilitado porque la radio fija el silenciador activado en un nivel fijo y rechaza cambios.
- **Modos FM (FM, NFM, DFM):** Los controles de tono FM (CTCSS/DCS) están disponibles; el silenciador funciona normalmente en estos modos.

Cuando el silenciador está deshabilitado y estaba previamente activado, el sistema apaga automáticamente el silenciador para el slice y guarda su estado. Cuando cambia de nuevo a un modo de voz, el silenciador puede restaurarse.

## Cambios en el diseño del panel VFO en v26.5.3

El widget de pestañas apiladas dentro del panel VFO ahora usa una subclase personalizada de `QStackedWidget` (`TabStack`) que reporta solo el tamaño preferido de la pestaña actual. Esto corrige un espacio visual que ocurría al cambiar de la pestaña Mode (que tiene una altura de contenido más corta) a la pestaña DSP (que es más alta cuando el subcontenedor digital es visible). El panel VFO ya no asigna altura en exceso basándose en la pestaña más alta. El panel ahora ajusta su altura limpiamente al cambiar entre pestañas.

## Cambios en el diseño del panel VFO en v26.7.4

El widget `TabStack` ahora además reenvía `hasHeightForWidth()` y `heightForWidth()` de la página actual. Esto permite que las páginas que mantienen una relación de aspecto (como el medidor SmartMtrWidget) controlen la altura de la tira correctamente. Las páginas sin altura según ancho (como el espaciador del medidor S) no se ven afectadas. La bandera VFO ahora también incluye una sombra de elevación ligera renderizada por un widget separado `FlagShadow`. La sombra se mantiene en una superficie separada para que las repeticiones de pintado del medidor en vivo no vuelvan a difuminar toda la bandera a la velocidad de animación.

## Cambios en la navegación de pestañas en v26.6.3

Las etiquetas de las pestañas en el panel VFO se han cambiado de `QLabel` a `QPushButton`. Esto mejora la accesibilidad al hacer que los botones de pestaña sean enfocables con el teclado mediante la navegación con la tecla Tab. Cada botón de pestaña ahora tiene un indicador de enfoque (contorno) que se muestra cuando se enfoca mediante el teclado.

**Pestaña Audio:** Haga clic derecho en el botón de la pestaña Audio para alternar el estado de silencio de ese slice directamente, sin abrir la pestaña Audio.

**Entrada de frecuencia:** El campo de entrada de frecuencia se ha reemplazado con un widget `FreqLineEdit` que muestra texto de sugerencia en lugar de texto de marcador de posición, mejorando la apariencia visual de la entrada directa de frecuencia.

**Refinamiento del evento de rueda:** La rueda de desplazamiento de frecuencia ahora respeta la configuración `reverseMouseWheel` de `InteractionSettings`. Si ha configurado la rueda del mouse invertida en la configuración, al desplazarse sobre la frecuencia del panel VFO se invertirá la dirección en consecuencia (#3302).

## Cambios de tematización en v26.6.1

El panel VFO ahora usa el sistema de tematización de AetherSDR. Todos los estilos de controles deslizantes y botones se derivan de tokens de color del tema en lugar de valores codificados, asegurando que el panel coincida con el tema de color activo. Los cambios visuales clave son:

- **Control deslizante de paneo:** El relleno anclado al centro ahora usa el color de acento del tema (`color.accent`) para la región (centro → control). El fondo de la ranura usa el color de fondo del tema (`color.background.1`). Un punto de marca central permanece visible en la posición neutra.
- **Botones de alternancia pequeños (insignia TX, insignia RX, etc.):** Estos ahora heredan los colores de fondo y acento del tema a través de los tokens `{{color.background.1}}` y `{{color.accent}}`, reemplazando los valores codificados anteriores `#1a2a3a` y `#00b4d8`.
- **Alcance del tema:** El panel VFO se coloca bajo el alcance del
