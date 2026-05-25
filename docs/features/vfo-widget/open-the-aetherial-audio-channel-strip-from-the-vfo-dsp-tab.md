# Uso del panel VFO

El panel VFO es un panel de control flotante por segmento, anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a las configuraciones más utilizadas por segmento — modo, preajustes de filtro, selección de antena, ganancia AF, panorámico, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.

## Abrir el panel VFO

Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado. El panel VFO se abre en modo expandido.

## Contraer o expandir el panel VFO

Haga clic en el botón **Collapse toggle** (icono de flecha) en el borde derecho de la barra de título del panel VFO para contraerlo a una tira compacta que solo muestra la frecuencia. Vuelva a hacer clic para expandirlo.

## Uso de las pestañas

El panel VFO contiene varias pestañas:

- **Audio** — controles de ganancia AF, panorámico, silencio, squelch y AGC
- **DSP** — botones de algoritmos de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR, NRL, NRS, RNN, NRF), botón ADSP y botón AetherVoice
- **Mode** — selección de modo y botones de preajustes de filtro
- **X/RIT** — sintonización incremental RIT y XIT
- **DAX** — asignación de canal de audio DAX

## Función de cada control

| Control | Pestaña | Etiqueta | Predeterminado | Rango válido | Comportamiento |
|---------|---------|----------|----------------|--------------|----------------|
| Botón antena RX | — | **RX** (icono) | — | — | Abre el menú de selección de antena para la antena receptora de este segmento. El menú muestra la lista de antenas RX de la radio cuando está disponible; de lo contrario, recurre a la lista general de antenas. |
| Botón antena TX | — | **TX** (icono) | — | — | Abre el menú de selección de antena para la antena transmisora de este segmento. Solo se muestran antenas adecuadas para transmisión (no puertos solo RX). |
| Visualización de frecuencia | — | (lectura de frecuencia) | — | — | Muestra la frecuencia actual del segmento. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba la frecuencia en MHz y presione Enter o Tab. En bandas XVTR, la frecuencia máxima admitida es 50000 MHz. En bandas de 2m/70cm (rango 100-999 MHz), los números enteros sin decimales con 4-6 dígitos insertan automáticamente un punto decimal después del tercer dígito (por ejemplo, 1446 → 144.6, 14696 → 146.96, 144600 → 144.600). En bandas de microondas, un número entero sin decimales se interpreta directamente como MHz. Si el segmento está bloqueado, la entrada directa se cancela y se bloquea; consulte las notas del botón Lock. |
| Insignia de segmento | — | (insignia de color con la letra del segmento) | — | — | Muestra la letra del segmento en una insignia de color. Admite formato de texto enriquecido para renderizado HTML (#2606). Haga clic para alternar el foco en el segmento correspondiente. |
| Etiqueta de ancho de filtro | — | (lectura de ancho de banda) | — | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones de preajuste de filtro en la pestaña Mode. Utiliza RxApplet::formatFilterWidth como fuente única de verdad. |
| Deslizador de ganancia AF | Audio | — | 100 | 0-100 | Establece el nivel de salida de audio para este segmento. No se persiste. |
| Deslizador de panorámico | Audio | — | 50 | 0-100 | Establece el paneo estéreo izquierda/derecha para este segmento (50 = centro). |
| Botón de silencio | Audio | **Mute** | desactivado | — | Silencia la salida de audio de este segmento sin cambiar la configuración de ganancia AF. |
| Botón de alternancia de squelch | Audio | **Squelch** | desactivado | — | Activa o desactiva el squelch para este segmento. Deshabilitado en modos DIGU, DIGL, CW, CWL y RTTY. |
| Deslizador de squelch | Audio | (adyacente al botón Squelch) | — | 0-100 | Establece el umbral de squelch. |
| Combo AGC | Audio | **FAST** | FAST | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este segmento. |
| Botón NR | DSP | **NR** | desactivado | — | Activa el algoritmo de reducción de ruido correspondiente. La disponibilidad depende de la serie y compilación de la radio. |
| Botón NR2 | DSP | **NR2** | desactivado | — | Activa el algoritmo de reducción de ruido NR2. Haga clic derecho para abrir la configuración de AetherDSP. |
| Botón RN2 | DSP | **RN2** | desactivado | — | Activa el algoritmo de reducción de ruido RN2. |
| Botón NR4 | DSP | **NR4** | desactivado | — | Activa el algoritmo de reducción de ruido NR4. Haga clic derecho para abrir la configuración de AetherDSP. |
| Botón MNR | DSP | **MNR** | desactivado | — | Activa el algoritmo de reducción de ruido MNR. Haga clic derecho para abrir la configuración de AetherDSP. |
| Botón DFNR | DSP | **DFNR** | desactivado | — | Activa el algoritmo de reducción de ruido DFNR. Haga clic derecho para abrir la configuración de AetherDSP. |
| Botón BNR | DSP | **BNR** | desactivado | — | Activa el algoritmo de reducción de ruido BNR. |
| Botón NRL | DSP | **NRL** | desactivado | — | Activa el algoritmo de reducción de ruido NRL. |
| Botón NRS | DSP | **NRS** | desactivado | — | Activa el algoritmo de reducción de ruido NRS. |
| Botón RNN | DSP | **RNN** | desactivado | — | Activa el algoritmo de reducción de ruido RNN. |
| Botón NRF | DSP | **NRF** | desactivado | — | Activa el algoritmo de reducción de ruido NRF. |
| Botón ADSP | DSP | **ADSP** | — | — | Abre el diálogo de configuración de AetherDSP. No seleccionable. |
| Botón AetherVoice | DSP | **AetherVoice** | desactivado (no seleccionable) | — | Alterna la visualización del Aetherial Audio Channel Strip. |
| Combo de modo | Mode | **USB** | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este segmento. |
| Botones de preajuste de filtro | Mode | **1**, **2**, **3**, **4** | — | — | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Alternancia RIT | X/RIT | **RIT** | desactivado | — | Activa la sintonización incremental del receptor. La rueda de desplazamiento ajusta el desplazamiento en pasos de 10 Hz. |
| Alternancia XIT | X/RIT | **XIT** | desactivado | — | Activa la sintonización incremental del transmisor. La rueda de desplazamiento ajusta el desplazamiento en pasos de 10 Hz. |
| Etiqueta de desplazamiento RIT/XIT | X/RIT | (lectura de desplazamiento) | — | — | Muestra el desplazamiento actual de RIT o XIT. |
| Combo de canal DAX | DAX | **Off** | Off | Off, 1-8 | Asigna un canal de audio DAX a este segmento. |
| Botón de grosor del marcador | — | (icono de grosor de línea) | 1 px | Off, 1 px, 3 px | Cambia cíclicamente el grosor de la línea del marcador VFO. Se persiste por segmento. |
| Botón de bordes del filtro | — | (icono de borde de filtro) | mostrado | — | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se persiste por segmento. |
| Alternancia de colapso | — | (icono de flecha) | expandido | — | Contrae el panel VFO a una tira compacta que solo muestra la frecuencia. Se persiste por segmento. |
| Botón de bloqueo | — | 🔒 (bloqueado) / 🔓 (desbloqueado) | desbloqueado | — | Bloquea la frecuencia del VFO. Cuando está bloqueado, se bloquean la sintonización con la rueda de desplazamiento y la entrada directa de frecuencia. En modo contraído, se bloquea el desplazamiento sobre el panel. La visualización de frecuencia muestra una superposición **LOCKED**. Al desbloquear, se limpia la superposición centralmente en SliceModel (#2983). |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Insignia TX | TX (rojo), oculto | Se muestra cuando este segmento es el segmento de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un segmento diferente al segmento de recepción activo. |
| Superposición LOCKED | LOCKED (texto), oculto | Se muestra en la visualización de frecuencia cuando el VFO está bloqueado. Se limpia al desbloquear. |

---

# Abrir el Aetherial Audio Channel Strip desde la pestaña DSP del VFO

Abre el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX — directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **AetherVoice** en la pestaña DSP del panel VFO.
3. Haga clic en **AetherVoice**. Aparece el Aetherial Audio Channel Strip.

## Función de cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---------|----------|----------------|----------------|
| Botón AetherVoice | **AetherVoice** | desactivado (no seleccionable) | Alterna la visualización del Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

## Relacionado

- [Abrir la configuración de AetherDSP desde la pestaña DSP del VFO](open-aetherdsp-settings-from-the-vfo-dsp-tab.md)

---

# Abrir la configuración de AetherDSP desde la pestaña DSP del VFO

Abre el diálogo de configuración de AetherDSP (algoritmos de reducción de ruido del lado del cliente) directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **ADSP** en la pestaña DSP del panel VFO.
3. Haga clic en **ADSP**. Aparece el diálogo de configuración de AetherDSP.

## Función de cada control

| Control | Etiqueta | Predeterminado | Comportamiento |
|---------|----------|----------------|----------------|
| Botón ADSP | **ADSP** | n/a | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). No seleccionable. Al hacer clic, eleva y enfoca el diálogo no modal. |

## Notas

- Haga clic derecho en los botones **NR2**, **NR4**, **MNR** o **DFNR** para abrir el diálogo de configuración de AetherDSP para ese algoritmo específico.

## Relacionado

- Abrir el Aetherial Audio Channel Strip desde la pestaña DSP del VFO

---

# Uso del squelch en un panel VFO

Activa o desactiva el squelch para un segmento y ajusta el umbral de squelch desde el panel VFO en la pantalla del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado para abrir el panel VFO.
2. Haga clic en la pestaña **Audio**.
3. Haga clic en el botón de alternancia **Squelch** para activar el squelch para este segmento.
4. Arrastre el deslizador adyacente para establecer el umbral de squelch (0-100).

## Notas importantes

- El squelch se desactiva automáticamente en los modos **DIGU**, **DIGL**, **CW**, **CWL** y **RTTY**. En modos digital, RTTY y CW, el audio alimenta decodificadores externos a través de DAX, donde el squelch no tiene sentido y puede enmascarar señales débiles. En modo CW, la radio también bloquea el squelch activado a un nivel fijo y rechaza los cambios del lado del cliente.
- Al cambiar a un modo donde el squelch está desactivado, el estado del squelch se guarda y se restaura al volver a un modo de voz o FM.
- Las configuraciones de squelch no se persisten y reflejan solo el estado en vivo de la radio.

## Función de cada control

| Control | Etiqueta | Predeterminado | Rango válido | Comportamiento |
|---------|----------|----------------|--------------|----------------|
| Botón de alternancia de squelch | **Squelch** | desactivado | — | Activa o desactiva el squelch para este segmento. |
| Deslizador de squelch | (adyacente al botón Squelch) | — | 0-100 | Establece el umbral de squelch. |
