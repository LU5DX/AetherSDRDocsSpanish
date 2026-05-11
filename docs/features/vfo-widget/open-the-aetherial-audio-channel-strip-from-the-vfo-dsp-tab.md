# Abrir la tira de canal de audio Aetherial desde la pestaña DSP del VFO

Abre la tira de canal de audio Aetherial (el conjunto unificado de DSP de TX/RX) directamente desde el panel VFO sin tener que navegar por los menús.

## Antes de empezar

- Asegúrese de que la radio esté conectada y al menos un slice esté activo.
- El panel VFO debe ser visible en el visor del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en el visor del espectro para el slice deseado y abra el panel VFO.
2. Localice el botón **AetherVoice** en la pestaña DSP del panel VFO.
3. Haga clic en **AetherVoice**. Aparecerá la tira de canal de audio Aetherial.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Comportamiento |
|---------|----------|----------------------|----------------|
| Botón AetherVoice | **AetherVoice** | desactivado (no seleccionable) | Activa o desactiva la tira de canal de audio Aetherial (el conjunto unificado de DSP de TX/RX). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

## Relacionado

- [Abrir la configuración de AetherDSP desde la pestaña DSP del VFO](open-aetherdsp-settings-from-the-vfo-dsp-tab.md)

---

# Abrir la configuración de AetherDSP desde la pestaña DSP del VFO

Abre el cuadro de diálogo de configuración de AetherDSP (algoritmos de reducción de ruido del lado del cliente) directamente desde el panel VFO sin tener que navegar por los menús.

## Antes de empezar

- Asegúrese de que la radio esté conectada y al menos un slice esté activo.
- El panel VFO debe ser visible en el visor del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en el visor del espectro para el slice deseado y abra el panel VFO.
2. Localice el botón **ADSP** en la pestaña DSP del panel VFO.
3. Haga clic en **ADSP**. Aparecerá el cuadro de diálogo de configuración de AetherDSP.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Comportamiento |
|---------|----------|----------------------|----------------|
| Botón ADSP | **ADSP** | n/a | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). No seleccionable. Al hacer clic, eleva y enfoca el cuadro de diálogo no modal. |

## Notas

- Haga clic derecho en los botones **NR2**, **NR4**, **MNR** o **DFNR** para abrir el cuadro de diálogo de configuración de AetherDSP para ese algoritmo específico.

## Relacionado

- [Abrir la tira de canal de audio Aetherial desde la pestaña DSP del VFO](open-aetherial-audio-channel-strip-from-the-vfo-dsp-tab.md)

---

# Usar el squelch en un panel VFO

Activa o desactiva el squelch para un slice y ajusta el umbral de squelch desde el panel VFO en el visor del espectro.

## Antes de empezar

- Asegúrese de que la radio esté conectada y al menos un slice esté activo.
- El panel VFO debe ser visible en el visor del espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en el visor del espectro para el slice deseado y abra el panel VFO.
2. Haga clic en la pestaña **Audio**.
3. Haga clic en el botón de alternancia **Squelch** para activar el squelch en este slice.
4. Arrastre el control deslizante adyacente para ajustar el umbral de squelch (0-100).

## Notas importantes

- El squelch se desactiva automáticamente en los modos **DIGU**, **DIGL**, **CW**, **CWL** y **RTTY**. En los modos digital, RTTY y CW, el audio se envía a decodificadores externos a través de DAX, donde el squelch no tiene sentido y puede enmascarar señales débiles. En modo CW, la radio también bloquea el squelch activado a un nivel fijo y rechaza los cambios del lado del cliente.
- Al cambiar a un modo en el que el squelch está desactivado, el estado del squelch se guarda y se restaura al volver a un modo de voz o FM.
- La configuración del squelch no se conserva y refleja únicamente el estado en vivo de la radio.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------|----------------------|--------------|----------------|
| Botón de alternancia Squelch | **Squelch** | desactivado | — | Activa o desactiva el squelch para este slice. |
| Control deslizante de Squelch | (adyacente al botón Squelch) | — | 0-100 | Ajusta el umbral de squelch. |

---

# Usar el panel VFO

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en el visor del espectro. Proporciona acceso rápido a las configuraciones por slice más utilizadas (modo, preajustes de filtro, selección de antena, ganancia de AF, panoramización, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación de DAX) sin salir de la vista del espectro.

## Antes de empezar

- Asegúrese de que la radio esté conectada y al menos un slice esté activo.

