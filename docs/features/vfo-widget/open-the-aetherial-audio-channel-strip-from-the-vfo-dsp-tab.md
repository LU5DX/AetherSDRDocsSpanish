# Use el panel VFO

El panel VFO es un panel de control flotante por segmento (slice) anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por segmento más utilizados (modo, preajustes de filtro, selección de antena, ganancia de AF, paneo (pan), silenciador (squelch), CAG, RIT/XIT, botones de reducción de ruido DSP y asignación DAX) sin salir de la vista del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y que al menos un segmento esté activo.

## Abrir el panel VFO

Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado. El panel VFO se abre en modo expandido.

## Contraer o expandir el panel VFO

Haga clic en el botón **Collapse toggle** (icono de flecha) en el borde derecho de la barra de título del panel VFO para contraerlo a una tira compacta de solo frecuencia. Vuelva a hacer clic para expandirlo.

## Use las pestañas

El panel VFO contiene varias pestañas:

- Pestaña **Audio** — controles de ganancia de AF, paneo, silencio, silenciador y CAG.
- Pestaña **DSP** — botones de algoritmos de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR, NRL, NRS, RNN, NRF), botón ADSP y botón AetherVoice.
- Pestaña **Mode** — selección de modo y botones de preajuste de filtro.
- Pestaña **X/RIT** — sintonización incremental RIT y XIT.
- Pestaña **DAX** — asignación de canal de audio DAX.

## Qué hace cada control

