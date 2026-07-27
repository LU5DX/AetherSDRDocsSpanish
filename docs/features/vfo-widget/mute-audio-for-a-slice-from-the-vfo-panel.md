# Silenciar audio de un slice desde el panel VFO

Silencie la salida de audio de un slice individual sin cambiar su ajuste de Ganancia AF. Use esta función cuando desee suprimir un slice temporalmente y restaurar su volumen anterior con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO para el slice de destino debe estar abierto. Si está colapsado en una tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo primero.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla de espectro para el slice que desea silenciar. El panel VFO se abre anclado al marcador.
2. Haga clic en **Audio** para seleccionar la pestaña Audio dentro del panel VFO. Alternativamente, haga clic derecho en el botón de la pestaña Audio para alternar el silencio directamente sin abrir la pestaña.
3. Haga clic en **Mute**. El botón se activa y la salida de audio del slice se detiene. El valor del deslizador de Ganancia AF no cambia.
4. Para restaurar el audio, haga clic en **Mute** nuevamente. El botón se desactiva y el audio se reanuda al nivel de Ganancia AF anterior.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Notas |
|---------|------|----------------|----------------|-------|
| Botón de antena RX | Botón pulsador | — | Abre el menú de selección de antena para la antena receptora de este slice. | |
| Botón de antena TX | Botón pulsador | — | Abre el menú de selección de antena para la antena transmisora de este slice. | |
| Indicador de frecuencia | Indicador | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, la entrada de enteros simples inserta un decimal después del tercer dígito para bandas de 2 m/70 cm (rango 100-999 MHz). Para bandas de 23 cm y microondas, los enteros simples se tratan como valores completos en MHz. Las entradas de frecuencia con punto decimal explícito por encima de 54 MHz se aceptan como valores en MHz en cualquier banda. | Accesibilidad: la etiqueta de frecuencia emite `QAccessibleValueChangeEvent` cuando la frecuencia cambia mediante actualización de radio, para que los lectores de pantalla puedan anunciar el nuevo valor. |
| Etiqueta de ancho de filtro | Indicador | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad. | Corrige un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Deslizador de Ganancia AF (pestaña Audio) | Deslizador | 100 | Establece el nivel de salida de audio para este slice. | No se conserva — refleja el estado vivo de la radio. |
| Deslizador de Pan (pestaña Audio) | Deslizador | 50 | Establece el paneo estéreo izquierda/derecha para este slice. 50 = centro. El llenado del deslizador se ancla desde el centro hacia afuera, con un pequeño punto de marca central pintado en la ranura para mostrar la posición neutra. | |
| Botón Mute (pestaña Audio) | Botón de alternancia | Off | Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. | Haga clic derecho en la etiqueta de la pestaña Audio para alternar el silencio directamente. |
| Botón + deslizador de Squelch (pestaña Audio) | Botón de alternancia | Off | Activa el squelch para este slice. El deslizador adyacente establece el umbral. | El squelch está deshabilitado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX y el squelch no tiene sentido — también bloquea señales FSK débiles. En modo CW, la radio bloquea el squelch activado a un nivel fijo y rechaza cambios. |
| Combo AGC (pestaña Audio) | Cuadro combinado | FAST | Establece la velocidad de ataque/release del AGC para este slice. | |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia | Off | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de botones depende de la serie de radio y la compilación. | Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón ADSP (pestaña DSP) | Botón pulsador | — | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo de alternancia DSP del lado de la radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo de Configuración de AetherDSP no modal. |
| Botón AetherVoice (pestaña DSP) | Botón pulsador | — | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para el strip. |
| Combo de modo (pestaña Mode) | Cuadro combinado | USB | Establece el modo de demodulación para este slice. | |
| Botones de preajuste de filtro (pestaña Mode) | Botón pulsador | — | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Botón de alternancia | Off | Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. | |
| Combo de canal DAX (pestaña DAX) | Cuadro combinado | Off | Asigna un canal de audio DAX a este slice. | |
| Botón de grosor de marcador | Botón pulsador | 1 px | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. | Se conserva por slice en `Slice{N}_MarkerWidth`. |
| Botón de bordes de filtro | Botón de alternancia | Mostrado | Alterna las líneas de borde del filtro en la banda de paso del espectro. | Se conserva por slice en `Slice{N}_FilterEdgesHidden`. |
| Alternancia de colapso | Botón de alternancia | Expandido | Colapsa el panel VFO a una tira compacta de solo frecuencia. | Se conserva por slice en `SliceFlagCollapsed_{N}`. |