## Abrir el panel VFO

Haga clic en la bandera del marcador VFO en el visor del espectro para el slice deseado. El panel VFO se abre en modo expandido.

## Contraer o expandir el panel VFO

Haga clic en el botón **Collapse toggle** (icono de flecha) en el borde derecho de la barra de título del panel VFO para contraerlo a una tira compacta que solo muestra la frecuencia. Vuelva a hacer clic para expandirlo.

## Usar las pestañas

El panel VFO contiene varias pestañas:

- Pestaña **Audio**: controles de ganancia de AF, panoramización, silencio, squelch y AGC.
- Pestaña **DSP**: botones de algoritmos de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR, NRL, NRS, RNN, NRF), botón ADSP y botón AetherVoice.
- Pestaña **Mode**: selección de modo y botones de preajustes de filtro.
- Pestaña **X/RIT**: sintonización incremental RIT y XIT.
- Pestaña **DAX**: asignación de canal de audio DAX.

## Función de cada control

| Control | Pestaña | Etiqueta | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------|----------|----------------------|--------------|----------------|
| Botón de antena RX | — | **RX** (icono) | — | — | Abre el menú de selección de antena para la antena receptora de este slice. |
| Botón de antena TX | — | **TX** (icono) | — | — | Abre el menú de selección de antena para la antena transmisora de este slice. |
| Visualización de frecuencia | — | (lectura de frecuencia) | — | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba la frecuencia en MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | — | (lectura de ancho de banda) | — | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajustes de filtro en la pestaña Mode. |
| Control deslizante de ganancia AF | Audio | — | 100 | 0-100 | Ajusta el nivel de salida de audio para este slice. No se conserva. |
| Control deslizante de panoramización | Audio | — | 50 | 0-100 | Ajusta la panoramización estéreo izquierda/derecha para este slice (50 = centro). |
| Botón de silencio | Audio | **Mute** | desactivado | — | Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. |
| Botón de alternancia Squelch | Audio | **Squelch** | desactivado | — | Activa o desactiva el squelch para este slice. Desactivado en modos DIGU, DIGL, CW, CWL y RTTY. |
| Control deslizante de Squelch | Audio | (adyacente al botón Squelch) | — | 0-100 | Ajusta el umbral de squelch. |
| Combo AGC | Audio | **FAST** | FAST | FAST, MED, SLOW, OFF | Ajusta la velocidad de ataque/liberación del AGC para este slice. |
| Botón NR | DSP | **NR** | desactivado | — | Activa el algoritmo de reducción de ruido correspondiente. La disponibilidad depende de la serie de radio y la compilación. |
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
| Botón ADSP | DSP | **ADSP** | — | — | Abre el cuadro de diálogo de configuración de AetherDSP. No seleccionable. |
| Botón AetherVoice | DSP | **AetherVoice** | desactivado (no seleccionable) | — | Activa o desactiva la tira de canal de audio Aetherial. |
| Combo Mode | Mode | **USB** | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este slice. |
| Botones de preajustes de filtro | Mode | **1**, **2**, **3**, **4** | — | — | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Alternancia RIT | X/RIT | **RIT** | desactivado | — | Activa la sintonización incremental del receptor. La rueda del ratón ajusta el desplazamiento en pasos de 10 Hz. |
| Alternancia XIT | X/RIT | **XIT** | desactivado | — | Activa la sintonización incremental del transmisor. La rueda del ratón ajusta el desplazamiento en pasos de 10 Hz. |
| Etiqueta de desplazamiento RIT/XIT | X/RIT | (lectura de desplazamiento) | — | — | Muestra el desplazamiento actual de RIT o XIT. |
| Combo de canal DAX | DAX | **Off** | Off | Off, 1-8 | Asigna un canal de audio DAX a este slice. |
| Botón de grosor de marcador | — | (icono de grosor de línea) | 1 px | Off, 1 px, 3 px | Recorre el grosor de la línea del marcador VFO. Se conserva por slice. |
| Botón de bordes de filtro | — | (icono de borde de filtro) | mostrado | — | Activa o desactiva las líneas de borde del filtro en la banda de paso del espectro. Se conserva por slice. |
| Collapse toggle | — | (icono de flecha) | expandido | — | Contrae el panel VFO a una tira compacta que solo muestra la frecuencia. Se conserva por slice. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Insignia TX | TX (rojo), oculto | Se muestra cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo. |
