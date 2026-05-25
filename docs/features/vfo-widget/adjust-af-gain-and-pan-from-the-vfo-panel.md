# Ajustar la ganancia de AF y la panoramización desde el panel VFO

Utilice la pestaña Audio en el panel VFO para configurar el nivel de salida de audio y la posición estéreo de cualquier receptor de forma independiente de otros receptores.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del receptor deseado debe estar abierto. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier parte de la tira colapsada para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO en el visualizador de espectro del receptor que desea ajustar. El panel VFO se abre anclado al marcador.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Para configurar el nivel de salida de audio, arrastre el **control deslizante AF Gain** hacia la izquierda o derecha. El valor predeterminado es 100; el rango válido es de 0 a 100.
4. Para configurar la posición estéreo, arrastre el **control deslizante Pan** hacia la izquierda o derecha. El valor predeterminado es 50 (centro); el rango válido es de 0 a 100. Un valor inferior a 50 desplaza el audio hacia el canal izquierdo; superior a 50 hacia el derecho.

## Qué hace cada control

| Control | Predeterminado | Rango |
|---|---|---|
| Control deslizante AF Gain (pestaña Audio) | 100 | 0–100 |
| Control deslizante Pan (pestaña Audio) | 50 | 0–100 |
| Botón Mute (pestaña Audio) | desactivado | — |
| Botón + control deslizante Squelch (pestaña Audio) | desactivado | 0–100 |
| Combinación AGC (pestaña Audio) | FAST | FAST \| MED \| SLOW \| OFF |
| Botón ADSP (pestaña DSP) | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un conmutador DSP del lado de la radio pero sin capacidad de selección. Al hacer clic, levanta y enfoca el diálogo no modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP) | Conmuta la tira de canal de audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | desactivado | Activa el algoritmo de reducción de ruido correspondiente para este receptor. La disponibilidad del botón depende de la serie de la radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo AetherDSP Settings para ese algoritmo. |
| Botón de antena RX | — | Abre el menú de selección de antena para la antena receptora de este receptor. |
| Botón de antena TX | — | Abre el menú de selección de antena para la antena transmisora de este receptor. |
| Visualización de frecuencia | — | Muestra la frecuencia actual del receptor. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Combinación Mode (pestaña Mode) | USB | USB \| LSB \| CW \| CWL \| AM \| SAM \| DIGU \| DIGL \| FM \| NFM \| DFM \| RTTY |
| Botones preestablecidos de filtro (pestaña Mode) | — | Aplica un ancho de filtro guardado preestablecido. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. Los bordes lo/hi personalizados se pueden configurar por ranura mediante clic derecho. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | desactivado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| Combinación de canal DAX (pestaña DAX) | Off | Off \| 1–8 |
| Botón de grosor del marcador | 1 px | Off \| 1 px \| 3 px. Recorre la línea del marcador VFO a través de estas opciones. Se conserva por receptor. |
| Botón de bordes del filtro | mostrado | Conmuta las líneas de borde del filtro en la banda pasante del espectro. Se conserva por receptor. |
| Conmutador de colapso | expandido | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se conserva por receptor. |
| Distintivo TX | — | Se muestra (rojo) cuando este receptor es el receptor de transmisión activo. |
| Distintivo SPLIT | — | Se muestra (ámbar) cuando TX está asignado a un receptor diferente al receptor de recepción activo. |

## Consejos

- Hacer doble clic en cualquier control deslizante lo restablece a su valor predeterminado: 100 para AF Gain, 50 para Pan.
- La ganancia AF es por receptor. Ajustar un receptor no afecta a ningún otro.
- Para silenciar un receptor sin mover el control deslizante AF Gain, utilice el **botón Mute** en la pestaña Audio. Silenciar no cambia el valor de ganancia almacenado.

## Cambios en la etiqueta de ancho de filtro en v0.9.8