## Cambios en la pestaña DSP en v0.9.7 (refinados en v0.9.8)

La pestaña DSP ahora muestra solo los algoritmos de reducción de ruido proporcionados por la radio. Los botones para NR2, RN2, BNR, NR4, MNR y DFNR se han eliminado del panel VFO. Esos algoritmos son módulos del lado del cliente; acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

Los botones presentes en la pestaña DSP son:

| Botón | Algoritmo |
|--------|-----------|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

Una fila compartida de **Nivel DSP** aparece debajo de la cuadrícula de botones. Contiene un deslizador y una lectura numérica. El deslizador se redirige automáticamente al algoritmo DSP con nivel que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el destino activo (por ejemplo, **NR** o **NB**). Cuando no hay ningún algoritmo DSP con nivel activo — o cuando solo RNN, ANFT o APF está encendido — la fila se atenúa y la interacción con el deslizador no tiene efecto. La fila permanece en el diseño en todo momento; no desplaza la cuadrícula de botones cuando se atenúa o aparece.

Algoritmos que admiten un nivel a través de este deslizador: NR, NB, ANF, NRL, NRS, NRF, ANFL.

**Nota:** En v0.9.8, el deslizador de nivel DSP ahora aparece al inicio para cualquier algoritmo DSP que estuviera habilitado en el perfil guardado de la radio. Anteriormente, faltaba hasta que el usuario alternaba manualmente el botón DSP.

## Comportamiento del squelch por modo

El botón y el deslizador de squelch se deshabilitan automáticamente en ciertos modos:

