# Ajustar la ganancia de AF y la panoramización desde el panel VFO

Use la pestaña Audio en el panel VFO para establecer el nivel de salida de audio y la posición de panoramización estéreo de cualquier segmento de recepción de forma independiente de otros segmentos.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO para el segmento objetivo debe estar abierto. Si está colapsado a una tira solo de frecuencia, haga clic en cualquier parte de la tira colapsada para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla del espectrograma para el segmento que desea ajustar. El panel VFO se abre anclado al marcador.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Para establecer el nivel de salida de audio, arrastre el **control deslizante de Ganancia AF** hacia la izquierda o la derecha. El valor predeterminado es 100; el rango válido es 0–100.
4. Para establecer la posición estéreo, arrastre el **control deslizante de Pan** hacia la izquierda o la derecha. El valor predeterminado es 50 (centro); el rango válido es 0–100. Un valor inferior a 50 mueve el audio hacia el canal izquierdo; superior a 50 hacia el derecho.

## Qué hace cada control

| Control | Valor predeterminado | Rango |
|---|---|---|
| Control deslizante de Ganancia AF (pestaña Audio) | 100 | 0–100 |
| Control deslizante de Pan (pestaña Audio) | 50 | 0–100 |
| Botón Silenciar (pestaña Audio) | desactivado | — |
| Botón y control deslizante de Squelch (pestaña Audio) | desactivado | 0–100 |
| Combinación AGC (pestaña Audio) | RÁPIDO | RÁPIDO \| MED \| LENTO \| APAGADO |
| Botón ADSP (pestaña DSP) | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Configuración (v0.9.8). | Con estilo de conmutador DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna la Tira de Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | desactivado | Activa el algoritmo de reducción de ruido correspondiente para este segmento. La disponibilidad del botón depende de la serie de la radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón de antena RX | — | Abre el menú de selección de antena para la antena receptora de este segmento. |
| Botón de antena TX | — | Abre el menú de selección de antena para la antena transmisora de este segmento. |
| Pantalla de frecuencia | — | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Modo. Usa `RxApplet::formatFilterWidth` como la única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Combinación de Modo (pestaña Modo) | USB | USB \| LSB \| CW \| CWL \| AM \| SAM \| DIGU \| DIGL \| FM \| NFM \| DFM \| RTTY |
| Botones de preajuste de filtro (pestaña Modo) | — | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. Los bordes lo/hi personalizados se pueden establecer por ranura mediante clic derecho. |
| Botones y etiquetas de RIT / XIT (pestaña X/RIT) | desactivado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| Combinación de canal DAX (pestaña DAX) | Apagado | Apagado \| 1–8 |
| Botón de grosor del marcador | 1 px | Apagado \| 1 px \| 3 px. Recorre la línea del marcador VFO a través de estas opciones. Se conserva por segmento. |
| Botón de bordes del filtro | mostrado | Alterna las líneas de borde del filtro en la banda pasante del espectrograma. Se conserva por segmento. |
| Alternar colapso | expandido | Colapsa el panel VFO a una tira compacta solo de frecuencia. Se conserva por segmento. |
| Distintivo TX | — | Se muestra (rojo) cuando este segmento es el segmento de transmisión activo. |
| Distintivo SPLIT | — | Se muestra (ámbar) cuando TX está asignado a un segmento diferente al segmento de recepción activo. |

## Consejos

- Al hacer doble clic en cualquiera de los controles deslizantes, se restablece a su valor predeterminado: 100 para Ganancia AF, 50 para Pan.
- La ganancia AF es por segmento. Ajustar un segmento no afecta a ningún otro segmento.
- Para silenciar un segmento sin mover el control deslizante de Ganancia AF, use el **botón Silenciar** en la pestaña Audio en su lugar. Silenciar no cambia el valor de ganancia almacenado.

## Marca central del control deslizante Pan (v26.6.1)

El control deslizante Pan ahora dibuja un punto de marca central en la ranura y llena la ranura desde el centro hacia afuera cuando el mango está descentrado. Esto proporciona una indicación visual clara de la posición neutra. El relleno usa el color de acento del tema en el lado hacia el cual se mueve el mango, y el color de fondo en el lado opuesto.

## Cambios en la etiqueta de ancho de filtro en v0.9.8

