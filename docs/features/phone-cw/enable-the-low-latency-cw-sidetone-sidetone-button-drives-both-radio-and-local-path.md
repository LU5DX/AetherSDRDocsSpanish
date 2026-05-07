# Habilitar el sintonizador lateral de baja latencia para CW (el botón de sidetone controla tanto la ruta de la radio como la local)

Al activar el sintonizador lateral (sidetone) de CW en AetherSDR, se habilitan dos rutas simultáneamente: el monitor alimentado por DAX de la radio y un generador de tono local con una latencia de aproximadamente 10 ms. Un solo botón y un solo control deslizante de volumen controlan ambas rutas al unísono, de modo que escucha un tono consistente independientemente de las fluctuaciones de la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión activa a la radio.
- La porción activa (slice) debe estar en modo CW. El panel del applet cambia automáticamente del subpanel Phone al subpanel CW cuando se detecta el modo CW.

## Pasos

1. Si el applet Phone/CW no está visible, haga clic en el botón **P/CW** de la barra lateral derecha para abrirlo.
2. Confirme que se muestra el subpanel CW. Si se muestra el subpanel Phone, cambie la porción activa a un modo CW en la radio; el panel cambia automáticamente.
3. Haga clic en **Sidetone** para habilitar el sintonizador lateral. El botón se ilumina cuando está activo.
4. Ajuste el control deslizante **Sidetone volume** a un nivel cómodo. El control deslizante maneja simultáneamente el volumen del monitor de la radio y el volumen del generador de tono local.
5. Opcionalmente, ajuste **Pitch < / >** para establecer la frecuencia del sintonizador lateral. El tono sigue automáticamente el ajuste `cw_pitch` de la radio, pero puede modificarlo en incrementos de 10 Hz usando los controles **<** y **>**. También puede escribir un valor directamente (100–6000) en el campo QLineEdit (v0.9.8).
6. Para **Delay (CW)**, **Speed (CW)** y **Sidetone volume**, haga clic en el valor numérico y escriba un nuevo número directamente. Pulse Enter o Tab para aplicar. El control deslizante y el valor escrito se mantienen sincronizados automáticamente (v0.9.8).

## Qué hace cada control

