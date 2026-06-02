# Silenciar el audio de un slice desde el panel VFO

Silencie la salida de audio de un slice individual sin cambiar su configuración de ganancia de AF. Utilice esta función cuando desee suprimir un slice temporalmente y restaurar su volumen anterior con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO del slice objetivo debe estar abierto. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo primero.

## Pasos

1. Haga clic en el indicador del marcador VFO en la pantalla de espectro del slice que desea silenciar. El panel VFO se abre anclado al marcador.
2. Haga clic en **Audio** para seleccionar la pestaña Audio dentro del panel VFO.
3. Haga clic en **Mute**. El botón se activa y la salida de audio del slice se detiene. El valor del control deslizante de ganancia de AF no cambia.
4. Para restaurar el audio, haga clic en **Mute** nuevamente. El botón se desactiva y el audio se reanuda al nivel de ganancia de AF anterior.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Notas |
|---------|------|----------------|----------------|-------|
| Botón de antena RX | Botón pulsador | — | Abre el menú de selección de antena para la antena receptora de este slice. El menú usa `rxAntennaList()` si está disponible; de lo contrario, recurre a la lista completa de antenas. Cada acción establece la antena mediante `data()`. | |
| Botón de antena TX | Botón pulsador | — | Abre el menú de selección de antena para la antena transmisora de este slice. El menú se construye desde `txAntennaOptions()` que filtra los puertos de solo RX. Cada acción establece la antena mediante `data()`. | |
| Indicador de frecuencia | Indicador | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, la entrada de números enteros sin decimal inserta un punto decimal después del tercer dígito para las bandas de 2m/70cm (rango de 100-999 MHz). Para las bandas de 23cm y microondas, los números enteros se tratan como valores completos en MHz. Las entradas de frecuencia con punto decimal explícito por encima de 54 MHz se aceptan como valores en MHz en cualquier banda. | |
| Etiqueta de ancho de filtro | Indicador | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad. | Corrige un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Control deslizante de ganancia de AF (pestaña Audio) | Control deslizante | 100 | Establece el nivel de salida de audio para este slice. | No se conserva — refleja el estado vivo de la radio. |
| Control deslizante de paneo (pestaña Audio) | Control deslizante | 50 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. El relleno del control deslizante se ancla desde el centro hacia afuera, con un pequeño punto de marca central pintado en la ranura para mostrar la posición neutra. | |
| Botón Mute (pestaña Audio) | Botón de alternancia | Apagado | Silencia la salida de audio de este slice sin cambiar la configuración de ganancia de AF. | |
| Botón + control deslizante de squelch (pestaña Audio) | Botón de alternancia | Apagado | Activa el squelch para este slice. El control deslizante adyacente establece el umbral. | El squelch está deshabilitado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX y el squelch no es significativo; también bloquea señales FSK débiles. En modo CW, la radio bloquea el squelch en un nivel fijo y rechaza los cambios. |
| Combinación AGC (pestaña Audio) | Cuadro combinado | RÁPIDO | Establece la velocidad de ataque/liberación del AGC para este slice. | |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia | Apagado | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie de la radio y la compilación. | Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de configuración de AetherDSP para ese algoritmo. |
| Botón ADSP (pestaña DSP) | Botón pulsador | — | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de alternancia de DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Botón pulsador | — | Alterna la tira de canales de audio Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8). | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combinación Mode (pestaña Mode) | Cuadro combinado | USB | Establece el modo de demodulación para este slice. | |
| Botones de preajuste de filtro (pestaña Mode) | Botón pulsador | — | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Botón de alternancia | Apagado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. | |
| Combinación de canal DAX (pestaña DAX) | Cuadro combinado | Apagado | Asigna un canal de audio DAX a este slice. | |
| Botón de grosor del marcador | Botón pulsador | 1 px | Cicla la línea del marcador VFO a través de Apagado, 1 px y 3 px. | Se conserva por slice en `Slice{N}_MarkerWidth`. |
| Botón de bordes del filtro | Botón de alternancia | Mostrado | Alterna las líneas del borde del filtro en la banda de paso del espectro. | Se conserva por slice en `Slice{N}_FilterEdgesHidden`. |
| Alternancia de colapso | Botón de alternancia | Expandido | Colapsa el panel VFO a una tira compacta de solo frecuencia. | Se conserva por slice en `SliceFlagCollapsed_{N}`. |

## Cambios en la pestaña DSP en v0.9.7 (refinados en v0.9.8)

La pestaña DSP ahora muestra solo los algoritmos de reducción de ruido proporcionados por la radio. Los botones NR2, RN2, BNR, NR4, MNR y DFNR se han eliminado del panel VFO. Esos algoritmos son módulos del lado del cliente; acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

Los botones presentes en la pestaña DSP son:

| Botón | Algoritmo |
|-------|-----------|
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

Una fila compartida de **Nivel DSP** aparece debajo de la cuadrícula de botones. Contiene un control deslizante y una lectura numérica. El control deslizante se reorienta automáticamente al algoritmo DSP con nivel que se haya habilitado más recientemente. La etiqueta a la izquierda del control deslizante muestra el objetivo activo (por ejemplo, **NR** o **NB**). Cuando no hay ningún algoritmo DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila se atenúa y la interacción con el control deslizante no tiene efecto. La fila permanece en el diseño en todo momento; no desplaza la cuadrícula de botones cuando aparece o desaparece.

