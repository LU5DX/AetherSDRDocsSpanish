# Uso del panel VFO

El panel VFO es un panel de control flotante por segmento anclado al marcador VFO en la pantalla de espectro. Proporciona acceso rápido a las configuraciones más usadas por segmento — modo, ajustes preestablecidos de filtro, selección de antena, ganancia AF, paneo, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista de espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.

## Abrir el panel VFO

Haga clic en la bandera del marcador VFO en la pantalla de espectro para el segmento deseado. El panel VFO se abre en modo expandido.

## Contraer o expandir el panel VFO

Haga clic en el botón **Collapse toggle** (icono de flecha) en el borde derecho de la barra de título del panel VFO para contraerlo a una tira compacta de solo frecuencia. Vuelva a hacer clic para expandirlo.

## Uso de las pestañas

El panel VFO contiene varias pestañas:

- Pestaña **Audio** — controles de ganancia AF, paneo, silencio, silenciador y AGC
- Pestaña **DSP** — botones de algoritmos de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR, NRL, NRS, RNN, NRF), botón ADSP y botón AetherVoice
- Pestaña **Mode** — selección de modo y botones de ajustes preestablecidos de filtro
- Pestaña **X/RIT** — sintonización incremental RIT y XIT
- Pestaña **DAX** — asignación de canal de audio DAX

Las etiquetas de pestaña se implementan como botones pulsables seleccionables que admiten el foco de teclado. Presione Tab para navegar entre etiquetas de pestaña; presione Enter o Espacio para activar la pestaña enfocada. Haga clic derecho en la etiqueta de la pestaña Audio para silenciar directamente el segmento actual.

## Función de cada control

