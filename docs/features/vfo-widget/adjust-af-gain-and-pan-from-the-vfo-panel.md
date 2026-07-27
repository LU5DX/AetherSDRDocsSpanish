# Ajustar el AF Gain y el Pan desde el panel VFO

Utilice la pestaña Audio en el panel VFO para establecer el nivel de salida de audio y la posición estéreo (pan) de cualquier slice de recepción de forma independiente de otros slices.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del slice de destino debe estar abierto. Si está colapsado en una tira que solo muestra la frecuencia, haga clic en cualquier lugar de la tira colapsada para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla de espectro para el slice que desea ajustar. Se abrirá el panel VFO anclado al marcador.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Para establecer el nivel de salida de audio, arrastre el **control deslizante de AF Gain** hacia la izquierda o la derecha. El valor predeterminado es 100; el rango válido es 0–100.
4. Para establecer la posición estéreo, arrastre el **control deslizante Pan** hacia la izquierda o la derecha. El valor predeterminado es 50 (centro); el rango válido es 0–100. Un valor inferior a 50 mueve el audio hacia el canal izquierdo; superior a 50, hacia el derecho.

## Qué hace cada control

| Control | Predeterminado | Rango |
|---|---|---|
| Control deslizante AF Gain (pestaña Audio) | 100 | 0–100 |
| Control deslizante Pan (pestaña Audio) | 50 | 0–100 |
| Botón Mute (pestaña Audio) | apagado | — |
| Botón + Control deslizante Squelch (pestaña Audio) | apagado | 0–100 |
| Combinado AGC (pestaña Audio) | FAST | FAST \| MED \| SLOW \| OFF |
| Botón ADSP (pestaña DSP) | Abre el diálogo Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Mismo punto de entrada que el menú Configuración (v0.9.8). | Tiene el estilo de un conmutador DSP del lado de la radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Conmuta la Tira de Canal de Audio Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | apagado | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo Configuración de AetherDSP para ese algoritmo. |
| Botón de antena RX | — | Abre el menú de selección de antena para la antena receptora de este slice. |
| Botón de antena TX | — | Abre el menú de selección de antena para la antena transmisora de este slice. |
| Pantalla de frecuencia | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar a escribir la frecuencia directamente; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Combinado Mode (pestaña Mode) | USB | USB \| LSB \| CW \| CWL \| AM \| SAM \| DIGU \| DIGL \| FM \| NFM \| DFM \| RTTY |
| Botones de preajuste de filtro (pestaña Mode) | — | Aplica un ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. Los bordes inferior/superior personalizados se pueden establecer por ranura mediante clic derecho. |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | apagado | Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| Combinado de canal DAX (pestaña DAX) | Off | Off \| 1–8 |
| Botón de grosor del marcador | 1 px | Off \| 1 px \| 3 px. Recorre estas opciones para la línea del marcador VFO. Se conserva por slice. |
| Botón de bordes del filtro | mostrado | Muestra u oculta las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice. |
| Conmutador de colapso | expandido | Colapsa el panel VFO a una tira compacta que solo muestra la frecuencia. Se conserva por slice. |
| Distintivo TX | — | Se muestra (rojo) cuando este slice es el slice de transmisión activo. |
| Distintivo SPLIT | — | Se muestra (ámbar) cuando TX está asignado a un slice diferente al slice de recepción activo. |

## Consejos

- Haga doble clic en cualquier control deslizante para restablecerlo a su valor predeterminado: 100 para AF Gain, 50 para Pan.
- El AF Gain es por slice. Ajustar un slice no afecta a ningún otro slice.
- Para silenciar un slice sin mover el control deslizante de AF Gain, use el **botón Mute** en la pestaña Audio en su lugar. Silenciar no cambia el valor de ganancia almacenado.

## Marca central del control deslizante Pan (v26.6.1)

