# Habilitar desplazamiento RIT o XIT desde el panel VFO

RIT (Receiver Incremental Tuning) y XIT (Transmitter Incremental Tuning) le permiten desplazar la frecuencia de recepción o transmisión por un pequeño margen sin mover el VFO principal. Esto es útil para trabajar contactos en frecuencia dividida o para compensar una estación que está ligeramente fuera de su frecuencia de marcación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO para el slice objetivo debe estar abierto y expandido. Si está colapsado a la tira de solo frecuencia, haga clic en cualquier lugar para expandirlo.

## Pasos

1. Haga clic en el marcador VFO en la pantalla de espectro del slice que desea ajustar. El panel VFO aparece anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el desplazamiento del receptor, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el desplazamiento RIT actual.
4. Para habilitar el desplazamiento del transmisor, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el desplazamiento XIT actual.
5. Con RIT o XIT activos, coloque el puntero del mouse sobre el botón correspondiente y gire la rueda del mouse para ajustar el desplazamiento. Cada paso de desplazamiento cambia el desplazamiento en 10 Hz.
6. Para deshabilitar RIT o XIT, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control                              | Tipo              | Valor predeterminado | Notas                                                                  |
|--------------------------------------|-------------------|----------------------|-----------------------------------------------------------------------|
| Botón de antena RX                   | Botón pulsador    |                      | Abre el menú de selección de antena para la antena receptora de este slice. |
| Botón de antena TX                   | Botón pulsador    |                      | Abre el menú de selección de antena para la antena transmisora de este slice. |
| Pantalla de frecuencia               | Indicador         |                      | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro          | Indicador         |                      | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Usa RxApplet::formatFilterWidth como fuente única de verdad, corrigiendo un desfase de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Control deslizante AF Gain (pestaña Audio) | Control deslizante | 100 | Establece el nivel de salida de audio para este slice. No se conserva — refleja el estado en vivo de la radio. |
| Control deslizante Pan (pestaña Audio) | Control deslizante | 50 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. |
| Botón Mute (pestaña Audio)           | Botón de alternancia | off     | Silencia la salida de audio para este slice sin cambiar la configuración de AF Gain. |
| Botón + control deslizante Squelch (pestaña Audio) | Botón de alternancia | off | Habilita el squelch para este slice. El control deslizante adyacente establece el umbral. |
| Combo AGC (pestaña Audio)            | Cuadro combinado  | FAST      | Establece la velocidad de ataque/soltura del AGC para este slice. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF / MN (pestaña DSP) | Botón de alternancia | off | Habilita el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de radio y la compilación. El botón MN (notch manual) aparece solo en radios que admiten filtrado de notch manual. |
| Botón ADSP (pestaña DSP)             | Botón pulsador    |                      | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Tiene el estilo de un conmutador DSP del lado de la radio pero no es marcable. Al hacer clic se eleva y enfoca el diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP)      | Botón pulsador    |                      | Alterna la Aetherial Audio Channel Strip — la suite DSP unificada TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |
| Combo Mode (pestaña Mode)            | Cuadro combinado  | USB       | Establece el modo de demodulación para este slice. |
| Botones de preselección de filtro (pestaña Mode) | Botón pulsador |          | Aplica un ancho de filtro guardado previamente. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conservan en FilterPresets. Los bordes lo/hi personalizados se pueden establecer por ranura mediante clic derecho. |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | Botón de alternancia | off | Habilita el desplazamiento incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del mouse ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX)     | Cuadro combinado  | Off       | Asigna un canal de audio DAX a este slice. |
| Botón de grosor del marcador         | Botón pulsador    | 1 px      | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por slice. |
| Botón de bordes de filtro            | Botón de alternancia | shown   | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se conserva por slice. |
| Alternancia de colapso                | Botón de alternancia | expanded | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se conserva por slice. |
| Insignia TX                           | Indicador         |           | Muestra TX (rojo) cuando este slice es el slice de transmisión activo. Oculto en caso contrario. |
| Insignia SPLIT                        | Indicador         |           | Muestra SPLIT (ámbar) cuando TX está asignado a un slice diferente del slice de recepción activo. Oculto en caso contrario. |

