# Usar el panel VFO

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en la visualización del espectro. Proporciona acceso rápido a los ajustes por slice más utilizados — modo, presets de filtro, selección de antena, ganancia AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y que al menos un slice esté activo.

## Abrir el panel VFO

Haga clic en el marcador VFO en la visualización del espectro para el slice deseado. El panel VFO se abre en modo expandido.

## Contraer o expandir el panel VFO

Haga clic en el botón **Collapse toggle** (icono de flecha) en el borde derecho de la barra de título del panel VFO para contraerlo a una tira compacta de solo frecuencia. Haga clic de nuevo para expandirlo. Haga clic derecho en la tira de frecuencia contraída para agregar un spot en la frecuencia del VFO.

## Usar las pestañas

El panel VFO contiene varias pestañas:

- Pestaña **Audio** — controles de ganancia AF, paneo, silencio, squelch y AGC
- Pestaña **DSP** — botones de algoritmos de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR, NRL, NRS, RNN, NRF, MN), botón ADSP y botón AetherVoice
- Pestaña **Mode** — selección de modo y botones de presets de filtro
- Pestaña **X/RIT** — sintonización incremental RIT y XIT
- Pestaña **DAX** — asignación de canal de audio DAX

Las etiquetas de las pestañas se implementan como botones pulsadores marcables que admiten el foco del teclado. Presione Tab para navegar entre las etiquetas de las pestañas; presione Enter o Espacio para activar la pestaña enfocada. Haga clic derecho en la etiqueta de la pestaña Audio para alternar el silencio directamente para el slice actual.

## Qué hace cada control