| Control         | Tipo                                                                                                                                                                                        | Valor predeterminado                                                                             |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| Delay (CW)      | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (0–2000 ms) directamente en el campo, o arrastre el control deslizante. Llama a TransmitModel::setCwDelay.                       | 500 ms                                                                                           |
| Speed (CW)      | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (5–100 PPM) directamente en el campo, o arrastre el control deslizante. Llama a TransmitModel::setCwSpeed.                      | 20 PPM                                                                                           |
| Sidetone        | Botón de alternancia                                                                                                                                                                        | —                                                                                                |
| Sidetone volume | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (0–100) directamente en el campo, o arrastre el control deslizante. Llama a TransmitModel::setMonGainCw. También ajusta el volumen del generador de tono local al unísono. | 50                                                                                               |
| Pitch < / >     | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para incrementar en pasos de 10 Hz. Llama a TransmitModel::setCwPitch (v0.9.8, #2429).       | 600 Hz                                                                                           |
| L / R pan (CW)  | Control deslizante                                                                                                                                                                          | 50 (centro)                                                                                      |
| Breakin         | Botón de alternancia                                                                                                                                                                        | —                                                                                                |
| Iambic          | Botón de alternancia                                                                                                                                                                        | —                                                                                                |
| ALC             | Medidor                                                                                                                                                                                     | 0–100 (rojo > 80)                                                                                |

## Ingreso directo de valores (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor numérico en el subpanel CW se actualizaron de etiquetas de solo lectura a campos QLineEdit editables:

- **Delay (CW)** — Escriba cualquier valor de 0 a 2000 ms. Pulse Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Speed (CW)** — Escriba cualquier valor de 5 a 100 PPM. Pulse Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Sidetone volume** — Escriba cualquier valor de 0 a 100. Pulse Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Pitch < / >** — Escriba cualquier valor de 100 a 6000 Hz. Pulse Enter o Tab para aplicar. Los botones **<** y **>** incrementan en pasos de 10 Hz.

Cuando escribe un valor fuera del rango válido, el campo limita el valor al límite válido más cercano (paridad con SmartSDR).

## Modo RADE y el control deslizante de nivel de micrófono

Cuando el modo RADE está activo, el control deslizante **Mic gain** funciona como un control de ganancia local en lugar de enviar un comando de nivel de micrófono a la radio. El valor del control deslizante se almacena en `PcMicGain` (el mismo ajuste que se usa cuando la fuente de micrófono es PC) y no se escribe en la propiedad `mic_level` de la radio mientras RADE está activo. Esto evita que el modo RADE sobrescriba silenciosamente su ajuste de micrófono de hardware en la radio.

- El medidor **Level** permanece activo durante RX cuando RADE está habilitado, para que pueda monitorear el nivel de entrada sin transmitir.
- Cuando se desactiva el modo RADE, el control deslizante vuelve a reflejar el `mic_level` de la radio y el medidor Level regresa a su comportamiento de supresión normal (oculto durante RX a menos que `met_in_rx` esté activado).

## Consejos

- El tono y la panorámica del generador de tono local siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No es necesario configurarlos por separado para la ruta local.
- Al hacer doble clic en el control deslizante **L / R pan (CW)** se restablece al centro (50).
- El indicador **Compression** marca 0 dB durante RX. Solo muestra un valor distinto de cero cuando el interbloqueo de la radio informa el estado TRANSMITTING y el procesador de voz (**PROC**) está habilitado. Esto evita que se muestren lecturas obsoletas de la cadena de TX mientras está recibiendo.
- Con **Breakin** desactivado, las pulsaciones de tecla se ponen en cola y es necesario activar TX manualmente con PTT. Con **Breakin** activado (QSK), los flancos de las teclas activan TX directamente y `break_in_delay` controla el tiempo de retención del relé. Ningún sobreenvolvente de PTT automático anula este comportamiento.
- El control deslizante **Delay (CW)** ahora actualiza su valor almacenado en caché inmediatamente al arrastrarlo, evitando que la radio regrese el control deslizante a su posición anterior (v0.9.8, #2428).

## Solución de problemas

- **No se escucha tono a pesar de que Sidetone está habilitado** — Confirme que el control deslizante **Sidetone volume** esté por encima de 0. También verifique que el dispositivo de salida de audio de su sistema esté configurado correctamente, ya que el generador local utiliza la ruta de audio local.
- **El botón Sidetone no es visible** — El subpanel CW solo aparece cuando la porción activa está en modo CW. Cambie la porción activa a CW en la radio; el panel del applet cambia automáticamente.
- **El tono no coincide con lo esperado** — El tono sigue el ajuste `cw_pitch` de la radio. Ajústelo usando **Pitch < / >** en el applet, lo que actualiza el ajuste de la radio en pasos de 10 Hz.
- **El indicador de compresión siempre muestra 0** — Esto es normal durante RX. El indicador está controlado por el estado TRANSMITTING del interbloqueo de la radio. Mostrará compresión solo mientras esté transmitiendo con **PROC** habilitado.
- **Breakin OFF no mantiene TX entre caracteres** — Con **Breakin** desactivado, AetherSDR ya no aplica un sobreenvolvente de PTT automático. Active PTT manualmente antes de enviar y suéltelo cuando termine.
- **El control deslizante Mic gain no tiene efecto en modo RADE** — En modo RADE, el control deslizante establece la ganancia local almacenada como `PcMicGain` y no envía comandos a la radio. Ajuste el control deslizante al nivel deseado; surte efecto en la ruta de audio RADE local.
- **El control deslizante Delay vuelve a su posición tras arrastrarlo** — Este error se corrigió en v0.9.8 (#2428). Actualice a la versión más reciente si experimenta esto.

## Relacionado

- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
- [Pan the CW sidetone left or right](pan-the-cw-sidetone-left-or-right.md)
- [Listen to a TX sidetone monitor](listen-to-a-tx-sidetone-monitor.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Set CW break-in delay](set-cw-break-in-delay.md)
