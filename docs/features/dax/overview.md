# Descripción general de audio DAX

El applet DAX (Digital Audio eXchange) proporciona un puente de audio por software entre su FLEX-8600 y otras aplicaciones que se ejecutan en su computadora, como programas de modos digitales y de registro de QSO. Ofrece control de ganancia y medición por canal RX para cuatro flujos de recepción, más un flujo TX único.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que el applet DAX sea funcional.
- El applet DAX está oculto de forma predeterminada. Haga clic en el botón de bandeja **DAX** de la barra lateral derecha para mostrarlo.

## Cómo funciona

El applet DAX tiende un puente de audio entre la radio y el subsistema de audio del sistema operativo. Al hacer clic en **Enable**, AetherSDR inicia el puente de audio DAX, poniendo a disposición el audio del slice (canal de recepción) de la radio como dispositivos de audio virtuales que otras aplicaciones pueden seleccionar como entrada o salida.

El applet muestra cuatro canales RX (DAX 1–4) y un canal TX. Cada canal RX puede asignarse a un slice de la radio; la asignación se indica en el indicador de estado situado junto a cada canal. El canal TX transporta audio desde su computadora al transmisor de la radio y muestra qué slice tiene actualmente los privilegios de TX.

Cada canal cuenta con un medidor y control deslizante de ganancia combinados (MeterSlider). La barra de fondo muestra el nivel de audio en tiempo real después del fader — el nivel RMS suavizado multiplicado por la ganancia actual — por lo que la barra refleja el nivel de salida real. Un cursor arrastrable establece la ganancia. Los cambios de ganancia se guardan de inmediato.

También puede configurar DAX para que se inicie automáticamente cada vez que AetherSDR arranque mediante `Settings > Autostart DAX with AetherSDR`.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Enable** | Interruptor maestro. Inicia o detiene el puente de audio DAX. | Off | On / Off | `AutoStartDAX` |
| Ganancia+medidor **DAX 1** | Medidor de nivel y control deslizante de ganancia combinados para el canal RX DAX 1. Arrastre el cursor para ajustar la ganancia. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor **DAX 2** | Medidor de nivel y control deslizante de ganancia combinados para el canal RX DAX 2. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor **DAX 3** | Medidor de nivel y control deslizante de ganancia combinados para el canal RX DAX 3. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor **DAX 4** | Medidor de nivel y control deslizante de ganancia combinados para el canal RX DAX 4. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| Ganancia+medidor **TX** | Medidor de nivel y control deslizante de ganancia combinados para el flujo TX DAX. | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Estado de asignación de slice (RX, por canal) | Indicador de solo lectura que muestra qué slice está enrutado a cada canal RX DAX. Muestra `—` cuando no está asignado, o `Slice A` a `Slice H` cuando está asignado. | — | `—` o `Slice A`–`Slice H` | — |
| Estado de asignación TX | Indicador de solo lectura que muestra qué slice tiene actualmente los privilegios de TX y alimenta el flujo TX DAX. Muestra `—` cuando no hay ningún slice TX activo. | — | `—` o `Slice A`–`Slice H` | — |

## Consejos

- La configuración de ganancia de todos los canales se guarda de inmediato en cada evento de arrastre — no es necesario hacer clic en un botón de guardar.
- Para que el puente DAX se inicie cada vez que AetherSDR se abra, use `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en **Enable** manualmente en cada sesión.

## Relacionados

- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software de modos digitales](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Ajustar la ganancia RX DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia TX DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar cuál es el slice TX activo](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
