# Ajustar la ganancia de AF y la panorámica desde el panel del VFO

Utilice la pestaña Audio del panel del VFO para establecer el nivel de salida de audio y la posición de panorámica estéreo de cualquier segmento de recepción de forma independiente de otros segmentos.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El panel del VFO requiere una conexión activa al equipo.
- El panel del VFO para el segmento de destino debe estar abierto. Si está contraído a una tira de solo frecuencia, haga clic en cualquier parte de la tira contraída para expandirla.

## Pasos

1. Haga clic en la bandera marcadora del VFO en la pantalla del espectro para el segmento que desea ajustar. El panel del VFO se abre anclado al marcador.
2. Haga clic en la pestaña **Audio** dentro del panel del VFO.
3. Para establecer el nivel de salida de audio, arrastre el control deslizante **AF Gain** hacia la izquierda o derecha. El valor predeterminado es 100; el rango válido es 0–100.
4. Para establecer la posición estéreo, arrastre el control deslizante **Pan** hacia la izquierda o derecha. El valor predeterminado es 50 (centro); el rango válido es 0–100. Un valor inferior a 50 desplaza el audio hacia el canal izquierdo; superior a 50 hacia el derecho.

## Qué hace cada control

| Control | Valor predeterminado | Rango |
|---|---|---|
| Control deslizante AF Gain (pestaña Audio) | 100 | 0–100 |
| Control deslizante Pan (pestaña Audio) | 50 | 0–100 |
| Botón Mute (pestaña Audio) | desactivado | — |
| Botón + control deslizante Squelch (pestaña Audio) | desactivado | 0–100 |
| Combinación AGC (pestaña Audio) | FAST | FAST \| MED \| SLOW \| OFF |
| Botón ADSP (pestaña DSP) | Abre el cuadro de diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Ajustes (v0.9.8). | Estilizado como un conmutador de DSP del lado del equipo pero no seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Conmuta la tira de canales de audio Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | desactivado | Activa el algoritmo de reducción de ruido correspondiente para este segmento. La disponibilidad del botón depende de la serie del equipo y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón de antena RX | — | Abre el menú de selección de antena para la antena receptora de este segmento. |
| Botón de antena TX | — | Abre el menú de selección de antena para la antena transmisora de este segmento. |
| Pantalla de frecuencia | — | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones preestablecidos del filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, solucionando un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Combinación Mode (pestaña Mode) | USB | USB \| LSB \| CW \| CWL \| AM \| SAM \| DIGU \| DIGL \| FM \| NFM \| DFM \| RTTY |
| Botones preestablecidos de filtro (pestaña Mode) | — | Aplica un ancho de filtro preestablecido guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. Los bordes inferior/superior personalizados se pueden establecer por ranura mediante clic derecho. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | desactivado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del mouse ajusta en pasos de 10 Hz. |
| Combinación de canal DAX (pestaña DAX) | Off | Off \| 1–8 |
| Botón de grosor del marcador | 1 px | Off \| 1 px \| 3 px. Recorre cíclicamente estas opciones para la línea marcadora del VFO. Se conserva por segmento. |
| Botón de bordes del filtro | mostrado | Conmuta las líneas de borde del filtro en la banda pasante del espectro. Se conserva por segmento. |
| Conmutador de contracción | expandido | Contrae el panel del VFO a una tira compacta de solo frecuencia. Se conserva por segmento. |
| Distintivo TX | — | Se muestra (rojo) cuando este segmento es el segmento transmisor activo. |
| Distintivo SPLIT | — | Se muestra (ámbar) cuando TX está asignado a un segmento diferente al segmento receptor activo. |

## Consejos

- Haga doble clic en cualquiera de los controles deslizantes para restablecerlo a su valor predeterminado: 100 para AF Gain, 50 para Pan.
- La ganancia de AF es por segmento. Ajustar un segmento no afecta a ningún otro segmento.
- Para silenciar un segmento sin mover el control deslizante AF Gain, utilice el **botón Mute** en la pestaña Audio. Silenciar no cambia el valor de ganancia almacenado.

