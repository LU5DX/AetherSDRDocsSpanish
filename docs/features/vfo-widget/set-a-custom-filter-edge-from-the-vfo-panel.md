# Panel VFO (VfoWidget)

El panel VFO es un panel de control flotante por receptor anclado al marcador VFO en la visualización del espectro. Proporciona acceso rápido a las configuraciones más utilizadas por receptor: modo, preajustes de filtro, selección de antena, ganancia de AF, balance, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación de DAX, todo sin salir de la vista del espectro. El panel se contrae a una tira compacta que solo muestra la frecuencia.

## Abrir el panel VFO

Haga clic en la bandera del marcador VFO en la visualización del espectro para el receptor que desea controlar. El panel VFO aparece anclado a la bandera.

Si el panel VFO está contraído (muestra solo una tira de frecuencia), haga clic en cualquier parte del mismo para expandirlo.

## Barra de pestañas

La barra de pestañas en la parte superior del panel VFO utiliza botones pulsadores en lugar de etiquetas (v26.6.3). Cada botón de pestaña se puede enfocar con la tecla Tab. La pestaña activa tiene un borde inferior de color de acento. La pestaña predeterminada (Audio/Speaker) admite un menú contextual con clic derecho para alternar la silenciación directamente.

## Controles

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Botón de antena RX | Abre un menú de selección de antena para la antena receptora de este receptor. Utiliza la lista de antenas por receptor de la radio cuando está disponible; recurre a la lista global de antenas si está vacía. Cada elemento del menú muestra el nombre interno de la antena como información sobre herramientas y barra de estado. | — |
| Botón de antena TX | Abre un menú de selección de antena para la antena transmisora de este receptor. Filtra automáticamente los puertos de antena solo de RX. Utiliza `txAntennaOptions()` para determinar las antenas disponibles. Cada elemento del menú muestra el nombre interno de la antena como información sobre herramientas y barra de estado. | — |
| Visualización de frecuencia | Muestra la frecuencia actual del receptor. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. Utiliza FrequencyEntryParser para un análisis consistente. Admite la entrada explícita de MHz con separadores de punto (ej., "14.225.000"). En bandas XVTR, acepta frecuencias de hasta 50000 MHz. Para 2m/70cm (rango 100–999 MHz), un número entero simple como 1446 se convierte automáticamente a 144.6 MHz. En bandas de 23 cm y microondas (≥1000 MHz), un número entero simple se trata directamente como MHz. Al introducir explícitamente una frecuencia superior a 54 MHz como MHz, se acepta sin requerir la detección de banda XVTR. Cuando el receptor está bloqueado, se muestra la superposición de bloqueo y la entrada directa se cancela (#2983). | — |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza RxApplet::formatFilterWidth como fuente única de información, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2198, v0.9.8). | — |
| Insignia de receptor | Muestra la letra del receptor (ej., A, B) en una insignia de color. Admite renderizado HTML para la letra del receptor (#2606). Haga clic para seleccionar este receptor. | — |
| Control deslizante de ganancia AF (pestaña Audio) | Establece el nivel de salida de audio para este receptor (0–100). No se conserva: refleja el estado en vivo de la radio. | 100 |
| Control deslizante de balance (pestaña Audio) | Establece el balance estéreo izquierdo/derecho para este receptor. El relleno del control deslizante se pinta desde el centro hacia afuera — cuando el control está a la izquierda del centro, el relleno de acento se extiende desde el control hasta el centro; cuando el control está en el centro o a la derecha, no se pinta relleno desde el control hasta el centro. Se pinta un pequeño punto de marca central en la ranura en el punto medio para que la posición neutral sea visible de un vistazo. 50 = centro. | 50 |
| Botón de silencio (pestaña Audio) | Silencia la salida de audio para este receptor sin cambiar la configuración de ganancia AF. | desactivado |
| Botón + control deslizante de squelch (pestaña Audio) | Activa el squelch para este receptor. El control deslizante adyacente establece el umbral (0–100). El squelch se desactiva y se fuerza a apagado cuando el modo del receptor es DIGU, DIGL, RTTY o cualquier modo CW, ya que no es significativo para audio digital/RTTY alimentado a través de DAX o para CW donde la radio bloquea el squelch encendido (#2504). | desactivado |
| Combinado AGC (pestaña Audio) | Establece la velocidad de ataque/liberación del AGC para este receptor: FAST, MED, SLOW u OFF. | FAST |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Activa el algoritmo de reducción de ruido correspondiente para este receptor. La disponibilidad del botón depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo. | desactivado |
| Botón ADSP (pestaña DSP) | Abre el diálogo de Configuración de AetherDSP (NR2/NR4/DFNR/RN2/BNR/MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Estilizado como un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. | — |
| Botón AetherVoice (pestaña DSP) | Alterna el Aetherial Audio Channel Strip: el conjunto unificado de DSP TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para el strip. | — |
| Combinado Mode (pestaña Mode) | Establece el modo de demodulación para este receptor: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. | USB |
| Botones de preajuste de filtro (pestaña Mode) | Aplica un preajuste de ancho de filtro guardado al hacer clic. Haga clic derecho para guardar el ancho de filtro actual o establecer bordes lo/hi personalizados para esa ranura. Se conserva en FilterPresets. | — |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. | desactivado |
| Combinado de canal DAX (pestaña DAX) | Asigna un canal de audio DAX a este receptor: Off o 1–8. | Off |
| Botón de grosor del marcador | Cicla la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por receptor. | 1 px |
| Botón de bordes del filtro | Alterna las líneas de borde del filtro en la visualización de la banda pasante del espectro. Se conserva por receptor. | mostrados |
| Alternancia de contracción | Contrae el panel VFO a una tira compacta que solo muestra la frecuencia. Se conserva por receptor. | expandido |
| Botón de bloqueo | Alterna el bloqueo VFO para este receptor. Cuando está bloqueado, se bloquean la sintonización con la rueda del ratón y la entrada directa de frecuencia. Se muestra un icono de candado en la visualización de frecuencia. Los intentos de sintonización mientras está bloqueado muestran una superposición LOCKED y notifican mediante la señal `tuneBlockedByLock` (#2983). La entrada directa de frecuencia se cancela automáticamente al bloquear. Desbloquear elimina la superposición LOCKED de forma centralizada en SliceModel. | desbloqueado |

### Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo) / oculto | Se muestra cuando este receptor es el receptor de transmisión activo. La insignia y su contenedor ahora utilizan tokens conscientes del tema (`color.background.0`, `color.background.1`, `color.background.2`, `color.text.primary`, `color.text.label`, `color.accent`, `color.accent.bright`). Los clics en modo de inspección en la insignia o el medidor de señal revelan estos tokens para la personalización del tema. |
| Insignia SPLIT | SPLIT (ámbar) / oculto | Se muestra cuando TX está asignado a un receptor diferente al receptor de recepción activo. Haga clic para intercambiar los receptores TX y RX. |

### Botones de la pestaña DSP

A partir de v0.9.7, la **pestaña DSP** muestra solo los botones de reducción de ruido proporcionados por la radio. Los algoritmos del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se han movido al menú de superposición del espectro y al applet AetherDSP; actívelos allí.

Los botones disponibles en la pestaña DSP son:

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
| ADSP | Abre el diálogo de Configuración de AetherDSP (algoritmos del lado del cliente) |
| AetherVoice | Abre el Aetherial Audio Channel Strip (conjunto unificado de DSP TX/RX) |

#### Control deslizante de nivel DSP

Cuando una o más funciones DSP del lado de la radio que admiten un control de nivel están habilitadas, aparece un control deslizante de nivel compartido debajo de la cuadrícula de botones. La etiqueta y el valor del control deslizante se actualizan para reflejar la función habilitada más recientemente. El control deslizante siempre está presente en el diseño, pero se desvanece cuando no hay ninguna función DSP compatible activa. Arrastre el control deslizante para establecer el nivel (0–100) para la función objetivo.

Funciones a las que el control deslizante de nivel puede apuntar: NR, NB, ANF, NRL, NRS, NRF, ANFL.

Funciones a las que el control deslizante de nivel NO apunta: RNN, ANFT, APF.

## Establecer un borde de filtro personalizado desde el panel VFO

Los botones de preajuste de filtro del panel VFO le permiten guardar y recuperar anchos de filtro rápidamente. Al hacer clic derecho en un botón de preajuste se abre un diálogo donde puede establecer valores exactos de borde de filtro bajo y alto para esa ranura. Utilícelo cuando los anchos de preajuste integrados no se ajusten a sus necesidades operativas.

### Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO en la visualización del espectro para el receptor que desea ajustar.
- El panel VFO no debe estar contraído. Si muestra solo una tira de frecuencia, haga clic en cualquier parte del mismo para expandirlo.
- Abra la pestaña **Mode** dentro del panel VFO para que los botones de preajuste de filtro sean visibles.

### Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para abrir el panel VFO para el receptor objetivo.
2. En el panel VFO, haga clic en la pestaña **Mode** para mostrar el selector de modo y los botones de preajuste de filtro.
3. Haga clic derecho en el botón de preajuste de filtro cuyos bordes desea personalizar. Aparece un menú contextual o un diálogo.
4. Introduzca los valores de borde bajo y borde alto deseados en los campos proporcionados.
5. Confirme la entrada para guardar los bordes personalizados en esa ranura de preajuste.

El botón de preajuste ahora aplica sus bordes de filtro personalizados al hacer clic. Los valores se conservan en `FilterPresets`.

## Accesibilidad

La visualización de frecuencia incluye soporte de accesibilidad (v26.6.3). Cuando las herramientas de accesibilidad están activas, el valor de frecuencia se anuncia cuando cambia. El campo de entrada de frecuencia utiliza un widget `FreqLineEdit` personalizado con texto de sugerencia en lugar de texto de marcador de posición para mejorar la accesibilidad.

## Comportamiento del desplazamiento

El panel VFO respeta la configuración de rueda del ratón inversa en `InteractionSettings` (v26.6.3). Cuando la rueda inversa está habilitada, desplazarse hacia arriba disminuye la frecuencia y desplazarse hacia abajo la aumenta.

## Temas

El panel VFO utiliza su propio ámbito de tematización (`spectrum/vfo`) para permitir un estilo independiente de la visualización del espectro. La bandera del marcador VFO, la insignia del receptor y el medidor de señal se pintan utilizando tokens de tema declarados al inspector de temas. Cuando hace clic en la insignia del receptor o en el medidor de señal con el inspector de temas abierto, aparecen los siguientes tokens en la lista de resultados:

- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

El control deslizante de balance y el botón de grosor del marcador utilizan hojas de estilo conscientes del tema. El relleno de la marca central del control deslizante de balance se pinta utilizando los tokens `color.accent` y `color.background.1` en lugar de colores codificados.

## Consejos

- Para verificar los bordes de filtro activos en el espectro, confirme que el botón de bordes del filtro esté en su estado predeterminado mostrado. Si las líneas de borde están ocultas, alterne el botón de bordes del filtro para hacerlas visibles nuevamente.
- Haga clic derecho en un botón de preajuste para guardar el ancho de filtro *actual* en esa ranura como alternativa a escribir los valores de borde manualmente. Utilícelo para una captura rápida de un filtro que ya ha marcado.
- Para acceder a NR2, NR4, MNR, BNR, DFNR o RN2, haga clic derecho en la visualización del espectro para abrir el menú de superposición, o abra el applet AetherDSP.
- Los botones ADSP y AetherVoice se colocan en la cuadrícula de botones de la pestaña DSP junto a los conmutadores DSP del lado de la radio. No son marcables: al hacer clic en ADSP se abre el diálogo de Configuración de AetherDSP, y al hacer clic en AetherVoice se abre el Aetherial Audio Channel Strip.
- El squelch se desactiva automáticamente y se fuerza a apagado cuando cambia a DIGU, DIGL, RTTY o cualquier modo CW. Para volver a activar el squelch, cambie a un modo de voz (USB, LSB, AM, SAM, FM
