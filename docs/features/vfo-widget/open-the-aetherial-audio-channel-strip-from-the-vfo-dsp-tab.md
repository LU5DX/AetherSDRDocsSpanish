# Uso del panel VFO

El panel VFO es un panel de control flotante por segmento anclado al marcador VFO en la visualización del espectro. Proporciona acceso rápido a las configuraciones más usadas por segmento — modo, filtros preestablecidos, selección de antena, ganancia AF, paneo, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.

## Abrir el panel VFO

Haga clic en la bandera del marcador VFO en la visualización del espectro para el segmento deseado. El panel VFO se abre en modo expandido.

## Contraer o expandir el panel VFO

Haga clic en el botón **Collapse toggle** (icono de flecha) en el borde derecho de la barra de título del panel VFO para contraerlo a una tira compacta de solo frecuencia. Vuelva a hacer clic para expandirlo.

## Uso de las pestañas

El panel VFO contiene varias pestañas:

- **Audio** — controles de ganancia AF, paneo, silencio, silenciador y AGC
- **DSP** — botones de algoritmos de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR, NRL, NRS, RNN, NRF), botón ADSP y botón AetherVoice
- **Mode** — selección de modo y botones de filtros preestablecidos
- **X/RIT** — sintonización incremental RIT y XIT
- **DAX** — asignación de canal de audio DAX

Las etiquetas de las pestañas se implementan como botones pulsables que admiten el foco del teclado. Presione Tab para navegar entre las etiquetas; presione Enter o Espacio para activar la pestaña enfocada. Haga clic derecho en la etiqueta de la pestaña Audio para silenciar directamente el segmento actual.

## Función de cada control