- **Modos digitales (DIGU, DIGL):** El squelch está deshabilitado porque el audio alimenta decodificadores externos a través de DAX — el squelch no tiene sentido y bloquea señales FSK débiles.
- **RTTY:** El squelch está deshabilitado por las mismas razones que los modos digitales, resolviendo un problema donde el squelch bloqueaba señales FSK débiles (#2504).
- **CW:** El squelch está deshabilitado porque la radio bloquea el squelch activado a un nivel fijo y rechaza cambios.

Cuando el squelch está deshabilitado y estaba previamente activado, el sistema apaga automáticamente el squelch para el slice y guarda su estado. Cuando vuelve a un modo de voz, el squelch puede restaurarse.

## Cambios en el diseño del panel VFO en v26.5.3

El widget de pestañas apiladas dentro del panel VFO ahora usa una subclase personalizada de `QStackedWidget` (`TabStack`) que informa solo el tamaño preferido de la pestaña actual. Esto corrige un espacio visual que ocurría al cambiar de la pestaña Mode (que tiene una altura de contenido más corta) a la pestaña DSP (que es más alta cuando el subcontenedor digital está visible). El panel VFO ya no asigna altura en exceso basada en la pestaña más alta. El panel ahora ajusta su altura correctamente a medida que cambia entre pestañas.

## Cambios en el diseño del panel VFO en v26.7.4

El widget `TabStack` ahora además reenvía `hasHeightForWidth()` y `heightForWidth()` desde la página actual. Esto permite que las páginas que mantienen una relación de aspecto (como el medidor SmartMtrWidget) impulsen la altura de la tira correctamente. Las páginas sin altura-por-ancho (como el espaciador del S-meter) no se ven afectadas. La bandera VFO ahora también incluye una sombra de elevación ligera renderizada por un widget `FlagShadow` separado. La sombra se mantiene en una superficie separada para que las repintadas del medidor en vivo no vuelvan a desenfocar toda la bandera a la velocidad de animación.

## Cambios en la navegación de pestañas en v26.6.3

Las etiquetas de pestaña en el panel VFO se han cambiado de `QLabel` a `QPushButton`. Esto mejora la accesibilidad al hacer que los botones de pestaña sean enfocables por teclado con la navegación de tecla Tab. Cada botón de pestaña ahora tiene un indicador de enfoque (contorno) que se muestra cuando se enfoca mediante teclado.

**Pestaña Audio:** Haga clic derecho en el botón de la pestaña Audio para alternar el estado de silencio de ese slice directamente, sin abrir la pestaña Audio.

**Entrada de frecuencia:** El campo de entrada de frecuencia se ha reemplazado con un widget `FreqLineEdit` que muestra texto de sugerencia en lugar de texto de marcador de posición, mejorando la apariencia visual de la entrada directa de frecuencia.

**Refinamiento del evento de rueda:** La rueda de desplazamiento de frecuencia ahora respeta la configuración `reverseMouseWheel` de `InteractionSettings`. Si ha configurado la rueda del ratón invertida en la configuración, desplazarse sobre la frecuencia del panel VFO invertirá la dirección en consecuencia (#3302).

## Cambios de tematización en v26.6.1

El panel VFO ahora usa el sistema de tematización de AetherSDR. Todos los estilos de deslizadores y botones se derivan de tokens de color del tema en lugar de valores codificados, asegurando que el panel coincida con el tema de color activo. Los cambios visuales clave son:

- **Deslizador de Pan:** El llenado anclado al centro ahora usa el color de acento del tema (`color.accent`) para la región (centro → control deslizante). El fondo de la ranura usa el color de fondo del tema (`color.background.1`). Un punto de marca central permanece visible en la posición neutra.
- **Botones de alternancia pequeños (insignia TX, insignia RX, etc.):** Estos ahora heredan los colores de fondo y acento del tema a través de los tokens `{{color.background.1}}` y `{{color.accent}}`, reemplazando los valores codificados anteriores `#1a2a3a` y `#00b4d8`.
- **Ámbito del tema:** El panel VFO se coloca bajo el ámbito del contenedor `spectrum/vfo` para que los clics del inspector en componentes VFO muestren sus tokens de tematización sin propagarse a la pantalla de espectro.
- **Cobertura del inspector:** El widget declara su lista de tokens de lectura (`color.background.0`, `color.background.1`, `color.background.2`, `color.text.primary`, `color.text.label`, `color.accent`, `color.accent.bright`) para que los clics en modo Inspect produzcan listas de aciertos significativas para las áreas de fondo, medidor de señal e insignias.

## Consejos

- Silenciar un slice no restablece el deslizador de Ganancia AF. Cuando reactive el sonido, el audio regresa al mismo nivel que tenía antes.
- Haga clic derecho en la etiqueta de la pestaña **Audio** para alternar el silencio directamente sin cambiar a la pestaña Audio.
- Si desea silenciar un slice permanentemente en lugar de temporalmente, arrastre el deslizador de Ganancia AF a 0.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la pantalla de espectro para abrir el menú superpuesto, o abra el applet AetherDSP.
- Los botones ADSP y AetherVoice en la pestaña DSP son lanzadores del lado del cliente. Tienen el estilo de alternancias DSP del lado de la radio pero no son marcables.
- Use el botón **ADSP** para abrir el diálogo de Configuración de AetherDSP para algoritmos de reducción de ruido del lado del cliente.
- Use el botón **AetherVoice** para abrir la Aetherial Audio Channel Strip para DSP unificado TX/RX.
- El squelch se deshabilita automáticamente en modos digital, RTTY y CW. Si cambia a uno de estos modos mientras el squelch está encendido, el sistema lo apagará y guardará su estado para restaurarlo cuando regrese a un modo de voz.
- La insignia del slice ahora admite formato de texto en