| Control | Pestaña | Etiqueta | Predeterminado | Rango válido | Comportamiento |
|---------|---------|----------|----------------|---------------|----------------|
| Botón de antena RX | — | **RX** (icono) | — | — | Abre el menú de selección de antena para la antena receptora de este slice. El menú muestra la lista de antenas RX de la radio cuando está disponible; de lo contrario, recurre a la lista general de antenas. |
| Botón de antena TX | — | **TX** (icono) | — | — | Abre el menú de selección de antena para la antena transmisora de este slice. Solo se muestran antenas adecuadas para transmisión (no puertos solo RX). |
| Visualización de frecuencia | — | (lectura de frecuencia) | — | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba la frecuencia en MHz y presione Enter o Tab. En bandas XVTR, la frecuencia máxima admitida es 50000 MHz. En bandas de 2m/70cm (rango de 100-999 MHz), los números enteros de 4 a 6 dígitos insertan automáticamente un decimal después del tercer dígito (por ejemplo, 1446 → 144.6, 14696 → 146.96, 144600 → 144.600). En bandas de microondas, un número entero se interpreta directamente como MHz. Si el slice está bloqueado, la entrada directa se cancela y se bloquea; consulte las notas del botón Lock a continuación. |
| Insignia del slice | — | (insignia de color con la letra del slice) | — | — | Muestra la letra del slice en una insignia de color. Admite formato de texto enriquecido para renderizado HTML (#2606). Haga clic para alternar el foco en el slice correspondiente. |
| Etiqueta de ancho de filtro | — | (lectura de ancho de banda) | — | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de presets de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como única fuente de verdad. |
| Control deslizante de ganancia AF | Audio | — | 100 | 0-100 | Establece el nivel de salida de audio para este slice. No se guarda. |
| Control deslizante de paneo | Audio | — | 50 | 0-100 | Establece el paneo estéreo izquierdo/derecho para este slice (50 = centro). El relleno del control deslizante se ancla desde el centro hacia afuera, con un punto de marca central en la ranura para mostrar la posición neutra. |
| Botón de silencio | Audio | **Mute** | desactivado | — | Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. |
| Botón de alternancia de squelch | Audio | **Squelch** | desactivado | — | Activa o desactiva el squelch para este slice. Desactivado en modos DIGU, DIGL, CW, CWL y RTTY. |
| Control deslizante de squelch | Audio | (adyacente al botón Squelch) | — | 0-100 | Establece el umbral de squelch. |
| Combinación AGC | Audio | **FAST** | FAST | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este slice. |
| Botón NR | DSP | **NR** | desactivado | — | Activa el algoritmo de reducción de ruido correspondiente. La disponibilidad depende de la serie de la radio y la compilación. |
| Botón NR2 | DSP | **NR2** | desactivado | — | Activa el algoritmo de reducción de ruido NR2. Haga clic derecho para abrir AetherDSP Settings. |
| Botón RN2 | DSP | **RN2** | desactivado | — | Activa el algoritmo de reducción de ruido RN2. |
| Botón NR4 | DSP | **NR4** | desactivado | — | Activa el algoritmo de reducción de ruido NR4. Haga clic derecho para abrir AetherDSP Settings. |
| Botón MNR | DSP | **MNR** | desactivado | — | Activa el algoritmo de reducción de ruido MNR. Haga clic derecho para abrir AetherDSP Settings. |
| Botón DFNR | DSP | **DFNR** | desactivado | — | Activa el algoritmo de reducción de ruido DFNR. Haga clic derecho para abrir AetherDSP Settings. |
| Botón BNR | DSP | **BNR** | desactivado | — | Activa el algoritmo de reducción de ruido BNR. |
| Botón NRL | DSP | **NRL** | desactivado | — | Activa el algoritmo de reducción de ruido NRL. |
| Botón NRS | DSP | **NRS** | desactivado | — | Activa el algoritmo de reducción de ruido NRS. |
| Botón RNN | DSP | **RNN** | desactivado | — | Activa el algoritmo de reducción de ruido RNN. |
| Botón NRF | DSP | **NRF** | desactivado | — | Activa el algoritmo de reducción de ruido NRF. |
| Botón MN | DSP | **MN** | desactivado | — | Activa el filtro de muesca manual. Solo se muestra en radios que admiten filtrado de muesca manual. |
| Botón ADSP | DSP | **ADSP** | — | — | Abre el diálogo AetherDSP Settings. No marcable. |
| Botón AetherVoice | DSP | **AetherVoice** | desactivado (no marcable) | — | Alterna la Aetherial Audio Channel Strip. |
| Combinación de modo | Mode | **USB** | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este slice. |
| Botones de preset de filtro | Mode | **1**, **2**, **3**, **4** | — | — | Aplica un preset de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Alternancia RIT | X/RIT | **RIT** | desactivado | — | Activa la sintonización incremental del receptor. La rueda de desplazamiento ajusta el desvío en pasos de 10 Hz. |
| Alternancia XIT | X/RIT | **XIT** | desactivado | — | Activa la sintonización incremental del transmisor. La rueda de desplazamiento ajusta el desvío en pasos de 10 Hz. |
| Etiqueta de desvío RIT/XIT | X/RIT | (lectura de desvío) | — | — | Muestra el desvío RIT o XIT actual. |
| Combinación de canal DAX | DAX | **Off** | Off | Off, 1-8 | Asigna un canal de audio DAX a este slice. |
| Botón de grosor del marcador | — | (icono de grosor de línea) | 1 px | Off, 1 px, 3 px | Recorre el grosor de línea del marcador VFO. Se guarda por slice. |
| Botón de bordes de filtro | — | (icono de borde de filtro) | mostrado | — | Alterna las líneas de borde de filtro en la banda pasante del espectro. Se guarda por slice. |
| Alternancia de contracción | — | (icono de flecha) | expandido | — | Contrae el panel VFO a una tira compacta de solo frecuencia. Se guarda por slice. |
| Botón Lock | — | 🔒 (bloqueado) / 🔓 (desbloqueado) | desbloqueado | — | Bloquea la frecuencia del VFO. Cuando está bloqueado, la sintonización con la rueda de desplazamiento y la entrada directa de frecuencia están bloqueadas. En modo contraído, el desplazamiento sobre el panel está bloqueado. La visualización de frecuencia muestra una superposición **LOCKED**. Al desbloquear se limpia la superposición de forma centralizada en SliceModel (#2983). |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Insignia TX | TX (rojo), oculto | Se muestra cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente del slice de recepción activo. La insignia tiene un estilo con mejor contraste para su legibilidad. |
| Superposición LOCKED | LOCKED (texto), oculto | Se muestra en la visualización de frecuencia cuando el VFO está bloqueado. Se limpia al desbloquear. |

## Sintonización con la rueda de desplazamiento

La rueda de desplazamiento sintoniza la frecuencia del slice. El paso de sintonización depende del modo actual. Si el ajuste **Reverse mouse wheel** está habilitado en Interaction Settings, la dirección de sintonización se invierte, por lo que desplazarse hacia arriba disminuye la frecuencia y desplazarse hacia abajo la aumenta.

---

# Abrir la Aetherial Audio Channel Strip desde la pestaña DSP del VFO

Abre la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX — directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y que al menos un slice esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en el marcador VFO si está contraído).

## Pasos

1. Haga clic en el marcador VFO en la visualización del espectro para el slice deseado para abrir el panel VFO.
2. Localice el botón **AetherVoice** en la pestaña DSP del panel VFO.
3. Haga clic en **AetherVoice**. Aparece la Aetherial Audio Channel Strip.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---------|----------|----------------|----------------|
| Botón AetherVoice | **AetherVoice** | desactivado (no marcable) | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX. Abarca 2 columnas en la cuadrícula DSP de 4 columnas. |

## Relacionado

- [Open AetherDSP Settings from the VFO DSP tab](open-aetherdsp-settings-from-the-vfo-dsp-tab.md)

---

# Abrir AetherDSP Settings desde la pestaña DSP del VFO

Abre el diálogo AetherDSP Settings (algoritmos de reducción de ruido del lado del cliente) directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y que al menos un slice esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en el marcador VFO si está contraído).