| Control | Pestaña | Etiqueta | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------|----------|----------------------|--------------|----------------|
| Botón de antena RX | — | **RX** (icono) | — | — | Abre el menú de selección de antena para la antena receptora de este segmento. El menú muestra la lista de antenas RX de la radio cuando está disponible; de lo contrario, usa la lista general de antenas. |
| Botón de antena TX | — | **TX** (icono) | — | — | Abre el menú de selección de antena para la antena transmisora de este segmento. Solo se muestran antenas adecuadas para transmisión (no puertos exclusivos RX). |
| Visualización de frecuencia | — | (lectura de frecuencia) | — | — | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba la frecuencia en MHz y presione Enter o Tab. En bandas XVTR, la frecuencia máxima admitida es 50000 MHz. En bandas de 2m/70cm (rango 100-999 MHz), los números enteros de 4 a 6 dígitos insertan automáticamente un decimal después del tercer dígito (p. ej., 1446 → 144.6, 14696 → 146.96, 144600 → 144.600). En bandas de microondas, un número entero se interpreta directamente como MHz. Si el segmento está bloqueado, la entrada directa se cancela y se bloquea; consulte las notas del botón Lock a continuación. |
| Insignia de segmento | — | (insignia de color con letra del segmento) | — | — | Muestra la letra del segmento en una insignia de color. Admite formato de texto enriquecido para renderizado HTML (#2606). Haga clic para alternar el foco en el segmento correspondiente. |
| Etiqueta de ancho de filtro | — | (lectura de ancho de banda) | — | — | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de filtros preestablecidos en la pestaña Mode. Usa RxApplet::formatFilterWidth como fuente única de verdad. |
| Deslizador de ganancia AF | Audio | — | 100 | 0-100 | Establece el nivel de salida de audio para este segmento. No se guarda. |
| Deslizador de paneo | Audio | — | 50 | 0-100 | Establece el paneo estéreo izquierdo/derecho para este segmento (50 = centro). El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central en la ranura para mostrar la posición neutra. |
| Botón de silencio | Audio | **Mute** | apagado | — | Silencia la salida de audio de este segmento sin cambiar la configuración de ganancia AF. |
| Botón de silenciador | Audio | **Squelch** | apagado | — | Activa o desactiva el silenciador para este segmento. Desactivado en modos DIGU, DIGL, CW, CWL y RTTY. |
| Deslizador de silenciador | Audio | (adyacente al botón Squelch) | — | 0-100 | Establece el umbral del silenciador. |
| Combo AGC | Audio | **FAST** | FAST | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/soltura del AGC para este segmento. |
| Botón NR | DSP | **NR** | apagado | — | Activa el algoritmo de reducción de ruido correspondiente. La disponibilidad depende de la serie de radio y la compilación. |
| Botón NR2 | DSP | **NR2** | apagado | — | Activa el algoritmo de reducción de ruido NR2. Haga clic derecho para abrir la configuración de AetherDSP. |
| Botón RN2 | DSP | **RN2** | apagado | — | Activa el algoritmo de reducción de ruido RN2. |
| Botón NR4 | DSP | **NR4** | apagado | — | Activa el algoritmo de reducción de ruido NR4. Haga clic derecho para abrir la configuración de AetherDSP. |
| Botón MNR | DSP | **MNR** | apagado | — | Activa el algoritmo de reducción de ruido MNR. Haga clic derecho para abrir la configuración de AetherDSP. |
| Botón DFNR | DSP | **DFNR** | apagado | — | Activa el algoritmo de reducción de ruido DFNR. Haga clic derecho para abrir la configuración de AetherDSP. |
| Botón BNR | DSP | **BNR** | apagado | — | Activa el algoritmo de reducción de ruido BNR. |
| Botón NRL | DSP | **NRL** | apagado | — | Activa el algoritmo de reducción de ruido NRL. |
| Botón NRS | DSP | **NRS** | apagado | — | Activa el algoritmo de reducción de ruido NRS. |
| Botón RNN | DSP | **RNN** | apagado | — | Activa el algoritmo de reducción de ruido RNN. |
| Botón NRF | DSP | **NRF** | apagado | — | Activa el algoritmo de reducción de ruido NRF. |
| Botón ADSP | DSP | **ADSP** | — | — | Abre el diálogo de configuración de AetherDSP. No seleccionable. |
| Botón AetherVoice | DSP | **AetherVoice** | apagado (no seleccionable) | — | Alterna la tira de canales de audio Aetherial. |
| Combo de modo | Mode | **USB** | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este segmento. |
| Botones de filtros preestablecidos | Mode | **1**, **2**, **3**, **4** | — | — | Aplica un ancho de filtro preestablecido guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Alternar RIT | X/RIT | **RIT** | apagado | — | Activa la sintonización incremental del receptor. La rueda del ratón ajusta el desplazamiento en pasos de 10 Hz. |
| Alternar XIT | X/RIT | **XIT** | apagado | — | Activa la sintonización incremental del transmisor. La rueda del ratón ajusta el desplazamiento en pasos de 10 Hz. |
| Etiqueta de desplazamiento RIT/XIT | X/RIT | (lectura de desplazamiento) | — | — | Muestra el desplazamiento actual de RIT o XIT. |
| Combo de canal DAX | DAX | **Off** | Off | Off, 1-8 | Asigna un canal de audio DAX a este segmento. |
| Botón de grosor de marcador | — | (icono de grosor de línea) | 1 px | Off, 1 px, 3 px | Recorre el grosor de la línea del marcador VFO. Se guarda por segmento. |
| Botón de bordes de filtro | — | (icono de borde de filtro) | mostrado | — | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se guarda por segmento. |
| Alternar colapso | — | (icono de flecha) | expandido | — | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se guarda por segmento. |
| Botón de bloqueo | — | 🔒 (bloqueado) / 🔓 (desbloqueado) | desbloqueado | — | Bloquea la frecuencia del VFO. Cuando está bloqueado, la sintonización con la rueda del ratón y la entrada directa de frecuencia están bloqueadas. En modo colapsado, el desplazamiento sobre el panel está bloqueado. La visualización de frecuencia muestra una superposición **LOCKED**. Desbloquear elimina la superposición centralmente en SliceModel (#2983). |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Insignia TX | TX (rojo), oculto | Se muestra cuando este segmento es el segmento de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un segmento diferente al segmento de recepción activo. La insignia tiene contraste mejorado para legibilidad. |
| Superposición LOCKED | LOCKED (texto), oculto | Se muestra en la visualización de frecuencia cuando el VFO está bloqueado. Se borra al desbloquear. |

## Sintonización con la rueda del ratón

La rueda del ratón sintoniza la frecuencia del segmento. El paso de sintonización depende del modo actual. Si la opción **Reverse mouse wheel** está habilitada en la configuración de interacción, la dirección de sintonización se invierte, por lo que desplazarse hacia arriba disminuye la frecuencia y hacia abajo la aumenta.

---

# Abrir la tira de canales de audio Aetherial desde la pestaña DSP del VFO

Abre la tira de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX — directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en la bandera del marcador VFO si está colapsado).

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **AetherVoice** en la pestaña DSP del panel VFO.
3. Haga clic en **AetherVoice**. Aparece la tira de canales de audio Aetherial.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Comportamiento |
|---------|----------|----------------------|----------------|
| Botón AetherVoice | **AetherVoice** | apagado (no seleccionable) | Alterna la tira de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

## Relacionado

- [Abrir la configuración de AetherDSP desde la pestaña DSP del VFO](open-aetherdsp-settings-from-the-vfo-dsp-tab.md)

---

# Abrir la configuración de AetherDSP desde la pestaña DSP del VFO

Abre el diálogo de configuración de AetherDSP (algoritmos de reducción de ruido del lado del cliente) directamente desde el panel VFO sin navegar por los menús.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en la bandera del marcador VFO si está colapsado).

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para el segmento deseado para abrir el panel VFO.
2. Localice el botón **ADSP** en la pestaña DSP del panel VFO.
3. Haga clic en **ADSP**. Aparece el diálogo de configuración de AetherDSP.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Comportamiento |
|---------|----------|----------------------|----------------|
| Botón ADSP | **ADSP** | n/a | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). No seleccionable. Al hacer clic, abre y enfoca el diálogo no modal. |