**Botón de antena RX** — Abre un menú de selección de antena para la antena receptora de este slice. El menú ahora usa la propiedad `rxAntennaList()` por slice cuando está disponible, con respaldo a la lista global de antenas. Los elementos del menú muestran una etiqueta legible junto al identificador interno de la antena.

**Botón de antena TX** — Abre un menú de selección de antena para la antena transmisora de este slice. El menú filtra los puertos de antena solo de recepción. Usa el asistente `txAntennaOptions()` para determinar las antenas de transmisión válidas. Los elementos del menú muestran una etiqueta legible junto al identificador interno de la antena.

**Etiqueta de ancho de filtro** — Muestra el ancho de banda del filtro actual para el slice. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. La etiqueta usa RxApplet::formatFilterWidth como fuente única de verdad, lo que corrige un desfase de 0,1 kHz que antes afectaba las lecturas en modos SSB y digital (#2197, v0.9.8).

**Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF / MN (pestaña DSP)** — Habilitan el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de radio y la compilación. El botón MN (notch manual) aparece solo en radios que admiten filtrado de notch manual. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo.

**Botón ADSP (pestaña DSP)** — Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). El botón tiene el estilo de un conmutador DSP del lado de la radio pero no es marcable; al hacer clic se eleva y enfoca el diálogo no modal de Configuración de AetherDSP.

**Botón AetherVoice (pestaña DSP)** — Alterna la Aetherial Audio Channel Strip — la suite DSP unificada TX/RX (v0.9.8). El botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

**Botón de grosor del marcador** — Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por slice.

**Botón de bordes de filtro** — Alterna las líneas de borde del filtro en la banda de paso del espectro. Se conserva por slice.

**Alternancia de colapso** — Colapsa el panel VFO a una tira compacta de solo frecuencia. Se conserva por slice.

**Insignia TX** — Se muestra cuando este slice es el slice de transmisión activo. Muestra un indicador TX rojo.

**Insignia SPLIT** — Se muestra cuando TX está asignado a un slice diferente del slice de recepción activo. Muestra un indicador SPLIT ámbar.

**Botones RIT / XIT + etiquetas** — Habilitan el desplazamiento incremental del receptor (RIT) o del transmisor (XIT) para este slice. Cuando están activos, la etiqueta junto a cada botón muestra el valor de desplazamiento actual. Gire la rueda del mouse sobre el botón para ajustar el desplazamiento en pasos de 10 Hz. Ninguna de las dos configuraciones se conserva; el estado refleja el estado en vivo de la radio.

