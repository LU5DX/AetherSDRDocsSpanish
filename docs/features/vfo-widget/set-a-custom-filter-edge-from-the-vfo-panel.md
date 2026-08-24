# Panel VFO (VfoWidget)

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por slice más utilizados — modo, presets de filtro, selección de antena, ganancia AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. El panel se colapsa a una franja compacta de solo frecuencia.

## Abrir el panel VFO

Haga clic en el marcador VFO en la pantalla del espectro para el slice que desea controlar. El panel VFO aparece anclado al marcador.

Si el panel VFO está colapsado (muestra solo una franja de frecuencia), haga clic en cualquier parte del mismo para expandirlo.

## Barra de pestañas

La barra de pestañas en la parte superior del panel VFO utiliza botones pulsadores en lugar de etiquetas (v26.6.3). Cada botón de pestaña es enfocable con la tecla Tab. La pestaña activa tiene un borde inferior de color de acento. La pestaña predeterminada (Audio/Speaker) admite un menú contextual con clic derecho para alternar la silenciación directamente.

## Controles

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este slice. Utiliza la lista de antenas por slice del radio cuando está disponible; recurre a la lista global de antenas si está vacía. Cada elemento del menú muestra su nombre interno de antena como información sobre herramientas y sugerencia de estado. | — |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra automáticamente los puertos de antena solo RX. Utiliza `txAntennaOptions()` para determinar las antenas disponibles. Cada elemento del menú muestra su nombre interno de antena como información sobre herramientas y sugerencia de estado. | — |
| Pantalla de frecuencia | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba los MHz y presione Enter o Tab. Utiliza FrequencyEntryParser para un análisis consistente. Admite entrada explícita de MHz con separadores de punto (p. ej., "14.225.000"). En bandas XVTR, acepta frecuencias hasta 50000 MHz. Para 2m/70cm (rango de 100–999 MHz), un entero simple como 1446 se convierte automáticamente a 144.6 MHz. En bandas de 23cm y microondas (≥1000 MHz), un entero simple se trata directamente como MHz. Al ingresar explícitamente una frecuencia superior a 54 MHz como MHz, se acepta sin requerir detección de banda XVTR. Cuando el slice está bloqueado, se muestra la superposición de bloqueo y se cancela la entrada directa (#2983). | — |
| Etiqueta de ancho de filtro | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de preset de filtro en la pestaña Mode. Utiliza RxApplet::formatFilterWidth como fuente única de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas de modo SSB/digital (#2197, v0.9.8). | — |
| Insignia de slice | Muestra la letra del slice (p. ej., A, B) en una insignia de color. Admite renderizado HTML para la letra del slice (#2606). Haga clic para seleccionar este slice. | — |
| Control deslizante de ganancia AF (pestaña Audio) | Establece el nivel de salida de audio para este slice (0–100). No se persiste — refleja el estado en vivo del radio. | 100 |
| Control deslizante de paneo (pestaña Audio) | Establece el paneo estéreo izquierdo/derecho para este slice. El relleno del control deslizante se pinta desde el centro hacia afuera — cuando el control está a la izquierda del centro, el relleno de acento se extiende desde el control hasta el centro; cuando el control está en el centro o a la derecha, no se pinta relleno del control al centro. Se pinta un pequeño punto de marca central en la ranura en el punto medio para que la posición neutral sea visible de un vistazo. 50 = centro. | 50 |
| Botón de silencio (pestaña Audio) | Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. | off |
| Botón + control deslizante de squelch (pestaña Audio) | Habilita el squelch para este slice. El control deslizante adyacente establece el umbral (0–100). El squelch se desactiva y se fuerza a off cuando el modo del slice es DIGU, DIGL, RTTY o cualquier modo CW, ya que no es significativo para audio digital/RTTY alimentado vía DAX o para CW donde el radio bloquea el squelch (#2504). | off |
| Combobox AGC (pestaña Audio) | Establece la velocidad de ataque/soltura del AGC para este slice: FAST, MED, SLOW u OFF. | FAST |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Habilita el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de botones depende de la serie del radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Ajustes de AetherDSP para ese algoritmo. | off |
| Botón ADSP (pestaña DSP) | Abre el diálogo de Ajustes de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Estilizado como un conmutador DSP del lado del radio pero no marcable. Al hacer clic, eleva y enfoca el diálogo no modal de Ajustes de AetherDSP. | — |
| Botón AetherVoice (pestaña DSP) | Alterna la Aetherial Audio Channel Strip — la suite DSP unificada TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira. | — |
| Combobox de modo (pestaña Mode) | Establece el modo de demodulación para este slice: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. | USB |
| Botones de preset de filtro (pestaña Mode) | Aplica un preset guardado de ancho de filtro al hacer clic. Haga clic derecho para guardar el ancho de filtro actual o establecer bordes lo/hi personalizados para esa ranura. Se persiste en FilterPresets. | — |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Habilita la sintonización incremental del receptor (RIT) o transmisor (XIT). La etiqueta muestra el desfase actual; la rueda del mouse ajusta en pasos de 10 Hz. | off |
| Combobox de canal DAX (pestaña DAX) | Asigna un canal de audio DAX a este slice: Off o 1–8. | Off |
| Botón de grosor del marcador | Cicla la línea del marcador VFO entre Off, 1 px y 3 px. Se persiste por slice. | 1 px |
| Botón de bordes de filtro | Alterna las líneas de borde del filtro en la pantalla de banda pasante del espectro. Se persiste por slice. | shown |
| Alternancia de colapso | Colapsa el panel VFO a una franja compacta de solo frecuencia. Se persiste por slice. | expanded |
| Botón de bloqueo | Alterna el bloqueo VFO para este slice. Cuando está bloqueado, la sintonización con rueda del mouse y la entrada directa de frecuencia están bloqueadas. Se muestra un icono de candado en la pantalla de frecuencia. Los intentos de sintonización mientras está bloqueado muestran una superposición LOCKED y notifican mediante la señal `tuneBlockedByLock` (#2983). La entrada directa de frecuencia se cancela automáticamente al bloquear. Desbloquear limpia la superposición LOCKED centralmente en SliceModel. | unlocked |

### Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo) / oculta | Se muestra cuando este slice es el slice de transmisión activo. La insignia y su contenedor ahora usan tokens conscientes del tema (`color.background.0`, `color.background.1`, `color.background.2`, `color.text.primary`, `color.text.label`, `color.accent`, `color.accent.bright`). Los clics en modo de inspección en la insignia o el medidor de señal revelan estos tokens para la personalización del tema. |
| Insignia SPLIT | SPLIT (ámbar) / oculta | Se muestra cuando TX está asignado a un slice diferente del slice receptor activo. Haga clic para intercambiar los slices TX y RX. |

### Botones de la pestaña DSP

A partir de v0.9.7, la **pestaña DSP** muestra solo los botones de reducción de ruido suministrados por el radio. Los algoritmos del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se han movido al menú de superposición del espectro y al applet AetherDSP; actívelos allí.

Los botones disponibles en la pestaña DSP son:

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
| MN | Filtro de muesca manual (solo en radios que lo admiten) |
| ADSP | Abre el diálogo de Ajustes de AetherDSP (algoritmos del lado del cliente) |
| AetherVoice | Abre la Aetherial Audio Channel Strip (suite DSP unificada TX/RX) |

- El botón MN está oculto a menos que el radio conectado informe soporte de filtro de muesca manual.
- El botón APF es visible solo en modo CW.

#### Control deslizante de nivel DSP

Cuando una o más funciones DSP del lado del radio que admiten control de nivel están habilitadas, aparece un control deslizante de nivel compartido debajo de la cuadrícula de botones. La etiqueta y el valor del control deslizante se actualizan para reflejar la función habilitada más recientemente. El control deslizante está siempre presente en el diseño pero se desvanece cuando ninguna función DSP compatible está activa. Arrastre el control deslizante para establecer el nivel (0–100) para la función seleccionada.

Funciones que el control deslizante de nivel puede seleccionar: NR, NB, ANF, NRL, NRS, NRF, ANFL, MN.

Funciones que no utilizan el control deslizante de nivel: RNN, ANFT, APF.

## Establecer un borde de filtro personalizado desde el panel VFO

Los botones de preset de filtro del panel VFO le permiten guardar y recuperar anchos de filtro rápidamente. Hacer clic derecho en un botón de preset abre un diálogo donde puede establecer valores exactos de borde de filtro bajo y alto para esa ranura. Use esto cuando los anchos de preset integrados no coincidan con sus necesidades operativas.

### Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El panel VFO debe estar abierto. Si no está visible, haga clic en el marcador VFO en la pantalla del espectro para el slice que desea ajustar.
- El panel VFO no debe estar colapsado. Si muestra solo una franja de frecuencia, haga clic en cualquier parte del mismo para expandirlo.
- Abra la pestaña **Mode** dentro del panel VFO para que los botones de preset de filtro sean visibles.

### Pasos

1. Haga clic en el marcador VFO en la pantalla del espectro para abrir el panel VFO del slice objetivo.
2. En el panel VFO, haga clic en la pestaña **Mode** para mostrar el selector de modo y los botones de preset de filtro.
3. Haga clic derecho en el botón de preset de filtro cuyos bordes desea personalizar. Aparece un menú contextual o diálogo.
4. Ingrese los valores de borde bajo y borde alto deseados en los campos proporcionados.
5. Confirme la entrada para guardar los bordes personalizados en esa ranura de preset.

El botón de preset ahora aplica sus bordes de filtro personalizados al hacer clic. Los valores se persisten en `FilterPresets`.

## Controles de tono FM

Cuando el modo del slice es FM, NFM o DFM, el panel VFO muestra controles de tono específicos de FM. Estos controles no se muestran para DSTR u otros modos FM digitales (v26.8.4).

## Accesibilidad

La pantalla de frecuencia incluye soporte de accesibilidad (v26.6.3). Cuando las herramientas de accesibilidad están activas, el valor de frecuencia se anuncia cuando cambia. El campo de entrada de frecuencia utiliza un widget `FreqLineEdit` personalizado con texto de sugerencia en lugar de texto de marcador de posición para una mejor accesibilidad.

Cada botón de alternancia de la pestaña DSP tiene un nombre de objeto estable (p. ej., `dspNRBtn`, `dspANFLBtn`, `dspMNBtn`) para herramientas de automatización, además de su nombre accesible para lectores de pantalla (v26.8.4).

## Comportamiento de desplazamiento

El panel VFO respeta la configuración de rueda del mouse inversa en `InteractionSettings` (v26.6.3). Cuando la rueda inversa está habilitada, desplazarse hacia arriba disminuye la frecuencia y desplazarse hacia abajo la aumenta.

## Tematización

El panel VFO utiliza su propio ámbito de tematización (`spectrum/vfo`) para permitir un estilo independiente de la pantalla del espectro. El marcador VFO, la insignia de slice y el medidor de señal se pintan utilizando tokens de tema declarados al inspector de temas. Cuando hace clic en la insignia de slice o el medidor de señal con el inspector de temas abierto, los siguientes tokens aparecen en la lista de resultados:

- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

El control deslizante de paneo y los botones de grosor del marcador utilizan hojas de estilo conscientes del tema. El relleno de marca central del control deslizante de paneo se pinta utilizando los tokens `color.accent` y `color.background.1` en lugar de colores codificados.

## Consejos

- Para verificar los bordes de filtro activos en el espectro, confirme que el botón de bordes de filtro esté en su estado predeterminado shown. Si las líneas de borde están ocultas, alterne el botón de bordes de filtro para hacerlas visibles nuevamente.
- Hacer clic derecho en un botón de preset guarda el ancho de filtro *actual* en esa ranura como alternativa a escribir los valores de borde manualmente. Use esto para una captura rápida de un filtro que ya ha ajustado.
- Para acceder a NR2, NR4, MNR, BNR, DFNR o RN2, haga clic derecho en la pantalla del espectro para abrir el menú de superposición, o abra el applet AetherDSP.
- El botón ADSP y el botón AetherVoice están colocados en la cuadrícula de botones de la pestaña DSP junto a los conmutadores DSP del lado del radio. No son marc