Algoritmos que admiten un nivel a través de este control deslizante: NR, NB, ANF, NRL, NRS, NRF, ANFL.

**Nota:** En v0.9.8, el control deslizante de nivel DSP ahora aparece al inicio para cualquier algoritmo DSP que estuviera habilitado en el perfil guardado de la radio. Anteriormente, faltaba hasta que el usuario alternaba manualmente el botón DSP.

## Comportamiento del squelch por modo

El botón y el control deslizante de squelch se deshabilitan automáticamente en ciertos modos:

- **Modos digitales (DIGU, DIGL):** El squelch está deshabilitado porque el audio alimenta decodificadores externos a través de DAX; el squelch no es significativo y bloquea señales FSK débiles.
- **RTTY:** El squelch está deshabilitado por las mismas razones que los modos digitales, resolviendo un problema donde el squelch bloqueaba señales FSK débiles (#2504).
- **CW:** El squelch está deshabilitado porque la radio bloquea el squelch en un nivel fijo y rechaza los cambios.

Cuando el squelch está deshabilitado y estaba previamente activado, el sistema apaga automáticamente el squelch para el slice y guarda su estado. Cuando vuelva a cambiar a un modo de voz, es posible que el squelch se restaure.

## Cambios en el diseño del panel VFO en v26.5.3

El widget de pestañas apiladas dentro del panel VFO ahora usa una subclase personalizada de `QStackedWidget` (`TabStack`) que informa solo el tamaño preferido de la pestaña actual. Esto corrige un espacio visual que aparecía al cambiar de la pestaña Mode (que tiene una altura de contenido más corta) a la pestaña DSP (que es más alta cuando el subcontenedor digital es visible). El panel VFO ya no asigna altura en exceso basándose en la pestaña más alta. El panel ahora ajusta su altura limpiamente al cambiar entre pestañas.

## Cambios de tematización en v26.6.1

El panel VFO ahora utiliza el sistema de tematización de AetherSDR. Todos los estilos de controles deslizantes y botones se derivan de tokens de color del tema en lugar de valores codificados, lo que garantiza que el panel coincida con el tema de color activo. Los cambios visuales clave son:

- **Control deslizante de paneo:** El relleno anclado al centro ahora usa el color de acento del tema (`color.accent`) para la región (centro → control). El fondo de la ranura usa el color de fondo del tema (`color.background.1`). Un punto de marca central permanece visible en la posición neutra.
- **Botones de alternancia pequeños (insignia TX, insignia RX, etc.):** Ahora heredan los colores de fondo y acento del tema a través de los tokens `{{color.background.1}}` y `{{color.accent}}`, reemplazando los valores codificados anteriores de `#1a2a3a` y `#00b4d8`.
- **Ámbito del tema:** El panel VFO se coloca bajo el ámbito del contenedor `spectrum/vfo` para que los clics del inspector en los componentes VFO muestren sus tokens de tematización sin propagarse a la pantalla de espectro.
- **Cobertura del inspector:** El widget declara su lista de tokens de lectura (`color.background.0`, `color.background.1`, `color.background.2`, `color.text.primary`, `color.text.label`, `color.accent`, `color.accent.bright`) para que los clics en modo Inspección produzcan listas de aciertos significativas para las áreas de fondo, medidor de señal e insignias.

## Consejos

- Silenciar un slice no restablece el control deslizante de ganancia de AF. Cuando reactive el sonido, el audio regresará al mismo nivel que tenía antes.
- Si desea silenciar un slice de forma permanente en lugar de temporal, arrastre el control deslizante de ganancia de AF a 0.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la pantalla de espectro para abrir el menú superpuesto, o abra el applet AetherDSP.
- Los botones ADSP y AetherVoice en la pestaña DSP son lanzadores del lado del cliente. Tienen el estilo de las alternancias DSP del lado de la radio pero no se pueden seleccionar.
- Use el botón **ADSP** para abrir el cuadro de diálogo de configuración de AetherDSP para algoritmos de reducción de ruido del lado del cliente.
- Use el botón **AetherVoice** para abrir la tira de canales de audio Aetherial para DSP unificado de TX/RX.
- El squelch se deshabilita automáticamente en modos digital, RTTY y CW. Si cambia a uno de estos modos mientras el squelch está activado, el sistema lo apagará y guardará su estado para restaurarlo cuando regrese a un modo de voz.
- La insignia del slice ahora admite formato de texto enriquecido para la letra del slice (#2606), lo que permite una representación HTML adecuada en la etiqueta de la insignia.
- Al ingresar una frecuencia directamente, si escribe un punto decimal explícito (por ejemplo, "144.200") y el valor está por encima de 54 MHz, se trata como MHz en cualquier banda, no solo en bandas XVTR. Esto funciona para todas las bandas de VHF, UHF y microondas.

## Relacionado

- [Ajustar ganancia de AF y paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Activar squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