La etiqueta de ancho de filtro ahora utiliza `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desplazamiento de 0.1 kHz que afectaba anteriormente las lecturas en modo SSB y digital (#2197, v0.9.8). La etiqueta ahora se mantiene sincronizada con la lectura del filtro en el applet RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

El botón y control deslizante Squelch ahora están deshabilitados en modo RTTY, además de los modos digital y CW. Esto evita que el squelch obstruya las señales FSK débiles cuando el audio alimenta decodificadores externos a través de DAX (#2504).

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

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo AetherDSP Settings para ese algoritmo.

### Botón ADSP (v0.9.8)

La pestaña DSP ahora incluye un **botón ADSP** que abre el diálogo AetherDSP Settings. Este botón proporciona el mismo punto de entrada que el menú Settings. Está estilizado como un conmutador DSP del lado de la radio pero no se puede marcar. Haga clic en él para levantar y enfocar el diálogo no modal AetherDSP Settings.

### Botón AetherVoice (v0.9.8)

La pestaña DSP también incluye un **botón AetherVoice** que conmuta la tira de canal de audio Aetherial — el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

### Control deslizante de nivel DSP

Ahora aparece un control deslizante de nivel compartido debajo de la cuadrícula de botones DSP. El control deslizante se reenfoca automáticamente al algoritmo DSP con nivel que se activó más recientemente. La etiqueta a la izquierda del control deslizante muestra el nombre del algoritmo actualmente seleccionado, y el valor numérico se muestra a la derecha.

Cambio importante en v0.9.8: El control deslizante de nivel DSP ahora aparece correctamente al inicio para cualquier DSP que estuviera activado en el perfil guardado de la radio. Anteriormente, el control deslizante faltaba hasta que se conmutaba manualmente el algoritmo (#startup-slider). Esto afecta a NB, NR, ANF, NRL, NRS, NRF y ANFL.

La fila del control deslizante permanece diseñada en todo momento. Cuando ningún algoritmo con nivel está activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del control deslizante se atenúa y no responde a los clics.

| Control | Rango | Comportamiento |
|---|---|---|
| Control deslizante de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP con nivel activado más recientemente. Se reenfoca automáticamente cuando cambia de algoritmos. Oculto (atenuado) cuando ningún algoritmo con nivel está activo. |

## Selección de antena (v26.5.2.1)

Los botones de antena RX y TX abren menús contextuales que muestran los puertos de antena disponibles para el receptor actual.

- El menú de antena RX muestra las antenas de la lista de antenas RX dedicadas del receptor cuando están disponibles, recurriendo a la lista de antenas global.
- El menú de antena TX filtra automáticamente los puertos de antena solo RX. Los puertos de antena que comienzan con "RX" se excluyen de la selección TX.
- Cada entrada del menú muestra el nombre de la antena. La antena actualmente seleccionada está marcada con una marca de verificación.

## Indicadores del panel VFO

El panel VFO incluye dos indicadores que aparecen cuando se cumplen ciertas condiciones:

- **Distintivo TX (rojo)**: Se muestra cuando este receptor es el receptor de transmisión activo.
- **Distintivo SPLIT (ámbar)**: Se muestra cuando TX está asignado a un receptor diferente al receptor de recepción activo.

El distintivo del receptor muestra la letra del receptor y utiliza formato de texto enriquecido para una representación adecuada.

## Entrada de frecuencia para bandas XVTR (v26.5.2.1)

Al ingresar frecuencias en bandas XVTR (frecuencia del receptor superior a 54 MHz o antena RX que comienza con "XVT"):

- La frecuencia máxima aceptada es 50000 MHz.
- Para receptores en el rango de 100–999 MHz (bandas de 2m/70cm), los números enteros sin formato se formatean automáticamente con un decimal después del tercer dígito. Por ejemplo, ingresar 1446 se convierte en 144.6, 14696 se convierte en 146.96 y 144600 se convierte en 144.600.
- Para bandas de microondas (23 cm y superiores, 1000 MHz y más), los números enteros sin formato se tratan como el valor exacto en MHz. Por ejemplo, 1296 se convierte en 1296 MHz.

## Entrada de frecuencia con MHz explícito (v26.5.3)

Al ingresar frecuencias, el panel VFO utiliza `FrequencyEntryParser` para un análisis preciso. Si ingresa una frecuencia explícitamente en MHz (por ejemplo, 146.520 o 144.390), la entrada se acepta como MHz incluso si el valor supera los 54 MHz. Esto permite la entrada directa de MHz para frecuencias VHF y UHF sin requerir la detección de banda XVTR.

## Comportamiento del receptor bloqueado (v26.5.3)

Cuando un receptor está bloqueado:
- El **botón Lock VFO** en el panel VFO muestra un icono de candado. Al hacer clic en el botón, se conmuta el estado de bloqueo.
- Cuando está bloqueado, la pantalla de frecuencia muestra un indicador de superposición de bloqueo.
- La sintonización con la rueda del ratón está bloqueada. Si intenta desplazarse mientras está bloqueado, el receptor emite una notificación de "sintonización bloqueada por bloqueo".
- La entrada directa de frecuencia está bloqueada. Cualquier entrada directa en curso se cancela cuando el receptor está bloqueado.
- El panel VFO actualiza la etiqueta de frecuencia para mostrar el estado de bloqueo.

## Corrección de altura de la pila de pestañas (v26.5.3)

El contenido de las pestañas del panel VFO ahora se dimensiona correctamente al contenido de la pestaña actual. Esto corrige un espacio que podía aparecer dentro de la pestaña Mode cuando la pestaña DSP era más alta (por ejemplo, cuando el submódulo DIGU/DIGL era visible). La pila de pestañas ahora informa solo el tamaño preferido de la página actual en lugar del máximo de todas las páginas.

## Relacionados

- [Silenciar el audio de un receptor desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Activar el squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Resumen del panel VFO](overview.md)
