# Descripción general de Phone/CW

El applet Phone/CW es un panel de control de transmisión que reconoce el modo activo. Muestra los controles de micrófono, procesador y monitor cuando el slice activo está en un modo de voz, y cambia automáticamente a los controles de CW — incluyendo manipulador (keyer), sidetone y tono (pitch) — cuando el slice activo está en modo CW.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet requiere una conexión de radio activa.
- El applet siempre está presente en el Panel de Applets (barra lateral derecha). Si el panel está oculto, actívelo mediante `View > Applet Panel`. Abra o cierre el applet con el botón de bandeja `P/CW`.

## Cómo funciona

El applet contiene dos subpaneles apilados uno detrás del otro. AetherSDR alterna entre ellos automáticamente según el modo del slice activo:

- **Subpanel Phone** — activo en modos de voz (SSB, AM, FM). Muestra la medición del micrófono, fuente y ganancia del micrófono, procesador de voz, DAX y controles del monitor de TX.
- **Subpanel CW** — activo cuando el slice está en modo CW. Muestra la medición ALC, velocidad y retardo del keyer, break-in, iámbico, sidetone del radio y la ruta de sidetone local del lado del cliente.

### Controles del subpanel Phone

| Control | Función | Valor predeterminado | Rango / Valores | Clave de ajuste |
|---|---|---|---|---|
| Level | Medidor de pico de entrada del micrófono (dBFS). Indica –150 cuando el radio no está transmitiendo y met_in_rx está desactivado. | — | –40 a +10 dBFS (rojo por encima de 0) | — |
| Compression | Medidor de compresión de voz (relleno invertido — la barra se llena de derecha a izquierda). | — | –25 a 0 dB | — |
| Mic profile | Carga un perfil de procesamiento de micrófono con nombre desde la lista de perfiles del radio. | — | Obtenido del radio | — |
| Mic source | Selecciona la fuente de entrada del micrófono. | — | MIC, BAL, LINE, ACC, PC | — |
| Mic gain | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se conserva en el lado del cliente porque el radio siempre reporta mic_level=0 para esa fuente. | 50 | 0–100 | `PcMicGain` |
| +ACC | Activa la mezcla de entrada de micrófono accesorio. Seleccionable. | — | On / Off | — |
| PROC | Activa o desactiva el procesador de voz. Seleccionable. | — | On / Off | — |
| NOR/DX/DX+ | Control deslizante de nivel del procesador con tres posiciones. | 0 (NOR) | 0 = NOR, 1 = DX, 2 = DX+ | — |
| DAX | Habilita DAX como fuente de audio de TX. Seleccionable. | — | On / Off | — |
| MON | Habilita el monitor de banda lateral de TX. Seleccionable. | — | On / Off | — |
| Monitor volume | Establece el volumen del monitor de banda lateral. | — | 0–100 | — |

### Controles del subpanel CW

| Control | Función | Valor predeterminado | Rango / Valores | Clave de ajuste |
|---|---|---|---|---|
| ALC | Medidor de lectura ALC. Rojo por encima de 80. | — | 0–100 | — |
| Delay | Retardo de break-in de CW en milisegundos. | — | 0–2000 ms (paso 10) | — |
| Speed | Velocidad de manipulación CW. | — | 5–100 WPM | — |
| Breakin | Activa o desactiva el break-in completo (QSK). Seleccionable. | — | On / Off | — |
| Iambic | Activa o desactiva el keyer de paleta iámbica. Seleccionable. | — | On / Off | — |
| Pitch < / > | Ajusta el tono de sidetone y decodificación CW en pasos de 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | — |
| Sidetone | Activa o desactiva el monitor de sidetone CW del radio (alimentado por DAX). Seleccionable. | — | On / Off | — |
| Sidetone volume | Establece el volumen del monitor CW del radio. | — | 0–100 | — |
| L / R pan | Panoramización del monitor CW. | 50 | 0–100 | — |
| Local STn | Habilita el sidetone CW local de baja latencia del lado del cliente (~10 ms de latencia), generado independientemente del monitor alimentado por DAX del radio. Funciona con paleta, manipulador recto y texto CWX. Seleccionable. | Off | On / Off | `CwLocalSidetoneEnabled` |
| Local sidetone volume | Volumen del sidetone local, independiente de la ganancia del sidetone del radio. | 50 | 0–100 | `CwLocalSidetoneVolume` |
| Follow | Cuando está activado, el tono del sidetone local sigue la configuración de tono CW del radio. Cuando está desactivado, el control deslizante de tono manual está activo. Seleccionable. | On | On / Off | `CwLocalSidetonePitchFollow` |
| Local sidetone pitch | Tono manual del sidetone local en Hz. Solo ajustable cuando Follow está desactivado. | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` |

## Consejos

- Los subpaneles Phone y CW cambian automáticamente. No es necesario seleccionarlos manualmente — basta con cambiar el modo del slice.
- El sidetone local (Local STn) y el sidetone del radio (Sidetone) son independientes. Puede usar ambos simultáneamente o usar cualquiera de ellos por separado.
- Cuando Mic source está configurado en PC, el valor de Mic gain se almacena en `PcMicGain` en el cliente. El radio no lo conserva.
- Follow está activado de forma predeterminada, por lo que el tono del sidetone local se mantiene sincronizado con el tono CW del radio sin necesidad de ajuste manual.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
- [Habilitar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Habilitar el sidetone CW local de baja latencia (Local STn) para trabajo rápido con paleta, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Ajustar el volumen del sidetone local de forma independiente al monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
- [Hacer que el tono del sidetone local siga el tono CW del radio, o ajustarlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
