# Descripción general de Phone/CW

El applet Phone/CW es el panel de control de transmisión adaptado al modo activo en AetherSDR. Muestra los controles de micrófono, procesador y monitor cuando el slice activo está en un modo de voz, y cambia automáticamente a los controles de CW cuando el slice activo está en un modo CW.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet requiere una conexión de radio activa.
- Asegúrese de que el panel de applets sea visible. Si no lo es, seleccione `View > Applet Panel`.

## Cómo funciona

El applet aparece etiquetado como **P/CW** en la bandeja del panel de applets. Haga clic en el botón **P/CW** de la bandeja para mostrarlo u ocultarlo. El panel contiene dos sub-paneles apilados uno detrás del otro:

**Sub-panel Phone** — se muestra cuando el slice activo está en un modo de voz (SSB, AM, FM y similares). Proporciona selección de fuente de micrófono, ganancia, procesamiento de voz, DAX y un monitor de audio TX.

**Sub-panel CW** — se muestra automáticamente cuando el slice activo cambia a un modo CW. Proporciona velocidad de manipulación, retardo de break-in, modo iámbico, tono lateral (sidetone) y controles de tono CW.

No es necesario seleccionar qué sub-panel mostrar; AetherSDR cambia entre ellos según el modo del slice activo.

## Qué hace cada control

### Sub-panel Phone

| Control | Tipo | Descripción | Predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|---|
| Level | Medidor | Nivel de pico de entrada del micrófono en dBFS. Indica –150 cuando el medidor en RX está desactivado y no se está transmitiendo. | — | –40 a +10 dBFS (rojo por encima de 0) | — |
| Compression | Medidor | Cantidad de compresión de voz en dB. El relleno es inverso (barra completa = compresión máxima). | — | –25 a 0 dB | — |
| Mic profile | Cuadro combinado | Carga un perfil de procesamiento de micrófono con nombre desde la lista de perfiles de la radio. | — | Obtenida de la radio | — |
| Mic source | Cuadro combinado | Selecciona la fuente de entrada del micrófono. | — | MIC, BAL, LINE, ACC, PC | — |
| Mic gain | Control deslizante | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se almacena localmente porque la radio siempre reporta el nivel de micrófono como 0 para la fuente PC. | 50 | 0–100 | `PcMicGain` |
| +ACC | Botón de alternancia | Activa la mezcla de entrada de micrófono accesorio junto con la fuente seleccionada. | — | Activado / Desactivado | — |
| PROC | Botón de alternancia | Activa el procesador de voz. | — | Activado / Desactivado | — |
| NOR/DX/DX+ | Control deslizante | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2). | NOR (0) | 0, 1, 2 | — |
| DAX | Botón de alternancia | Activa DAX como fuente de audio TX. | — | Activado / Desactivado | — |
| MON | Botón de alternancia | Activa el monitor de banda lateral TX (para escuchar su propio audio transmitido). | — | Activado / Desactivado | — |
| Monitor volume | Control deslizante | Establece el volumen del monitor de banda lateral. | — | 0–100 | — |

### Sub-panel CW

| Control | Tipo | Descripción | Predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|---|
| ALC | Medidor | Lectura del control automático de nivel. | — | 0–100 (rojo por encima de 80) | — |
| Delay (CW) | Control deslizante | Establece el retardo de break-in CW. | — | 0–2000 ms (paso 10) | — |
| Speed (CW) | Control deslizante | Establece la velocidad de manipulación CW. | — | 5–100 WPM | — |
| Sidetone | Botón de alternancia | Activa el monitor de tono lateral CW. | — | Activado / Desactivado | — |
| Sidetone volume | Control deslizante | Establece el volumen del monitor CW. | — | 0–100 | — |
| L / R pan (CW) | Control deslizante | Establece la posición de panoramización estéreo del monitor CW. | 50 | 0–100 | — |
| Breakin | Botón de alternancia | Activa el modo de break-in completo (QSK). | — | Activado / Desactivado | — |
| Iambic | Botón de alternancia | Activa el manipulador de paleta iámbica. | — | Activado / Desactivado | — |
| Pitch < / > | Cuadro de número | Ajusta el tono lateral y el tono de decodificación CW en pasos de 10 Hz por clic. | 600 Hz | 100–6000 Hz (paso 10) | — |

## Consejos

- Cuando **Mic source** está configurado en PC, la radio no reporta el nivel de micrófono al cliente. AetherSDR almacena el valor de **Mic gain** localmente mediante `PcMicGain`, de modo que la posición del control deslizante se conserva entre sesiones.
- El control deslizante **NOR/DX/DX+** solo afecta el nivel del procesador. **PROC** debe estar activado para que se aplique cualquier compresión.
- El medidor **ALC** aparece en el sub-panel CW, no en el sub-panel Phone. Obsérvelo mientras ajusta el nivel de excitación para evitar sobreexcitación.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Activar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
