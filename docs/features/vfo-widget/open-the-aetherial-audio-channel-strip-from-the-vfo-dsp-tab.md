# Usar el panel VFO

El panel VFO es un panel de control flotante por segmento anclado al marcador VFO en la visualización del espectro. Proporciona acceso rápido a las configuraciones más utilizadas por segmento — modo, preajustes de filtro, selección de antena, ganancia AF, panorámico, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.

## Abrir el panel VFO

Haga clic en el marcador VFO en la visualización del espectro para el segmento deseado. El panel VFO se abre en modo expandido.

## Contraer o expandir el panel VFO

Haga clic en el botón **Collapse toggle** (icono de flecha) en el borde derecho de la barra de título del panel VFO para contraerlo a una tira compacta que solo muestra la frecuencia. Vuelva a hacer clic para expandir.

## Usar las pestañas

El panel VFO contiene varias pestañas:

- Pestaña **Audio** — controles de ganancia AF, panorámico, silencio, silenciador y AGC
- Pestaña **DSP** — botones de algoritmos de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR, NRL, NRS, RNN, NRF), botón ADSP y botón AetherVoice
- Pestaña **Mode** — selección de modo y botones de preajuste de filtro
- Pestaña **X/RIT** — sintonización incremental RIT y XIT
- Pestaña **DAX** — asignación de canal de audio DAX

## Qué hace cada control

| Control | Pestaña | Etiqueta | Predeterminado | Rango válido | Comportamiento |
|---------|---------|----------|----------------|--------------|----------------|
| Botón de antena RX | — | **RX** (icono) | — | — | Abre el menú de selección de antena para la antena receptora de este segmento. El menú muestra la lista de antenas RX de la radio cuando está disponible; de lo contrario, usa la lista general de antenas. |
| Botón de antena TX | — | **TX** (icono) | — | — | Abre el menú de selección de antena para la antena transmisora de este segmento. Solo se muestran las antenas aptas para transmisión (no puertos solo RX). |
| Visualización de frecuencia | — | (lectura de frecuencia) | — | — | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba la frecuencia en MHz y presione Enter o Tab. En bandas XVTR, la frecuencia máxima admitida es 50000 MHz. En bandas de 2m/70cm (rango de 100-999 MHz), los números enteros desnudos con 4-6 dígitos insertan automáticamente un decimal después del tercer dígito (ej. 1446 → 144.6, 14696 → 146.96, 144600 → 144.600). En bandas de microondas, un número entero desnudo se interpreta directamente como MHz. |
| Distintivo de segmento | — | (distintivo de color con la letra del segmento) | — | — | Muestra la letra del segmento en un distintivo de color. Admite formato de texto enriquecido para renderizado HTML (#2606). Haga clic para alternar el foco en el segmento correspondiente. |
| Etiqueta de ancho de filtro | — | (lectura de ancho de banda) | — | — | Muestra el ancho de banda actual del filtro. Haga clic para recorrer cíclicamente los botones de preajuste de filtro en la pestaña Mode. Utiliza RxApplet::formatFilterWidth como fuente única de verdad. |
| Deslizador de ganancia AF | Audio | — | 100 | 0-100 | Establece el nivel de salida de audio para este segmento. No se persiste. |
| Deslizador de panorámico | Audio | — | 50 | 0-100 | Establece el paneo estéreo izquierdo/derecho para este segmento (50 = centro). |
| Botón de silencio | Audio | **Mute** | apagado | — | Silencia la salida de audio para este segmento sin cambiar la configuración de ganancia AF. |
| Botón de activación de silenciador | Audio | **Squelch** | apagado | — | Activa o desactiva el silenciador para este segmento. Deshabilitado en modos DIGU, DIGL, CW, CWL y RTTY. |
| Deslizador de silenciador | Audio | (adyacente al botón Squelch) | — | 0-100 | Establece el umbral del silenciador. |
| Combo AGC | Audio | **FAST** | FAST | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este segmento. |
| Botón NR | DSP | **NR** | apagado | — | Activa el algoritmo de reducción de ruido correspondiente. La disponibilidad depende de la serie de radio y la compilación. |
| Botón NR2 | DSP | **NR2** | apagado | — | Activa el algoritmo de reducción de ruido NR2. Haga clic derecho para abrir AetherDSP Settings. |
| Botón RN2 | DSP | **RN2** | apagado | — | Activa el algoritmo de reducción de ruido RN2. |
| Botón NR4 | DSP | **NR4** | apagado | — | Activa el algoritmo de reducción de ruido NR4. Haga clic derecho para abrir AetherDSP Settings. |
| Botón MNR | DSP | **MNR** | apagado | — | Activa el algoritmo de reducción de ruido MNR. Haga clic derecho para abrir AetherDSP Settings. |
| Botón DFNR | DSP | **DFNR** | apagado | — | Activa el algoritmo de reducción de ruido DFNR. Haga clic derecho para abrir AetherDSP Settings. |
| Botón BNR | DSP | **BNR** | apagado | — | Activa el algoritmo de reducción de ruido BNR. |
| Botón NRL | DSP | **NRL** | apagado | — | Activa el algoritmo de reducción de ruido NRL. |
| Botón NRS | DSP | **NRS** | apagado | — | Activa el algoritmo de reducción de ruido NRS. |
| Botón RNN | DSP | **RNN** | apagado | — | Activa el algoritmo de reducción de ruido RNN. |
| Botón NRF | DSP | **NRF** | apagado | — | Activa el algoritmo de reducción de ruido NRF. |
| Botón ADSP | DSP | **ADSP** | — | — | Abre el diálogo AetherDSP Settings. No seleccionable. |
| Botón AetherVoice | DSP | **AetherVoice** | apagado (no seleccionable) | — | Alterna la Aetherial Audio Channel Strip. |
| Combo de modo | Mode | **USB** | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este segmento. |
| Botones de preajuste de filtro | Mode | **1**, **2**, **3**, **4** | — | — | Aplica un ancho de filtro preajustado guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Activación RIT | X/RIT | **RIT** | apagado | — | Activa la sintonización incremental del receptor. La rueda del ratón ajusta el desplazamiento en pasos de 10 Hz. |
| Activación XIT | X/RIT | **XIT** | apagado | — | Activa la sintonización incremental del transmisor. La rueda del ratón ajusta el desplazamiento en pasos de 10 Hz. |
| Etiqueta de desplazamiento RIT/XIT | X/RIT | (lectura de desplazamiento) | — | — | Muestra el desplazamiento actual de RIT o XIT. |
| Combo de canal DAX | DAX | **Off** | Off | Off, 1-8 | Asigna un canal de audio DAX a este segmento. |
| Botón de grosor del marcador | — | (icono de grosor de línea) | 1 px | Off, 1 px, 3 px | Recorre cíclicamente el grosor de la línea del marcador VFO. Se persiste por segmento. |
| Botón de bordes del filtro | — | (icono de borde de filtro) | mostrado | — | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se persiste por segmento. |
| Alternar colapso | — | (icono de flecha) | expandido | — | Contrae el panel VFO a una tira compacta que solo muestra la frecuencia. Se persiste por segmento. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Distintivo TX | TX (rojo), oculto | Se muestra cuando este segmento es el segmento transmisor activo. |
| Distintivo SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un segmento diferente al segmento receptor activo. |

---

# Abrir la Aetherial Audio Channel Strip desde la pestaña DSP del VFO

Abre la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX — directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en el marcador VFO si está contraído).