La etiqueta de ancho de filtro ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desplazamiento de 0.1 kHz que anteriormente afectaba las lecturas en modo SSB y digital (#2197, v0.9.8). La etiqueta ahora se mantiene sincronizada con la lectura del filtro en el applet RX.

## Comportamiento de Squelch para modo RTTY (v26.5.1)

El botón y el control deslizante de Squelch ahora están deshabilitados en modo RTTY, además de los modos digital y CW. Esto evita que el squelch bloquee señales FSK débiles cuando el audio alimenta decodificadores externos a través de DAX (#2504).

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO muestra los siguientes botones de reducción de ruido cuando están disponibles desde la radio:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Eliminador de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo.

### Botón ADSP (v0.9.8)

La pestaña DSP ahora incluye un **botón ADSP** que abre el diálogo de Configuración de AetherDSP. Este botón proporciona el mismo punto de entrada que el menú Configuración. Tiene el estilo de un conmutador DSP del lado de la radio pero no es marcable. Haga clic en él para abrir y enfocar el diálogo no modal de Configuración de AetherDSP.

### Botón AetherVoice (v0.9.8)

La pestaña DSP también incluye un **botón AetherVoice** que alterna la Tira de Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

### Control deslizante de nivel DSP

Un control deslizante de nivel compartido ahora aparece debajo de la cuadrícula de botones DSP. El control deslizante se reorienta automáticamente al algoritmo DSP con nivel que se habilitó más recientemente. La etiqueta a la izquierda del control deslizante muestra el nombre del algoritmo actualmente dirigido, y el valor numérico se muestra a la derecha.

Cambio importante en v0.9.8: El control deslizante de nivel DSP ahora aparece correctamente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado de la radio. Anteriormente, el control deslizante faltaba hasta que se alternaba manualmente el algoritmo (#startup-slider). Esto afecta a NB, NR, ANF, NRL, NRS, NRF y ANFL.

La fila del control deslizante permanece dispuesta en todo momento. Cuando ningún algoritmo con nivel está activo — o cuando solo RNN, ANFT o APF está encendido — la fila del control deslizante se atenúa y no responde a los clics.

| Control | Rango | Comportamiento |
|---|---|---|
| Control deslizante de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP con nivel habilitado más recientemente. Se reorienta automáticamente cuando cambia de algoritmos. Oculto (atenuado) cuando ningún algoritmo con nivel está activo. |

## Selección de antena (v26.5.2.1)

Los botones de antena RX y antena TX abren menús contextuales que muestran los puertos de antena disponibles para el segmento actual.

- El menú de antena RX muestra antenas de la lista de antenas RX dedicadas del segmento cuando estén disponibles, recurriendo a la lista de antenas global.
- El menú de antena TX filtra automáticamente los puertos de antena solo de RX. Los puertos de antena que comienzan con "RX" se excluyen de la selección de TX.
- Cada entrada del menú muestra el nombre de la antena. La antena actualmente seleccionada está marcada con una marca de verificación.

## Indicadores del panel VFO

El panel VFO incluye dos indicadores que aparecen cuando se cumplen ciertas condiciones:

- **Distintivo TX (rojo)**: Se muestra cuando este segmento es el segmento de transmisión activo.
- **Distintivo SPLIT (ámbar)**: Se muestra cuando TX está asignado a un segmento diferente al segmento de recepción activo.

El distintivo del segmento muestra la letra del segmento y usa formato de texto enriquecido para una representación adecuada.

## Entrada de frecuencia para bandas XVTR (v26.5.2.1)

Al introducir frecuencias en bandas XVTR (frecuencia del segmento superior a 54 MHz o antena RX que comienza con "XVT"):

- La frecuencia máxima aceptada es de 50000 MHz.
- Para segmentos en el rango de 100–999 MHz (bandas de 2m/70cm), los enteros simples se formatean automáticamente con un decimal después del tercer dígito. Por ejemplo, al introducir 1446 se convierte en 144.6, 14696 se convierte en 146.96 y 144600 se convierte en 144.600.
- Para bandas de microondas (23 cm y superiores, 1000 MHz y más), los enteros simples se tratan como el valor exacto en MHz. Por ejemplo, 1296 se convierte en 1296 MHz.

## Entrada de frecuencia con MHz explícito (v26.5.3)

Al introducir frecuencias, el panel VFO usa `FrequencyEntryParser` para un análisis preciso. Si introduce una frecuencia explícitamente en MHz (por ejemplo, 146.520 o 144.390), la entrada se acepta como MHz incluso si el valor supera los 54 MHz. Esto permite la entrada directa en MHz para frecuencias VHF y UHF sin requerir la detección de banda XVTR.

## Comportamiento del segmento bloqueado (v26.5.3)

Cuando un segmento está bloqueado:
- El **botón Bloquear VFO** en el panel VFO muestra un icono de candado. Al hacer clic en el botón, se alterna el estado de bloqueo.
- Cuando está bloqueado, la pantalla de frecuencia muestra un indicador de superposición de bloqueo.
- La sintonización con la rueda del ratón está bloqueada. Si intenta desplazarse mientras está bloqueado, el segmento emite una notificación de "sintonización bloqueada por bloqueo".
- La entrada directa de frecuencia está bloqueada. Cualquier entrada directa en curso se cancela cuando el segmento está bloqueado.
- El panel VFO actualiza la etiqueta de frecuencia para mostrar el estado de bloqueo.

## Tematización y estilo de botones (v26.6.1)

- El panel VFO usa el contenedor de tematización `spectrum/vfo`. Esto mantiene las banderas VFO en su propia superficie de tematización, separada del alcance principal del espectrograma.
- El **botón de Grosor del Marcador** ahora usa colores conscientes del tema para sus fondos y estados presionados: `color.background.1` para fondos normales y de desplazamiento, `color.accent` para el estado presionado.

## Corrección de altura de la pila de pestañas (v26.5.3)

El contenido de la pestaña del panel VFO ahora se ajusta correctamente al contenido de la pestaña actual. Esto corrige un espacio que podía aparecer dentro de la pestaña Modo cuando la pestaña DSP era más alta (por ejemplo, cuando el sub-modo DIGU/DIGL era visible). La pila de pestañas ahora informa solo el tamaño preferido de la página actual en lugar del máximo de todas las páginas.

## Relacionado

- [Silenciar audio para un segmento desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Activar squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)