## Marca central del control deslizante Pan (v26.6.1)

El control deslizante Pan ahora dibuja un punto de marca central en la ranura y rellena la ranura desde el centro hacia afuera cuando el control está descentrado. Esto proporciona una indicación visual clara de la posición neutra. El relleno utiliza el color de acento del tema en el lado hacia el que se mueve el control, y el color de fondo en el lado opuesto.

## Cambios en la etiqueta de ancho de filtro en v0.9.8

La etiqueta de ancho de filtro ahora utiliza `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto soluciona un desplazamiento de 0.1 kHz que anteriormente afectaba las lecturas en modo SSB y digital (#2197, v0.9.8). La etiqueta ahora se mantiene sincronizada con la lectura del filtro en el applet de RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

El botón y el control deslizante de squelch ahora están deshabilitados en modo RTTY, además de los modos digital y CW. Esto evita que el squelch cierre las señales FSK débiles cuando el audio alimenta decodificadores externos a través de DAX (#2504).

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel del VFO muestra los siguientes botones de reducción de ruido cuando están disponibles en el equipo:

| Botón | Algoritmo |
|---|---|
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

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de Configuración de AetherDSP para ese algoritmo.

### Botón ADSP (v0.9.8)

La pestaña DSP ahora incluye un **botón ADSP** que abre el cuadro de diálogo de Configuración de AetherDSP. Este botón proporciona el mismo punto de entrada que el menú Ajustes. Está estilizado como un conmutador de DSP del lado del equipo pero no es seleccionable. Haga clic para abrir y enfocar el cuadro de diálogo no modal de Configuración de AetherDSP.

### Botón AetherVoice (v0.9.8)

La pestaña DSP también incluye un **botón AetherVoice** que conmuta la tira de canales de audio Aetherial, el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula de DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

### Control deslizante de nivel DSP

Un control deslizante de nivel compartido ahora aparece debajo de la cuadrícula de botones DSP. El control deslizante se reorienta automáticamente al algoritmo DSP con nivel que se habilitó más recientemente. La etiqueta a la izquierda del control deslizante muestra el nombre del algoritmo actualmente seleccionado, y el valor numérico se muestra a la derecha.

Cambio importante en v0.9.8: El control deslizante de nivel DSP ahora aparece correctamente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado del equipo. Anteriormente, el control deslizante faltaba hasta que se conmutaba manualmente el algoritmo (#startup-slider). Esto afecta a NB, NR, ANF, NRL, NRS, NRF y ANFL.

La fila del control deslizante permanece disponible en todo momento. Cuando no hay ningún algoritmo con nivel activo, o cuando solo RNN, ANFT o APF están activados, la fila del control deslizante se atenúa y no responde a los clics.

| Control | Rango | Comportamiento |
|---|---|---|
| Control deslizante de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP con nivel habilitado más recientemente. Se reorienta automáticamente al cambiar de algoritmo. Oculto (atenuado) cuando no hay ningún algoritmo con nivel activo. |

## Selección de antena (v26.5.2.1)

Los botones de antena RX y antena TX abren menús contextuales que muestran los puertos de antena disponibles para el segmento actual.

- El menú de antena RX muestra las antenas de la lista de antenas RX dedicadas del segmento cuando esté disponible, recurriendo a la lista global de antenas.
- El menú de antena TX filtra automáticamente los puertos de antena de solo RX. Los puertos de antena que comienzan con "RX" se excluyen de la selección de TX.
- Cada entrada del menú muestra el nombre de la antena. La antena actualmente seleccionada está marcada con una marca de verificación.

## Indicadores del panel VFO

El panel del VFO incluye dos indicadores que aparecen cuando se cumplen ciertas condiciones:

- **Distintivo TX (rojo)**: Se muestra cuando este segmento es el segmento transmisor activo.
- **Distintivo SPLIT (ámbar)**: Se muestra cuando TX está asignado a un segmento diferente al segmento receptor activo.

El distintivo del segmento muestra la letra del segmento y utiliza formato de texto enriquecido para una representación adecuada.

## Entrada de frecuencia para bandas XVTR (v26.5.2.1)

Al introducir frecuencias en bandas XVTR (frecuencia del segmento superior a 54 MHz o antena RX que comienza con "XVT"):

- La frecuencia máxima aceptada es 50000 MHz.
- Para segmentos en el rango de 100–999 MHz (bandas de 2m/70cm), los números enteros sin formato se formatean automáticamente con un decimal después del tercer dígito. Por ejemplo, al ingresar 1446 se convierte en 144.6, 14696 se convierte en 146.96 y 144600 se convierte en 144.600.
- Para bandas de microondas (23 cm y superiores, 1000 MHz y más), los números enteros sin formato se tratan como el valor exacto en MHz. Por ejemplo, 1296 se convierte en 1296 MHz.

## Entrada de frecuencia con MHz explícito (v26.5.3)

Al introducir frecuencias, el panel del VFO utiliza `FrequencyEntryParser` para un análisis preciso. Si introduce una frecuencia explícitamente en MHz (p. ej., 146.520 o 144.390), la entrada se acepta como MHz incluso si el valor supera los 54 MHz. Esto permite la entrada directa en MHz para frecuencias de VHF y UHF sin requerir la detección de banda XVTR.

## Comportamiento del segmento bloqueado (v26.5.3)

Cuando un segmento está bloqueado:
- El **botón Lock VFO** en el panel del VFO muestra un icono de candado. Al hacer clic en el botón, se conmuta el estado de bloqueo.
- Cuando está bloqueado, la pantalla de frecuencia muestra un indicador de superposición de bloqueo.
- La sintonización con la rueda del mouse está bloqueada. Si intenta desplazarse mientras está bloqueado, el segmento emite una notificación de "sintonización bloqueada por bloqueo".
- La entrada directa de frecuencia está bloqueada. Cualquier entrada directa en curso se cancela cuando el segmento se bloquea.
- El panel del VFO actualiza la etiqueta de frecuencia para mostrar el estado de bloqueo.

## Temas y estilo de botones (v26.6.1)

- El panel del VFO utiliza el contenedor de temas `spectrum/vfo`. Esto mantiene las banderas del VFO en su propia superficie de temas, separada del alcance principal del espectro.
- El **botón de grosor del marcador** ahora utiliza colores conscientes del tema para su fondo y estados presionados: `color.background.1` para fondos normales y de desplazamiento, `color.accent` para el estado presionado.

## Corrección de altura de la pila de pestañas (v26.5.3)

El contenido de la pestaña del panel del VFO ahora se dimensiona correctamente al contenido de la pestaña actual. Esto soluciona un espacio que podía aparecer dentro de la pestaña Mode cuando la pestaña DSP era más alta (p. ej., cuando el submódulo DIGU/DIGL era visible). La pila de pestañas ahora informa solo el tamaño preferido de la página actual en lugar del máximo de todas las páginas.

## Accesibilidad de botones de pestaña y acceso directo de silencio (v26.6.3)

Las etiquetas de las pestañas del panel del VFO se han cambiado de `QLabel` a `QPushButton` con un estilo plano y seleccionable. Esto mejora la accesibilidad y la navegación con teclado:

- Cada pestaña ahora es accesible mediante la tecla Tab en el orden de enfoque.
- La pestaña activa utiliza un indicador de enfoque (borde inferior en color de acento) para el seguimiento visual del enfoque.
- Haga clic derecho en el icono del altavoz de la pestaña (pestaña Audio) para conmutar el silencio directamente sin cambiar a la pestaña Audio.

## Dirección de sintonización con la rueda del mouse (v26.6.3)

El panel del VFO ahora respeta la configuración **Invertir dirección de la rueda del mouse** de `InteractionSettings`. Cuando la configuración está habilitada, la dirección de sintonización efectiva por paso de desplazamiento se invierte. Esto afecta a toda la sintonización con la rueda del mouse en el panel del V