## Pasos

1. Haga clic en el marcador VFO en la visualización del espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **AetherVoice** en la pestaña DSP del panel VFO.
3. Haga clic en **AetherVoice**. Aparece la Aetherial Audio Channel Strip.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---------|----------|----------------|----------------|
| Botón AetherVoice | **AetherVoice** | apagado (no seleccionable) | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX. Abarca 2 columnas en la cuadrícula DSP de 4 columnas. |

## Relacionado

- [Abrir AetherDSP Settings desde la pestaña DSP del VFO](open-aetherdsp-settings-from-the-vfo-dsp-tab.md)

---

# Abrir AetherDSP Settings desde la pestaña DSP del VFO

Abre el diálogo AetherDSP Settings (algoritmos de reducción de ruido del lado del cliente) directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en el marcador VFO si está contraído).

## Pasos

1. Haga clic en el marcador VFO en la visualización del espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **ADSP** en la pestaña DSP del panel VFO.
3. Haga clic en **ADSP**. Aparece el diálogo AetherDSP Settings.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---------|----------|----------------|----------------|
| Botón ADSP | **ADSP** | n/a | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). No seleccionable. Al hacer clic, eleva y enfoca el diálogo no modal. |

## Notas

- Haga clic derecho en los botones **NR2**, **NR4**, **MNR** o **DFNR** para abrir el diálogo AetherDSP Settings para ese algoritmo específico.

## Relacionado

- [Abrir Aetherial Audio Channel Strip desde la pestaña DSP del VFO](open-aetherial-audio-channel-strip-from-the-vfo-dsp-tab.md)

---

# Usar el silenciador en un panel VFO

Activa o desactiva el silenciador para un segmento y ajusta el umbral del silenciador desde el panel VFO en la visualización del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en el marcador VFO si está contraído).

## Pasos

1. Haga clic en el marcador VFO en la visualización del espectro para el segmento deseado para abrir el panel VFO.
2. Haga clic en la pestaña **Audio**.
3. Haga clic en el botón de activación **Squelch** para habilitar el silenciador para este segmento.
4. Arrastre el deslizador adyacente para establecer el umbral del silenciador (0-100).

## Notas importantes

- El silenciador se desactiva automáticamente en los modos **DIGU**, **DIGL**, **CW**, **CWL** y **RTTY**. En modos digitales, RTTY y CW, el audio alimenta a decodificadores externos a través de DAX, donde el silenciador no tiene sentido y puede bloquear señales débiles. En modo CW, la radio también bloquea el silenciador activado a un nivel fijo y rechaza los cambios del lado del cliente.
- Al cambiar a un modo donde el silenciador está deshabilitado, el estado del silenciador se guarda y se restaura al volver a un modo de voz o FM.
- La configuración del silenciador no se persiste y refleja únicamente el estado en vivo de la radio.

## Qué hace cada control

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento |
|---------|----------|----------------|--------------|----------------|
| Botón de activación de silenciador | **Squelch** | apagado | — | Activa o desactiva el silenciador para este segmento. |
| Deslizador de silenciador | (adyacente al botón Squelch) | — | 0-100 | Establece el umbral del silenciador. |