## Notas

- Haga clic derecho en los botones **NR2**, **NR4**, **MNR** o **DFNR** para abrir el diálogo de configuración de AetherDSP para ese algoritmo específico.

## Relacionado

- Abrir la tira de canales de audio Aetherial desde la pestaña DSP del VFO

---

# Uso del silenciador en un panel VFO

Activa o desactiva el silenciador para un segmento y ajusta el umbral del silenciador desde el panel VFO en la visualización del espectro.

## Antes de comenzar

- Asegúrese de que la radio esté conectada y al menos un segmento esté activo.
- El panel VFO debe estar visible en la visualización del espectro (haga clic en la bandera del marcador VFO si está colapsado).

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para el segmento deseado para abrir el panel VFO.
2. Haga clic en la pestaña **Audio**.
3. Haga clic en el botón **Squelch** para activar el silenciador para este segmento.
4. Arrastre el deslizador adyacente para establecer el umbral del silenciador (0-100).

## Notas importantes

- El silenciador se desactiva automáticamente en los modos **DIGU**, **DIGL**, **CW**, **CWL** y **RTTY**. En modos digitales, RTTY y CW, el audio alimenta decodificadores externos a través de DAX, donde el silenciador no es significativo y puede bloquear señales débiles. En modo CW, la radio también bloquea el silenciador activado a un nivel fijo y rechaza los cambios del lado del cliente.
- Al cambiar a un modo donde el silenciador está desactivado, el estado del silenciador se guarda y se restaura al volver a un modo de voz o FM.
- La configuración del silenciador no se guarda y refleja solo el estado en vivo de la radio.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------|----------------------|--------------|----------------|
| Botón de silenciador | **Squelch** | apagado | — | Activa o desactiva el silenciador para este segmento. |
| Deslizador de silenciador | (adyac