## Pasos

1. Haga clic en el marcador VFO en la visualización del espectro para el slice deseado para abrir el panel VFO.
2. Localice el botón **ADSP** en la pestaña DSP del panel VFO.
3. Haga clic en **ADSP**. Aparece el diálogo AetherDSP Settings.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---------|----------|----------------|----------------|
| Botón ADSP | **ADSP** | n/a | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). No marcable. Al hacer clic, se eleva y enfoca el diálogo no modal. |

## Notas

- Haga clic derecho en los botones **NR2**, **NR4**, **MNR** o **DFNR** para abrir el diálogo AetherDSP Settings para ese algoritmo específico.

## Relacionado

- Abrir la Aetherial Audio Channel Strip desde la pestaña DSP del VFO

---

# Usar squelch en un panel VFO

Activa o desactiva el squelch para un slice y ajusta el umbral de squelch desde el panel VFO en la visualización del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y que al menos un slice esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en el marcador VFO si está contraído).

## Pasos

1. Haga clic en el marcador VFO en la visualización del espectro para el slice deseado para abrir el panel VFO.
2. Haga clic en la pestaña **Audio**.
3. Haga clic en el botón de alternancia **Squelch** para activar el squelch para este slice.
4. Arrastre el control deslizante adyacente para establecer el umbral de squelch (0-100).

## Notas importantes

- El squelch se desactiva automáticamente en modos **DIGU**, **DIGL**, **CW**, **CWL** y **RTTY**. En modos digitales, RTTY y CW, el audio alimenta decodificadores externos a través de DAX, donde el squelch no es significativo y puede bloquear señales débiles. En modo CW, la radio también bloquea el squelch activado a un nivel fijo y rechaza cambios del lado del cliente.
- Al cambiar a un modo donde el squelch está desactivado, el estado del squelch se guarda y se restaura al volver a un modo de voz o FM.
- Los ajustes de squelch no se guardan y reflejan solo el estado en vivo de la radio.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento |
|---------|----------|----------------|---------------|----------------|
| Botón de alternancia de squelch | **Squelch** | desactivado | — | Activa o desactiva el squelch para este slice. |
| Control deslizante de squelch | (adyacente al botón Squelch) | — | 0-100 | Establece el umbral de squel
