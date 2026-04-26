# Descripción general de DAX Audio

El applet DAX (Digital Audio eXchange) actúa como puente de audio entre el FLEX-8600 y otros programas en su computadora — por ejemplo, programas de modos digitales como WSJT-X o fldigi. Proporciona controles deslizantes de ganancia RX y medidores por canal para los canales DAX 1–4, un único control deslizante de ganancia TX con su medidor, e indicadores de asignación de slice (rebanada de espectro) que muestran qué slice está enrutado a cada canal.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión activa con la radio.
- El applet DAX está oculto de forma predeterminada. Haga clic en el botón **DAX** de la barra lateral derecha para mostrarlo.

## Cómo funciona

Al hacer clic en **Enable**, AetherSDR inicia el puente de audio DAX y guarda su elección en `AutoStartDAX`. El puente expone hasta cuatro flujos de audio RX (uno por asignación de slice) y un flujo de audio TX al sistema operativo del equipo.

Cada canal RX (DAX 1–4) dispone de un medidor combinado con control deslizante de ganancia. El medidor muestra el nivel RMS suavizado del audio entrante después del fader — el nivel mostrado refleja la ganancia multiplicada por la señal bruta, de modo que arrastrar el control ofrece retroalimentación visual inmediata. El canal TX funciona de la misma manera para el audio saliente.

Los indicadores de asignación de slice junto a cada canal muestran qué slice (A–H) está enrutado en ese momento. Si no hay ningún slice asignado, el indicador muestra —. El indicador TX muestra qué slice tiene actualmente los privilegios de transmisión; no es editable por el usuario desde aquí.

Para iniciar DAX automáticamente cada vez que se inicia AetherSDR, utilice `Settings > Autostart DAX with AetherSDR`.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable** | Inicia o detiene el puente de audio DAX. Interruptor principal para todos los flujos RX y TX. | Off | On / Off | `AutoStartDAX` |
| Ganancia+medidor **DAX 1** | Establece la ganancia RX y muestra el nivel de audio del canal DAX 1. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor **DAX 2** | Establece la ganancia RX y muestra el nivel de audio del canal DAX 2. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor **DAX 3** | Establece la ganancia RX y muestra el nivel de audio del canal DAX 3. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor **DAX 4** | Establece la ganancia RX y muestra el nivel de audio del canal DAX 4. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| Ganancia+medidor **TX** | Establece la ganancia TX y muestra el nivel de audio del flujo DAX TX. | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Indicador de asignación de slice (por canal RX) | Muestra qué slice (p. ej., Slice A) está enrutado a este canal DAX, o — si no hay ninguno asignado. | — | — o Slice A–H | — |
| Indicador de asignación TX | Muestra qué slice tiene actualmente los privilegios de TX y gestiona el flujo DAX TX. | — | — o Slice A–H | — |

## Consejos

- Los valores de ganancia y medidor se guardan inmediatamente al arrastrar un control deslizante. Persisten entre reinicios.
- La dinámica del medidor utiliza un ataque rápido y una caída lenta, lo que coincide con el comportamiento de los medidores en el resto de AetherSDR.

## Temas relacionados

- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia DAX TX](set-dax-tx-gain.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar cuál es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
