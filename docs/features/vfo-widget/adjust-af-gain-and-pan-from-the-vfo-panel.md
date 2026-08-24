# Ajuste de ganancia de AF y paneo desde el panel VFO

Use la pestaña Audio en el panel VFO para establecer el nivel de salida de audio y la posición de paneo estéreo para cualquier slice de recepción, independientemente de otros slices.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del slice objetivo debe estar abierto. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier lugar de la tira colapsada para expandirla.

## Pasos

1. Haga clic en el marcador VFO en la pantalla del espectro para el slice que desea ajustar. El panel VFO se abre anclado al marcador.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Para establecer el nivel de salida de audio, arrastre el **control deslizante de ganancia AF** hacia la izquierda o la derecha. El valor predeterminado es 100; el rango válido es 0–100.
4. Para establecer la posición estéreo, arrastre el **control deslizante de pan** hacia la izquierda o la derecha. El valor predeterminado es 50 (centro); el rango válido es 0–100. Un valor inferior a 50 mueve el audio hacia el canal izquierdo; superior a 50, hacia el derecho.

## Función de cada control

| Control | Predeterminado | Rango |
|---|---|---|
| Control deslizante de ganancia AF (pestaña Audio) | 100 | 0–100 |
| Control deslizante de pan (pestaña Audio) | 50 | 0–100 |
| Botón de silencio (pestaña Audio) | desactivado | — |
| Botón y control deslizante de squelch (pestaña Audio) | desactivado | 0–100 |
| Combinación AGC (pestaña Audio) | FAST | FAST \| MED \| SLOW \| OFF |
| Botón ADSP (pestaña DSP) | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de conmutador DSP del lado de la radio, pero no marcable. Haga clic para elevar y enfocar el diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna la tira de canales de audio Aetherial — la suite unificada de DSP TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | desactivado | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de la radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón MN (pestaña DSP) | desactivado | Activa el filtro de muesca manual para este slice. Solo se muestra en radios que admiten filtrado de muesca manual. Establece el nivel mediante el control deslizante de nivel DSP compartido. |
| Botón de antena RX | — | Abre el menú de selección de antena para la antena receptora de este slice. |
| Botón de antena TX | — | Abre el menú de selección de antena para la antena transmisora de este slice. |
| Pantalla de frecuencia | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba los MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0,1 kHz que afectaba las lecturas de modo SSB/digital (#2197, v0.9.8). |
| Combinación de modo (pestaña Mode) | USB | USB \| LSB \| CW \| CWL \| AM \| SAM \| DIGU \| DIGL \| FM \| NFM \| DFM \| RTTY |
| Botones preestablecidos de filtro (pestaña Mode) | — | Aplica un ancho de filtro preestablecido guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. Se pueden configurar bordes lo/hi personalizados por ranura mediante clic derecho. |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | desactivado | Activa el sintonizado incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| Combinación de canal DAX (pestaña DAX) | Off | Off \| 1–8 |
| Botón de grosor de marcador | 1 px | Off \| 1 px \| 3 px. Recorre las opciones de la línea del marcador VFO. Se conserva por slice. |
| Botón de bordes de filtro | mostrado | Alterna las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice. |
| Conmutador de colapso | expandido | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se conserva por slice. |
| Insignia TX | — | Se muestra (roja) cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | — | Se muestra (ámbar) cuando TX está asignado a un slice diferente del slice de recepción activo. |

## Consejos

- Haga doble clic en cualquiera de los controles deslizantes para restablecer su valor predeterminado: 100 para ganancia AF, 50 para pan.
- La ganancia AF es por slice. Ajustar un slice no afecta a ningún otro.
- Para silenciar un slice sin mover el control deslizante de ganancia AF, use el **botón de silencio** en la pestaña Audio. Silenciar no cambia el valor de ganancia almacenado.

## Marca central del control deslizante de pan (v26.6.1)

El control deslizante de pan ahora dibuja un punto de marca central en la ranura y llena la ranura desde el centro hacia afuera cuando el control está descentrado. Esto proporciona una indicación visual clara de la posición neutra. El relleno usa el color de acento del tema en el lado hacia el cual se mueve el control, y el color de fondo en el lado opuesto.

## Cambios en la etiqueta de ancho de filtro en v0.9.8

La etiqueta de ancho de filtro ahora usa `RxApplet::formatFilterWidth` como única fuente de verdad. Esto corrige un desfase de 0,1 kHz que anteriormente afectaba las lecturas de modo SSB y digital (#2197, v0.9.8). La etiqueta ahora permanece sincronizada con la lectura del filtro en el applet RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

El botón y el control deslizante de squelch ahora están deshabilitados en modo RTTY, además de los modos digital y CW. Esto evita que el squelch enmascare señales FSK débiles cuando el audio alimenta decodificadores externos mediante DAX (#2504).

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO muestra los siguientes botones de reducción de ruido cuando están disponibles desde la radio:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Eliminador de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (solo modo CW) |
| MN | Filtro de muesca manual |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo.

### Botón de filtro de muesca manual (MN) (v26.8.4)

La pestaña DSP ahora incluye un **botón de filtro de muesca manual (MN)** que activa el filtro de muesca manual para el slice actual. Este botón solo se muestra en radios que informan soporte para filtrado de muesca manual (`hasManualNotch`). Cuando está activado, el nivel del filtro de muesca se puede ajustar con el control deslizante de nivel DSP compartido.

El botón MN usa un nombre de objeto estable (`dspMNBtn`) para el puente de automatización, consistente con otros conmutadores DSP en esta pestaña.

### Botón ADSP (v0.9.8)

La pestaña DSP ahora incluye un **botón ADSP** que abre el diálogo de Configuración de AetherDSP. Este botón proporciona el mismo punto de entrada que el menú Settings. Tiene estilo de conmutador DSP del lado de la radio, pero no es marcable. Haga clic en él para elevar y enfocar el diálogo no modal de Configuración de AetherDSP.

### Botón AetherVoice (v0.9.8)

La pestaña DSP también incluye un **botón AetherVoice** que alterna la tira de canales de audio Aetherial — la suite unificada de DSP TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

### Control deslizante de nivel DSP

Un control deslizante de nivel compartido ahora aparece debajo de la cuadrícula de botones DSP. El control deslizante se reorienta automáticamente al algoritmo DSP con nivel que se haya activado más recientemente. La etiqueta a la izquierda del control deslizante muestra el nombre del algoritmo actualmente objetivo, y el valor numérico se muestra a la derecha.

Cambio importante en v0.9.8: El control deslizante de nivel DSP ahora aparece correctamente al inicio para cualquier DSP que se haya activado en el perfil guardado de la radio. Anteriormente, el control deslizante faltaba hasta que se alternara manualmente el algoritmo (#startup-slider). Esto afecta a NB, NR, ANF, NRL, NRS, NRF, ANFL y MN.

La fila del control deslizante permanece diseñada en todo momento. Cuando ningún algoritmo con nivel está activo — o solo RNN, ANFT o APF está encendido — la fila del control deslizante se atenúa y no responde a los clics.

| Control | Rango | Comportamiento |
|---|---|---|
| Control deslizante de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP con nivel activado más recientemente. Se reorienta automáticamente al cambiar de algoritmo. Oculto (atenuado) cuando ningún algoritmo con nivel está activo. |

## Selección de antena (v26.5.2.1)

Los botones de antena RX y antena TX abren menús contextuales que muestran los puertos de antena disponibles para el slice actual.

- El menú de antena RX muestra las antenas de la lista de antenas RX dedicadas del slice cuando están disponibles, recurriendo a la lista global de antenas.
- El menú de antena TX filtra automáticamente los puertos de antena solo RX. Los puertos de antena que comienzan con "RX" se excluyen de la selección de TX.
- Cada entrada del menú muestra el nombre de la antena. La antena actualmente seleccionada se marca con una marca de verificación.

## Indicadores del panel VFO

El panel VFO incluye dos indicadores que aparecen cuando se cumplen ciertas condiciones:

- **Insignia TX (roja)**: Se muestra cuando este slice es el slice de transmisión activo.
- **Insignia SPLIT (ámbar)**: Se muestra cuando TX está asignado a un slice diferente del slice de recepción activo.

La insignia del slice muestra la letra del slice y usa formato de texto enriquecido para un renderizado adecuado.

## Entrada de frecuencia para bandas XVTR (v26.5.2.1)

Al ingresar frecuencias en bandas XVTR (frecuencia del slice superior a 54 MHz o antena RX que comienza con "XVT"):

- La frecuencia máxima aceptada es 50000 MHz.
- Para slices en el rango de 100–999 MHz (bandas de 2 m/70 cm), los números enteros simples se formatean automáticamente con un decimal después del tercer dígito. Por ejemplo, ingresar 1446 se convierte en 144.6, 14696 se convierte en 146.96 y 144600 se convierte en 144.600.
- Para bandas de microondas (23 cm y superiores, 1000 MHz y más), los números enteros simples se tratan como el valor exacto en MHz. Por ejemplo, 1296 se convierte en 1296 MHz.

## Entrada de frecuencia con MHz explícito (v26.5.3)

Al ingresar frecuencias, el panel VFO usa `FrequencyEntryParser` para un análisis preciso. Si ingresa una frecuencia explícitamente en MHz (por ejemplo, 146.520 o 144.390), la entrada se acepta como MHz incluso si el valor supera 54 MHz. Esto permite la entrada directa de MHz para frecuencias VHF y UHF sin requerir la detección de banda XVTR.

## Comportamiento de slice bloqueado (v26.5.3)

Cuando un slice está bloqueado:
- El **botón de bloqueo VFO** en el panel VFO muestra un icono de candado. Haga clic en el botón para alternar el estado de bloqueo.
- Cuando está bloqueado, la pantalla de frecuencia muestra un indicador de superposición de bloqueo.
- El sintonizado con la rueda del ratón está bloqueado. Si intenta desplazarse mientras está bloqueado, el slice emite una notificación de "sintonía bloqueada por bloqueo".
- La entrada directa de frecuencia está bloqueada. Cualquier entrada directa en curso se cancela cuando el slice se bloquea.
- El panel VFO actualiza la etiqueta de frecuencia para mostrar el estado de bloqueo.

## Temas y estilos de botones (v26.6.1)

- El panel VFO usa el contenedor de temas `spectrum/vfo`. Esto mantiene los marcadores VFO en su propia superficie de temas, separada del alcance principal del espectro.
- El **botón de grosor de marcador** ahora usa colores conscientes del tema para sus estados de fondo y presionado: `color.background.1` para fondos normales y de desplazamiento, `color.accent` para el estado presionado.

## Corrección de altura de la pila de pestañas (v26.5.3)

El contenido de las pestañas del panel VFO ahora se dimensiona correctamente según el contenido de la pestaña actual. Esto corrige un espacio que podía aparecer dentro de la pestaña Mode cuando la pestaña DSP era más alta (por ejemplo, cuando el submodo DIGU/DIGL estaba visible). La pila de pestañas ahora informa solo el tamaño preferido de la página actual en lugar del máximo de todas las páginas.

## Accesibilidad de botones de pestaña y acceso directo de silencio (v26.6.3)

Las etiquetas de las pestañas del panel VFO se han cambiado de `QLabel` a `QPushButton` con un estilo plano y marcable. Esto mejora la accesibilidad y la navegación por teclado:

- Cada pestaña ahora es accesible mediante la tecla Tab en el orden de enfoque.
- La pestaña activa usa un indicador de enfoque (borde