El control deslizante Pan ahora pinta un punto de marca central en la ranura y rellena la ranura desde el centro hacia afuera cuando el mango está descentrado. Esto proporciona una indicación visual clara de la posición neutral. El relleno usa el color de acento del tema en el lado hacia el que se mueve el mango, y el color de fondo en el lado opuesto.

## Cambios en la etiqueta de ancho de filtro en v0.9.8

La etiqueta de ancho de filtro ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desplazamiento de 0.1 kHz que anteriormente afectaba las lecturas en modo SSB y digital (#2197, v0.9.8). La etiqueta ahora se mantiene sincronizada con la lectura del filtro en el applet RX.

## Comportamiento de Squelch para modo RTTY (v26.5.1)

El botón y el control deslizante de Squelch ahora están deshabilitados en modo RTTY, además de en modos digital y CW. Esto evita que el squelch bloquee señales FSK débiles cuando el audio alimenta decodificadores externos a través de DAX (#2504).

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

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo Configuración de AetherDSP para ese algoritmo.

### Botón ADSP (v0.9.8)

La pestaña DSP ahora incluye un **botón ADSP** que abre el diálogo Configuración de AetherDSP. Este botón proporciona el mismo punto de entrada que el menú Configuración. Tiene el estilo de un conmutador DSP del lado de la radio pero no es marcable. Haga clic en él para abrir y enfocar el diálogo no modal de Configuración de AetherDSP.

### Botón AetherVoice (v0.9.8)

La pestaña DSP también incluye un **botón AetherVoice** que conmuta la Tira de Canal de Audio Aetherial, el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

### Control deslizante de nivel DSP

Un control deslizante de nivel compartido aparece ahora debajo de la cuadrícula de botones DSP. El control deslizante se reorienta automáticamente al algoritmo DSP con nivel que se habilitó más recientemente. La etiqueta a la izquierda del control deslizante muestra el nombre del algoritmo actualmente seleccionado, y el valor numérico se muestra a la derecha.

Cambio importante en v0.9.8: El control deslizante de nivel DSP ahora aparece correctamente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado de la radio. Anteriormente, el control deslizante faltaba hasta que se conmutaba manualmente el algoritmo (#startup-slider). Esto afecta a NB, NR, ANF, NRL, NRS, NRF y ANFL.

La fila del control deslizante permanece diseñada en todo momento. Cuando ningún algoritmo con nivel está activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del control deslizante se atenúa y no responde a los clics.

| Control | Rango | Comportamiento |
|---|---|---|
| Control deslizante de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP con nivel habilitado más recientemente. Se reorienta automáticamente cuando cambia de algoritmo. Oculto (atenuado) cuando ningún algoritmo con nivel está activo. |

## Selección de antena (v26.5.2.1)

Los botones de antena RX y TX abren menús contextuales que muestran los puertos de antena disponibles para el slice actual.

- El menú de antena RX muestra las antenas de la lista de antenas RX dedicadas del slice cuando está disponible, recurriendo a la lista global de antenas.
- El menú de antena TX filtra automáticamente los puertos de antena solo de RX. Los puertos de antena que comienzan con "RX" se excluyen de la selección TX.
- Cada entrada del menú muestra el nombre de la antena. La antena actualmente seleccionada está marcada con una marca de verificación.

## Indicadores del panel VFO

El panel VFO incluye dos indicadores que aparecen cuando se cumplen ciertas condiciones:

- **Distintivo TX (rojo)**: Se muestra cuando este slice es el slice de transmisión activo.
- **Distintivo SPLIT (ámbar)**: Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo.

El distintivo del slice muestra la letra del slice y usa formato de texto enriquecido para una representación adecuada.

## Ingreso de frecuencia para bandas XVTR (v26.5.2.1)

Al ingresar frecuencias en bandas XVTR (frecuencia de slice superior a 54 MHz o antena RX que comienza con "XVT"):

- La frecuencia máxima aceptada es 50000 MHz.
- Para slices en el rango de 100–999 MHz (bandas de 2m/70cm), los números enteros se formatean automáticamente con un decimal después del tercer dígito. Por ejemplo, al ingresar 1446 se convierte en 144.6, 14696 se convierte en 146.96 y 144600 se convierte en 144.600.
- Para bandas de microondas (23cm y superiores, 1000 MHz o más), los números enteros se tratan como el valor exacto en MHz. Por ejemplo, 1296 se convierte en 1296 MHz.

## Ingreso de frecuencia con MHz explícito (v26.5.3)

Al ingresar frecuencias, el panel VFO usa `FrequencyEntryParser` para un análisis preciso. Si ingresa una frecuencia explícitamente en MHz (por ejemplo, 146.520 o 144.390), la entrada se acepta como MHz incluso si el valor supera los 54 MHz. Esto permite el ingreso directo en MHz para frecuencias VHF y UHF sin requerir la detección de banda XVTR.

## Comportamiento de slice bloqueado (v26.5.3)

Cuando un slice está bloqueado:
- El **botón Lock VFO** en el panel VFO muestra un icono de candado. Al hacer clic en el botón se conmuta el estado de bloqueo.
- Cuando está bloqueado, la pantalla de frecuencia muestra un indicador de superposición de bloqueo.
- La sintonización con la rueda del ratón está bloqueada. Si intenta desplazarse mientras está bloqueado, el slice emite una notificación de "sintonización bloqueada por bloqueo".
- El ingreso directo de frecuencia está bloqueado. Cualquier ingreso directo en curso se cancela cuando el slice se bloquea.
- El panel VFO actualiza la etiqueta de frecuencia para mostrar el estado de bloqueo.

## Temas y estilo de botones (v26.6.1)

- El panel VFO usa el contenedor de temas `spectrum/vfo`. Esto mantiene las banderas VFO en su propia superficie de tema, separada del ámbito del espectro principal.
- El **botón de grosor del marcador** ahora usa colores conscientes del tema para su fondo y estados presionados: `color.background.1` para fondos normales y al pasar el ratón, `color.accent` para el estado presionado.

## Corrección de altura de pila de pestañas (v26.5.3)

El contenido de las pestañas del panel VFO ahora se ajusta correctamente al tamaño del contenido de la pestaña actual. Esto corrige un espacio que podía aparecer dentro de la pestaña Mode cuando la pestaña DSP era más alta (por ejemplo, cuando el sub-modo DIGU/DIGL era visible). La pila de pestañas ahora informa solo el tamaño preferido de la página actual en lugar del máximo de todas las páginas.

## Accesibilidad del botón de pestaña y acceso directo de silencio (v26.6.3)

Las etiquetas de las pestañas del panel VFO se han cambiado de `QLabel` a `QPushButton` con un estilo plano y marcable. Esto mejora la accesibilidad y la navegación por teclado:

- Cada pestaña ahora es accesible mediante la tecla Tab en el orden de enfoque.
- La pestaña activa usa un indicador de enfoque (borde inferior en color de acento) para el seguimiento visual del enfoque.
- Haga clic derecho en el icono del altavoz de la pestaña (pestaña Audio) para conmutar el silencio directamente sin cambiar a la pestaña Audio.

## Dirección de sintonización con la rueda del ratón (v26.6.3)

El panel VFO ahora respeta la configuración **Invertir dirección de la rueda del ratón** de `InteractionSettings`. Cuando la configuración está habilitada, la dirección de sintonización efectiva por paso de desplazamiento se invierte. Esto afecta a toda la sintonización con la rueda del panel VFO, independientemente del objetivo de desplazamiento.

## Anuncios de frecuencia de accesibilidad (v26.6.3)

El panel VFO ahora proporciona anuncios de frecuencia de accesibilidad cuando la tecnología de asistencia (por ejemplo, un lector de pantalla) está activa. La etiqueta de frecuencia dispara un `QAccessibleValueChangeEvent` a