| Control | Pestaña | Etiqueta | Predet. | Rango válido | Comportamiento |
|---------|---------|----------|---------|--------------|----------------|
| Botón antena RX | — | **RX** (icono) | — | — | Abre el menú de selección de antena para la antena receptora de este segmento. El menú muestra la lista de antenas RX de la radio cuando está disponible; de lo contrario, usa la lista general de antenas. |
| Botón antena TX | — | **TX** (icono) | — | — | Abre el menú de selección de antena para la antena transmisora de este segmento. Solo se muestran antenas aptas para transmisión (no puertos solo RX). |
| Pantalla de frecuencia | — | (lectura de frecuencia) | — | — | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba la frecuencia en MHz y presione Enter o Tab. En bandas XVTR, la frecuencia máxima admitida es 50000 MHz. En bandas de 2m/70cm (rango 100-999 MHz), los números enteros con 4-6 dígitos insertan automáticamente un punto decimal después del tercer dígito (ej.: 1446 → 144.6, 14696 → 146.96, 144600 → 144.600). En bandas de microondas, un número entero se interpreta directamente como MHz. Si el segmento está bloqueado, la entrada directa se cancela y se bloquea; consulte las notas del botón Lock a continuación. |
| Distintivo del segmento | — | (distintivo coloreado con letra del segmento) | — | — | Muestra la letra del segmento en un distintivo coloreado. Admite formato de texto enriquecido para renderizado HTML (#2606). Haga clic para alternar el foco en el segmento correspondiente. |
| Etiqueta de ancho de filtro | — | (lectura de ancho de banda) | — | — | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de ajustes preestablecidos de filtro en la pestaña Mode. Usa RxApplet::formatFilterWidth como fuente única de verdad. |
| Deslizador de ganancia AF | Audio | — | 100 | 0-100 | Establece el nivel de salida de audio para este segmento. No se persiste. |
| Deslizador de paneo | Audio | — | 50 | 0-100 | Establece el paneo estéreo izquierdo/derecho para este segmento (50 = centro). El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central en la ranura para mostrar la posición neutral. |
| Botón de silencio | Audio | **Mute** | desact. | — | Silencia la salida de audio para este segmento sin cambiar la configuración de ganancia AF. |
| Botón de silenciador | Audio | **Squelch** | desact. | — | Activa o desactiva el silenciador para este segmento. Desactivado en modos DIGU, DIGL, CW, CWL y RTTY. |
| Deslizador de silenciador | Audio | (adyacente al botón Squelch) | — | 0-100 | Establece el umbral del silenciador. |
| Combobox AGC | Audio | **FAST** | FAST | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este segmento. |
| Botón NR | DSP | **NR** | desact. | — | Activa el algoritmo de reducción de ruido correspondiente. La disponibilidad depende de la serie de radio y la compilación. |
| Botón NR2 | DSP | **NR2** | desact. | — | Activa el algoritmo de reducción de ruido NR2. Haga clic derecho para abrir Configuración de AetherDSP. |
| Botón RN2 | DSP | **RN2** | desact. | — | Activa el algoritmo de reducción de ruido RN2. |
| Botón NR4 | DSP | **NR4** | desact. | — | Activa el algoritmo de reducción de ruido NR4. Haga clic derecho para abrir Configuración de AetherDSP. |
| Botón MNR | DSP | **MNR** | desact. | — | Activa el algoritmo de reducción de ruido MNR. Haga clic derecho para abrir Configuración de AetherDSP. |
| Botón DFNR | DSP | **DFNR** | desact. | — | Activa el algoritmo de reducción de ruido DFNR. Haga clic derecho para abrir Configuración de AetherDSP. |
| Botón BNR | DSP | **BNR** | desact. | — | Activa el algoritmo de reducción de ruido BNR. |
| Botón NRL | DSP | **NRL** | desact. | — | Activa el algoritmo de reducción de ruido NRL. |
| Botón NRS | DSP | **NRS** | desact. | — | Activa el algoritmo de reducción de ruido NRS. |
| Botón RNN | DSP | **RNN** | desact. | — | Activa el algoritmo de reducción de ruido RNN. |
| Botón NRF | DSP | **NRF** | desact. | — | Activa el algoritmo de reducción de ruido NRF. |
| Botón ADSP | DSP | **ADSP** | — | — | Abre el diálogo de Configuración de AetherDSP. No seleccionable. |
| Botón AetherVoice | DSP | **AetherVoice** | desact. (no seleccionable) | — | Alterna la Aetherial Audio Channel Strip. |
| Combobox de modo | Mode | **USB** | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este segmento. |
| Botones de ajustes preestablecidos de filtro | Mode | **1**, **2**, **3**, **4** | — | — | Aplica un ajuste preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Alternancia RIT | X/RIT | **RIT** | desact. | — | Activa la sintonización incremental del receptor. La rueda de desplazamiento ajusta el desplazamiento en pasos de 10 Hz. |
| Alternancia XIT | X/RIT | **XIT** | desact. | — | Activa la sintonización incremental del transmisor. La rueda de desplazamiento ajusta el desplazamiento en pasos de 10 Hz. |
| Etiqueta de desplazamiento RIT/XIT | X/RIT | (lectura de desplazamiento) | — | — | Muestra el desplazamiento actual de RIT o XIT. |
| Combobox de canal DAX | DAX | **Off** | Off | Off, 1-8 | Asigna un canal de audio DAX a este segmento. |
| Botón de grosor del marcador | — | (icono de grosor de línea) | 1 px | Off, 1 px, 3 px | Alterna el grosor de la línea del marcador VFO. Se persiste por segmento. |
| Botón de bordes de filtro | — | (icono de borde de filtro) | mostrado | — | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se persiste por segmento. |
| Alternancia de colapso | — | (icono de flecha) | expandido | — | Contrae el panel VFO a una tira compacta de solo frecuencia. Se persiste por segmento. |
| Botón de bloqueo | — | 🔒 (bloqueado) / 🔓 (desbloqueado) | desbloqueado | — | Bloquea la frecuencia VFO. Cuando está bloqueado, se bloquean la sintonización con rueda de desplazamiento y la entrada directa de frecuencia. En modo contraído, se bloquea el desplazamiento sobre el panel. La pantalla de frecuencia muestra una superposición **LOCKED**. Al desbloquear, se elimina la superposición centralmente en SliceModel (#2983). |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Distintivo TX | TX (rojo), oculto | Se muestra cuando este segmento es el segmento de transmisión activo. |
| Distintivo SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un segmento diferente al segmento de recepción activo. El distintivo tiene contraste mejorado para legibilidad. |
| Superposición LOCKED | LOCKED (texto), oculto | Se muestra en la pantalla de frecuencia cuando el VFO está bloqueado. Se elimina al desbloquear. |

## Sintonización con la rueda de desplazamiento

La rueda de desplazamiento sintoniza la frecuencia del segmento. El paso de sintonía depende del modo actual. Si la configuración **Reverse mouse wheel** está habilitada en Ajustes de Interacción, la dirección de sintonización se invierte, por lo que desplazarse hacia arriba disminuye la frecuencia y hacia abajo la aumenta.

---

# Abrir la Aetherial Audio Channel Strip desde la pestaña DSP del VFO

Abre la Aetherial Audio Channel Strip — la suite unificada de DSP de TX/RX — directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla de espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla de espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **AetherVoice** en la pestaña DSP del panel VFO.
3. Haga clic en **AetherVoice**. Aparece la Aetherial Audio Channel Strip.

## Función de cada control

| Control | Etiqueta | Predet. | Comportamiento |
|---------|----------|---------|----------------|
| Botón AetherVoice | **AetherVoice** | desact. (no seleccionable) | Alterna la Aetherial Audio Channel Strip — la suite unificada de DSP de TX/RX. Abarca 2 columnas en la cuadrícula de 4 columnas de DSP. |

## Relacionado

- [Abrir Configuración de AetherDSP desde la pestaña DSP del VFO](open-aetherdsp-settings-from-the-vfo-dsp-tab.md)

---

# Abrir Configuración de AetherDSP desde la pestaña DSP del VFO

Abre el diálogo de Configuración de AetherDSP (algoritmos de reducción de ruido del lado del cliente) directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla de espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla de espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **ADSP** en la pestaña DSP del panel VFO.
3. Haga clic en **ADSP**. Aparece el diálogo de Configuración de AetherDSP.

## Función de cada control

| Control | Etiqueta | Predet. | Comportamiento |
|---------|----------|---------|----------------|
| Botón ADSP | **ADSP** | n/a | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). No seleccionable. Al hacer clic, abre y enfoca el diálogo no modal. |

## Notas

- Haga clic derecho en los botones **NR2**, **NR4**, **MNR** o **DFNR** para abrir el diálogo de Configuración de AetherDSP para ese algoritmo específico.

## Relacionado

- Abrir la Aetherial Audio Channel Strip desde la pestaña DSP del VFO

---

# Uso del silenciador en un panel VFO

Activa o desactiva el silenciador para un segmento y ajusta el umbral del silenciador desde el panel VFO en la pantalla de espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la pantalla de espectro (haga clic en la bandera del marcador VFO si está contraído).

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla de espectro para el segmento deseado para abrir el panel VFO.
2. Haga clic en la pestaña **Audio**.
3. Haga clic en el botón **Squelch** para activar el silenciador para este segmento.
4. Arrastre el deslizador adyacente para establecer el umbral del silenciador (0-100).

## Notas importantes

- El silenciador se desactiva automáticamente en modos **DIGU**, **DIGL**, **CW**, **CWL** y **RTTY**. En modos digitales, RTTY y CW, el audio alimenta decodificadores externos a través de DAX, donde el silenciador no es significativo y puede filtrar señales débiles. En modo CW, la radio también bloquea el silenciador activado a un nivel fijo y rechaza los cambios del lado del cliente.
- Al cambiar a un modo donde el silenciador está desactivado, el estado del silenciador se guarda y se restaura al volver a un modo de voz o FM.
- Las configuraciones del silenciador no se persisten y reflejan solo el estado en vivo de la radio.

## Función de cada control

| Control | Etiqueta | Predet. | Rango válido | Comportamiento |
|---------|----------|---------|--------------|----------------|
| Botón de silenciador | **Squelch** | desact. | — | Activa o desactiva el silenciador para este segmento. |
| Deslizador de silenciador
