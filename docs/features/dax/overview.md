# Descripción general de DAX Audio

El applet DAX (Digital Audio eXchange) proporciona un puente de audio por software entre su FLEX-8600 y otras aplicaciones que se ejecutan en su computadora, como programas de modos digitales y de registro de QSO. Ofrece control de ganancia de RX por canal y medición para cuatro flujos de recepción, más un único flujo de TX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que el applet DAX sea funcional.
- El applet DAX está oculto de forma predeterminada. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para mostrarlo.

## Cómo funciona

El applet DAX conecta el audio entre la radio y el subsistema de audio del sistema operativo. Cuando hace clic en **Enable**, AetherSDR inicia el puente de audio DAX, haciendo que el audio del slice (canal de recepción independiente) de la radio esté disponible como dispositivos de audio virtuales que otras aplicaciones pueden seleccionar como entrada o salida.

El applet muestra cuatro canales RX (DAX 1–4) y un canal TX. Cada canal RX puede asignarse a un slice de la radio; la asignación se muestra en el indicador de estado junto a cada canal. El canal TX lleva el audio desde su computadora al transmisor de la radio e indica qué slice tiene actualmente los privilegios de TX.

Cada canal cuenta con un medidor y control deslizante de ganancia combinados (un MeterSlider). La barra de fondo muestra el nivel de audio en tiempo real después del fader — el nivel RMS suavizado multiplicado por la ganancia actual — de modo que la barra refleja el nivel de salida real. Un control deslizable permite ajustar la ganancia. Los cambios de ganancia se guardan de inmediato.

También puede configurar DAX para que se inicie automáticamente cada vez que AetherSDR se abra mediante `Settings > Autostart DAX with AetherSDR`.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Enable** | Interruptor principal. Inicia o detiene el puente de audio DAX. | Off | On / Off | `AutoStartDAX` |
| Ganancia+medidor **DAX 1** | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 1 de DAX. Arrastre el control para ajustar la ganancia. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor **DAX 2** | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 2 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor **DAX 3** | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 3 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor **DAX 4** | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 4 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| Ganancia+medidor **TX** | Medidor de nivel y control deslizante de ganancia combinados para el flujo TX de DAX. | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Estado de asignación de slice (RX, por canal) | Indicador de solo lectura que muestra qué slice está enrutado a cada canal RX de DAX. Muestra `—` cuando no está asignado, o `Slice A` a `Slice H` cuando está asignado. | — | `—` o `Slice A`–`Slice H` | — |
| Estado de asignación TX | Indicador de solo lectura que muestra qué slice tiene actualmente los privilegios de TX y alimenta el flujo TX de DAX. Muestra `—` cuando no hay ningún slice de TX activo. | — | `—` o `Slice A`–`Slice H` | — |

## Consejos

- Los ajustes de ganancia de todos los canales se guardan de inmediato en cada evento de arrastre — no es necesario hacer clic en un botón de guardar.
- Para que el puente DAX se inicie cada vez que AetherSDR se abra, use `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en **Enable** manualmente en cada sesión.

## Temas relacionados

- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software de modos digitales](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Inicio automático de DAX al abrir la aplicación](autostart-dax-on-launch.md)
- [Ajustar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está utilizando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar qué slice es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