| Control | Pestaña | Etiqueta | Predeterminado | Rango válido | Comportamiento |
|---------|---------|----------|----------------|--------------|----------------|
| Botón de antena RX | — | **RX** (icono) | — | — | Abre el menú de selección de antena para la antena receptora de este segmento. El menú muestra la lista de antenas RX de la radio cuando está disponible; de lo contrario, recurre a la lista general de antenas. |
| Botón de antena TX | — | **TX** (icono) | — | — | Abre el menú de selección de antena para la antena transmisora de este segmento. Solo se muestran las antenas adecuadas para transmisión (no puertos solo RX). |
| Indicador de frecuencia | — | (lectura de frecuencia) | — | — | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba la frecuencia en MHz y presione Enter o Tab. En bandas XVTR, la frecuencia máxima admitida es 50000 MHz. En bandas de 2m/70cm (rango de 100-999 MHz), los números enteros desnudos de 4 a 6 dígitos insertan automáticamente un punto decimal después del tercer dígito (p. ej., 1446 → 144.6, 14696 → 146.96, 144600 → 144.600). En bandas de microondas, un número entero desnudo se interpreta directamente como MHz. Si el segmento está bloqueado, la entrada directa se cancela y se bloquea; consulte las notas del botón Lock a continuación. |
| Distintivo de segmento | — | (distintivo de color con letra del segmento) | — | — | Muestra la letra del segmento en un distintivo de color. Admite formato de texto enriquecido para renderizado HTML (#2606). Haga clic para alternar el foco en el segmento correspondiente. |
| Etiqueta de ancho de filtro | — | (lectura de ancho de banda) | — | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad. |
| Deslizador de ganancia AF | Audio | — | 100 | 0-100 | Ajusta el nivel de salida de audio para este segmento. No se conserva. |
| Deslizador de paneo | Audio | — | 50 | 0-100 | Ajusta el paneo estéreo izquierdo/derecho para este segmento (50 = centro). El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central en la ranura para mostrar la posición neutral. |
| Botón de silencio | Audio | **Mute** | apagado | — | Silencia la salida de audio para este segmento sin cambiar el ajuste de ganancia AF. |
| Botón de alternancia de silenciador | Audio | **Squelch** | apagado | — | Activa o desactiva el silenciador para este segmento. Deshabilitado en modos DIGU, DIGL, CW, CWL y RTTY. |
| Deslizador de silenciador | Audio | (adyacente al botón Squelch) | — | 0-100 | Ajusta el umbral del silenciador. |
| Combinación CAG | Audio | **FAST** | FAST | FAST, MED, SLOW, OFF | Ajusta la velocidad de ataque/liberación del CAG para este segmento. |
| Botón NR | DSP | **NR** | apagado | — | Activa el algoritmo de reducción de ruido correspondiente. La disponibilidad depende de la serie de radio y la compilación. |
| Botón NR2 | DSP | **NR2** | apagado | — | Activa el algoritmo de reducción de ruido NR2. Haga clic derecho para abrir Configuración de AetherDSP. |
| Botón RN2 | DSP | **RN2** | apagado | — | Activa el algoritmo de reducción de ruido RN2. |
| Botón NR4 | DSP | **NR4** | apagado | — | Activa el algoritmo de reducción de ruido NR4. Haga clic derecho para abrir Configuración de AetherDSP. |
| Botón MNR | DSP | **MNR** | apagado | — | Activa el algoritmo de reducción de ruido MNR. Haga clic derecho para abrir Configuración de AetherDSP. |
| Botón DFNR | DSP | **DFNR** | apagado | — | Activa el algoritmo de reducción de ruido DFNR. Haga clic derecho para abrir Configuración de AetherDSP. |
| Botón BNR | DSP | **BNR** | apagado | — | Activa el algoritmo de reducción de ruido BNR. |
| Botón NRL | DSP | **NRL** | apagado | — | Activa el algoritmo de reducción de ruido NRL. |
| Botón NRS | DSP | **NRS** | apagado | — | Activa el algoritmo de reducción de ruido NRS. |
| Botón RNN | DSP | **RNN** | apagado | — | Activa el algoritmo de reducción de ruido RNN. |
| Botón NRF | DSP | **NRF** | apagado | — | Activa el algoritmo de reducción de ruido NRF. |
| Botón ADSP | DSP | **ADSP** | — | — | Abre el cuadro de diálogo Configuración de AetherDSP. No marcable. |
| Botón AetherVoice | DSP | **AetherVoice** | apagado (no marcable) | — | Alterna la Aetherial Audio Channel Strip. |
| Combinación de modo | Mode | **USB** | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este segmento. |
| Botones de preajuste de filtro | Mode | **1**, **2**, **3**, **4** | — | — | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Alternancia RIT | X/RIT | **RIT** | apagado | — | Activa la sintonización incremental del receptor. La rueda de desplazamiento ajusta el desplazamiento en pasos de 10 Hz. |
| Alternancia XIT | X/RIT | **XIT** | apagado | — | Activa la sintonización incremental del transmisor. La rueda de desplazamiento ajusta el desplazamiento en pasos de 10 Hz. |
| Etiqueta de desplazamiento RIT/XIT | X/RIT | (lectura de desplazamiento) | — | — | Muestra el desplazamiento RIT o XIT actual. |
| Combinación de canal DAX | DAX | **Off** | Off | Off, 1-8 | Asigna un canal de audio DAX a este segmento. |
| Botón de grosor de marcador | — | (icono de grosor de línea) | 1 px | Off, 1 px, 3 px | Recorre el grosor de la línea del marcador VFO. Se conserva por segmento. |
| Botón de bordes de filtro | — | (icono de borde de filtro) | mostrado | — | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se conserva por segmento. |
| Alternancia de contracción | — | (icono de flecha) | expandido | — | Contrae el panel VFO a una tira compacta de solo frecuencia. Se conserva por segmento. |
| Botón de bloqueo | — | 🔒 (bloqueado) / 🔓 (desbloqueado) | desbloqueado | — | Bloquea la frecuencia del VFO. Cuando está bloqueado, la sintonización con la rueda de desplazamiento y la entrada directa de frecuencia están bloqueadas. En modo contraído, el desplazamiento sobre el panel está bloqueado. La pantalla de frecuencia muestra una superposición **LOCKED**. Al desbloquear, se elimina la superposición centralmente en `SliceModel` (#2983). |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Distintivo TX | TX (rojo), oculto | Se muestra cuando este segmento es el segmento de transmisión activo. |
| Distintivo SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un segmento diferente al segmento receptor activo. |
| Superposición LOCKED | LOCKED (texto), oculta | Se muestra en la pantalla de frecuencia cuando el VFO está bloqueado. Se borra al desbloquear. |

---

# Abrir la Aetherial Audio Channel Strip desde la pestaña DSP del VFO

Abre la Aetherial Audio Channel Strip (el conjunto unificado de DSP de TX/RX) directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y que al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **AetherVoice** en la pestaña DSP del panel VFO.
3. Haga clic en **AetherVoice**. Aparece la Aetherial Audio Channel Strip.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---------|----------|----------------|----------------|
| Botón AetherVoice | **AetherVoice** | apagado (no marcable) | Alterna la Aetherial Audio Channel Strip (el conjunto unificado de DSP de TX/RX). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

## Relacionado

- [Abrir Configuración de AetherDSP desde la pestaña DSP del VFO](open-aetherdsp-settings-from-the-vfo-dsp-tab.md)

---

# Abrir Configuración de AetherDSP desde la pestaña DSP del VFO

Abre el cuadro de diálogo Configuración de AetherDSP (algoritmos de reducción de ruido del lado del cliente) directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y que al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **ADSP** en la pestaña DSP del panel VFO.
3. Haga clic en **ADSP**. Aparece el cuadro de diálogo Configuración de AetherDSP.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---------|----------|----------------|----------------|
| Botón ADSP | **ADSP** | n/a | Abre el cuadro de diálogo Configuración de AetherDSP (algoritmos NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). No marcable. Al hacer clic, eleva y enfoca el cuadro de diálogo no modal. |

## Notas

- Haga clic derecho en los botones **NR2**, **NR4**, **MNR** o **DFNR** para abrir el cuadro de diálogo Configuración de AetherDSP para ese algoritmo específico.

## Relacionado

- [Abrir la Aetherial Audio Channel Strip desde la pestaña DSP del VFO](open-aetherial-audio-channel-strip-from-the-vfo-dsp-tab.md)

---

# Usar el silenciador en un panel VFO

Activa o desactiva el silenciador para un segmento y ajusta el umbral del silenciador desde el panel VFO en la pantalla del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y que al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado para abrir el panel VFO.
2. Haga clic en la pestaña **Audio**.
3. Haga clic en el botón de alternancia **Squelch** para activar el silenciador para este segmento.
4. Arrastre el deslizador adyacente para ajustar el umbral del silenciador (0-100).

## Notas importantes

- El silenciador se desactiva automáticamente en los modos **DIGU**, **DIGL**, **CW**, **CWL** y **RTTY**. En modos digitales, RTTY y CW, el audio se envía a decodificadores externos a través de DAX, donde el silenciador no es significativo y puede bloquear señales débiles. En el modo CW, la radio también bloquea el silenciador activado a un nivel fijo y rechaza los cambios del lado del cliente.
- Al cambiar a un modo donde el silenciador está desactivado, el estado del silenciador se guarda y se restaura al volver a un modo de voz o FM.
- La configuración del silenciador no se conserva y solo refleja el estado en vivo de la radio.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento |
|---------|----------|----------------|--------------|----------------|
| Botón de alternancia de silenciador | **Squelch** | apagado | — | Activa o desactiva el silenciador para este segmento. |
| Deslizador de silenciador | (adyacente al botón Squelch) | — | 0-100 | Ajusta el umbral del silenciador. |
