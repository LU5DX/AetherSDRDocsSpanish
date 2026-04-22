# Descripción general de DAX Audio

El applet DAX (Digital Audio eXchange) establece un puente de audio entre AetherSDR y otros programas en su computadora — aplicaciones de modos digitales como WSJT-X o fldigi, software de registro de QSO, o cualquier aplicación que lea o escriba en un dispositivo de audio virtual. Proporciona control de ganancia de RX por canal para cuatro flujos de recepción independientes más un flujo de TX, con medición de nivel en tiempo real en cada uno.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión activa con la radio.
- El applet DAX está oculto de manera predeterminada. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para mostrarlo.

## Cómo funciona

Al hacer clic en **Enable**, AetherSDR inicia el puente de audio DAX. La radio transmite audio para cada slice (segmento de frecuencia) asignado a través del puente; su software de operación se conecta a los dispositivos de audio virtuales resultantes para recibir o enviar audio.

Hay cuatro canales RX independientes (DAX 1–4). Cada canal transporta audio del slice que tenga asignado. La asignación del slice se realiza en la radio o en el slice, no dentro de este applet — el applet muestra la asignación actual como un indicador de solo lectura. El canal TX único transporta audio de transmisión del slice que tenga actualmente los privilegios de TX.

Cada canal RX y el canal TX disponen de un medidor de nivel combinado con un control deslizante de ganancia. La barra del medidor muestra el nivel de audio en tiempo real (después del fader, de modo que mover el control deslizante ofrece retroalimentación visual inmediata). Arrastre el control deslizante para ajustar la ganancia. Los valores de ganancia se guardan de inmediato y se restauran en el próximo inicio.

También puede activar DAX automáticamente cada vez que AetherSDR se inicie mediante `Settings > Autostart DAX with AetherSDR`. Esto escribe el mismo ajuste `AutoStartDAX` que el botón **Enable**.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| **Enable** | Inicia o detiene el puente de audio DAX. Interruptor principal para todos los flujos RX y TX. | Off | On / Off | `AutoStartDAX` |
| Ganancia+medidor **DAX 1** | Establece la ganancia RX y muestra el nivel del canal DAX 1. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor **DAX 2** | Establece la ganancia RX y muestra el nivel del canal DAX 2. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor **DAX 3** | Establece la ganancia RX y muestra el nivel del canal DAX 3. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor **DAX 4** | Establece la ganancia RX y muestra el nivel del canal DAX 4. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| Ganancia+medidor **TX** | Establece la ganancia TX y muestra el nivel del flujo DAX TX. | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Indicador de asignación de slice (por canal RX) | Muestra qué slice está enrutado a este canal DAX. Muestra `—` si no hay ningún slice asignado, o `Slice A`–`Slice H` cuando hay uno asignado. Solo lectura. | — | `—` o `Slice A`–`Slice H` | — |
| Indicador de asignación TX | Muestra qué slice tiene actualmente los privilegios de TX y controla el flujo DAX TX. Solo lectura. | — | `—` o `Slice A`–`Slice H` | — |

## Consejos

- Los cambios de ganancia surten efecto de inmediato y se conservan entre reinicios. No es necesario hacer clic en un control de guardado adicional.
- El color de la barra del medidor de nivel cambia de azul a amarillo y luego a rojo a medida que aumenta el nivel, lo que proporciona una advertencia visual rápida de saturación antes de que afecte a su software de audio.
- Si desea que DAX se ejecute en cada sesión sin tener que hacer clic manualmente en **Enable**, utilice `Settings > Autostart DAX with AetherSDR`. Ambos controles escriben `AutoStartDAX`.

## Solución de problemas

- **El applet DAX no es visible** — Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha. El applet está oculto de manera predeterminada y debe activarse para mostrarlo.
- **La asignación de slice muestra `—` en todos los canales** — Ningún slice ha sido asignado a un canal DAX en la radio. Asigne un canal DAX a un slice desde los controles del slice. El applet refleja la asignación automáticamente una vez realizada.
- **El indicador TX muestra `—`** — Ningún slice tiene actualmente los privilegios de TX, o la radio no está conectada.

## Temas relacionados

- [Activar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia DAX TX](set-dax-tx-gain.md)
- [Ver qué slice utiliza cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar cuál es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
