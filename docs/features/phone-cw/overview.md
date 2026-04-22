# Descripción general de Phone/CW

El applet Phone/CW es el panel de control de transmisión con reconocimiento de modo de AetherSDR. Muestra los controles de micrófono, procesador y monitor cuando el slice activo está en un modo de voz, y cambia automáticamente a los controles del manipulador CW cuando el slice activo está en un modo CW.

## Cómo funciona

El applet Phone/CW se encuentra en el panel de applets de la barra lateral derecha. Actívelo o desactívelo con el botón **P/CW** de la bandeja. Internamente utiliza una pila de dos paneles: el panel Phone se muestra para los modos de voz, y el panel CW se muestra para los modos CW. El cambio ocurre automáticamente según el modo del slice activo — no es necesario seleccionarlo manualmente.

### Panel Phone

El panel Phone proporciona los siguientes controles.

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Qué hace |
|---|---|---|---|---|---|
| Level | Medidor | — | −40 a +10 dBFS (rojo por encima de 0) | — | Muestra el nivel de pico de entrada del micrófono en dBFS. Se suprime a −150 cuando no se transmite y el monitoreo del micrófono está desactivado. |
| Compression | Medidor | — | −25 a 0 dB (relleno invertido) | — | Muestra la cantidad de compresión de voz en dB. El relleno va de derecha a izquierda. |
| Mic profile | Cuadro combinado | — | Obtenido del radio | — | Carga el perfil de procesamiento de micrófono indicado. |
| Mic source | Cuadro combinado | — | MIC, BAL, LINE, ACC, PC | — | Selecciona la fuente de entrada del micrófono. |
| Mic gain | Control deslizante | 50 | 0–100 | `PcMicGain` | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se almacena en el lado del cliente; el radio siempre reporta el nivel del micrófono como 0 para la fuente PC. |
| +ACC | Botón de alternancia | — | On / Off | — | Activa la mezcla de la entrada de micrófono accesorio junto con la fuente seleccionada. |
| PROC | Botón de alternancia | — | On / Off | — | Activa o desactiva el procesador de voz. |
| NOR/DX/DX+ | Control deslizante | 0 (NOR) | 0 = NOR, 1 = DX, 2 = DX+ | — | Establece el nivel del procesador de voz en tres pasos. |
| DAX | Botón de alternancia | — | On / Off | — | Habilita DAX como fuente de audio TX. |
| MON | Botón de alternancia | — | On / Off | — | Activa el monitor de banda lateral TX para escuchar su propio audio transmitido. |
| Monitor volume | Control deslizante | — | 0–100 | — | Establece el volumen del monitor de banda lateral. |

### Panel CW

El panel CW proporciona los siguientes controles.

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Qué hace |
|---|---|---|---|---|---|
| ALC | Medidor | — | 0–100 (rojo por encima de 80) | — | Muestra la lectura del control automático de nivel. |
| Delay | Control deslizante | — | 0–2000 ms (paso 10) | — | Establece el retardo de colgado en break-in CW (QSK). |
| Speed | Control deslizante | — | 5–100 WPM | — | Establece la velocidad de manipulación CW. |
| Sidetone | Botón de alternancia | — | On / Off | — | Activa o desactiva el monitor de tono lateral CW. |
| Sidetone volume | Control deslizante | — | 0–100 | — | Establece el volumen del monitor de tono lateral CW. |
| L / R pan | Control deslizante | 50 | 0–100 | — | Desplaza el audio del monitor CW hacia la izquierda o la derecha. |
| Breakin | Botón de alternancia | — | On / Off | — | Activa o desactiva el break-in completo (QSK). |
| Iambic | Botón de alternancia | — | On / Off | — | Activa o desactiva el modo de manipulador de paleta iámbica. |
| Pitch < / > | Cuadro de número | 600 Hz | 100–6000 Hz (paso 10) | — | Ajusta el tono del tono lateral CW y la decodificación. |

## Consejos

- Cuando Mic source está configurado en PC, el radio no reporta el nivel del micrófono a AetherSDR. El valor del control deslizante Mic gain se almacena localmente usando `PcMicGain` y se aplica desde el lado del cliente.
- Los paneles Phone y CW cambian automáticamente. Si los controles no parecen correctos, confirme el modo del slice activo en el panadapter.
- Mantenga el pico del medidor Level por debajo de 0 dBFS durante la operación normal; el medidor se pone rojo por encima de ese umbral.
- Mantenga el medidor ALC por debajo de 80 durante la transmisión CW; el medidor se pone rojo por encima de ese valor.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Habilitar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