**Botón + control deslizante Squelch (pestaña Audio)** — Habilita el squelch para este slice. El control deslizante adyacente establece el umbral. El squelch se desactiva automáticamente cuando el modo del slice es CW, digital o RTTY, porque en esos modos el audio alimenta decodificadores externos a través de DAX, donde el squelch podría enmascarar señales FSK débiles (#2504). El botón y el control deslizante se atenúan en esos modos.

## Consejos

- Los desplazamientos RIT y XIT son independientes. Puede habilitar ambos al mismo tiempo para desplazar la recepción y la transmisión de forma independiente.
- El ajuste con la rueda del mouse es de 10 Hz por paso. Para desplazamientos mayores, gire varias muescas.
- Cuando un slice está bloqueado, el ajuste con la rueda del mouse en el panel VFO está bloqueado. Aparece una notificación indicando que el ajuste está bloqueado por el bloqueo. La entrada directa de frecuencia también se cancela si estaba en curso cuando se aplicó el bloqueo.
- Haga clic derecho en la tira de frecuencia colapsada para agregar un spot. El menú contextual de clic derecho funciona incluso cuando el panel está colapsado a la tira de solo frecuencia, e informa correctamente la frecuencia del VFO en lugar de la frecuencia del cursor ajustada al paso de la pantalla de espectro subyacente (#4455).

## Cambios en v26.8.4

### Soporte de filtro de notch manual (MN)

Se ha agregado un nuevo botón **MN** (notch manual) a la cuadrícula de la pestaña DSP. Este botón está oculto por defecto y aparece solo en radios que informan soporte para filtrado de notch manual (`hasManualNotch`). Cuando está disponible, el botón MN alterna el filtro de notch manual para el slice, y el control deslizante compartido a nivel DSP ajusta el nivel del notch manual cuando el botón MN es el filtro activo.

El botón MN usa un nombre de objeto estable (`dspMNBtn`) para el direccionamiento del puente de automatización. Todos los botones de alternancia DSP ahora usan nombres de objeto estables basados en su texto (por ejemplo, `dspNRBtn`, `dspAPFBtn`) en lugar de nombres accesibles en estilo prosa. Esto garantiza que los scripts de automatización que controlan estos elementos sigan funcionando incluso si las etiquetas visibles al usuario se reformulan en el futuro.

### Cambio de nombre del método de squelch

El método interno de control de squelch se ha renombrado de `setSquelch()` a `setManualSquelch()` para distinguirlo de los modos de squelch automático. El comportamiento visible al usuario no cambia: el botón y el control deslizante de squelch en la pestaña Audio funcionan exactamente como antes.

### Corrección de spot con clic derecho en modo colapsado

Clic derecho → **Add Spot** ahora funciona correctamente cuando el panel VFO está colapsado a la tira de solo frecuencia (#4455). Anteriormente, los clics se propagaban al SpectrumWidget subyacente, que informaba la frecuencia del cursor ajustada al paso en lugar de la frecuencia real del VFO. La etiqueta de frecuencia colapsada ahora intercepta los eventos, por lo que el spot se agrega en la frecuencia del VFO.

### Detección de modo FM

El panel VFO ahora identifica correctamente los modos relacionados con FM (FM, NFM, DFM, DSTR) para fines de control de tonos. Los controles de tono FM se muestran solo para los modos FM, NFM y DFM.

## Cambios en v26.7.4

### Renderizado de sombra de elevación

El marcador VFO ahora renderiza su sombra de elevación usando un widget `FlagShadow` dedicado, separado del widget `VfoWidget` principal. Esto significa que los repintados de medidores en vivo dentro del marcador VFO no obligan a la sombra a volverse a desenfocar a la velocidad de animación, mejorando la velocidad de fotogramas cuando un SmartMeter u otro widget de actualización en vivo está incrustado en el área del marcador VFO. La sombra usa un algoritmo de desenfoque de caja con una imagen en caché que se reconstruye solo cuando el tamaño del widget o la relación de píxeles del dispositivo cambia.

### Reenvío de altura-para-ancho para páginas de medidores

La pila de pestañas ahora reenvía `heightForWidth()` desde la página actual. Esto permite que una página que conserva una relación de aspecto (como un widget SmartMeter incrustado a través de `SmartMtrWidget`) impulse la altura de la tira; las páginas sin altura-para-ancho (como el espaciador del S-meter) no se ven afectadas.

### Controles de filtro adaptativo

El panel VFO ahora incluye soporte para controles de filtro adaptativo a través de la nueva clase `AdaptiveFilterControls`. Cuando la radio proporciona señales de filtro adaptativo (compatibles con ciertas compilaciones de firmware FLEX-8600), el panel VFO muestra controles para configurar el comportamiento del filtro adaptativo por slice.

## Cambios en v26.6.3

### Botones de pestaña reemplazados por QPushButton

Las etiquetas de pestaña en la barra de pestañas se han reemplazado de QLabel a QPushButton. Cada pestaña es ahora un botón plano y marcable con soporte de enfoque de teclado. Presionar Tab recorre los botones de pestaña. El clic derecho en el botón de la pestaña Audio (altavoz) alterna el mute directamente sin abrir la pestaña.

### Anuncios de frecuencia accesibles

Cuando un lector de pantalla u otra herramienta de accesibilidad está activa, la pantalla de frecuencia emite un evento de cambio de valor accesible cuando la frecuencia cambia. Los anuncios duplicados se supr
