# Descripción general del audio DAX

El applet DAX (Digital Audio eXchange) proporciona un puente de audio por software entre su FLEX-8600 y otras aplicaciones que se ejecutan en su computadora, como programas de modos digitales y programas de registro de QSO. Ofrece control de ganancia de RX por canal e indicación de nivel para cuatro flujos de recepción, además de un único flujo de TX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 para que el applet DAX funcione.
- El applet DAX está oculto por defecto. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para mostrarlo.

## Cómo funciona

El applet DAX crea un puente de audio entre la radio y el subsistema de audio de su sistema operativo. Al hacer clic en **Enable**, AetherSDR inicia el puente de audio DAX, lo que hace que el audio de los slices de la radio esté disponible como dispositivos de audio virtuales que otras aplicaciones pueden seleccionar como su entrada o salida.

El applet muestra cuatro canales de RX (DAX 1–4) y un canal de TX. Cada canal de RX se puede asignar a un slice de la radio; la asignación se muestra en el indicador de estado junto a cada canal. El canal de TX transporta el audio desde su computadora hasta el transmisor de la radio e indica qué slice posee actualmente los privilegios de TX.

Cada canal cuenta con un medidor y un control deslizante de ganancia combinados (MeterSlider). La barra de fondo muestra el nivel de audio en vivo después del fader — el nivel RMS suavizado multiplicado por la ganancia actual —, por lo que la barra refleja el nivel de salida real. Un control deslizante ajustable permite establecer la ganancia. Los cambios de ganancia se guardan inmediatamente.

También puede configurar DAX para que se inicie automáticamente cada vez que AetherSDR se ejecute mediante `Settings > Autostart DAX with AetherSDR`.

## Descripción de cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Enable** | Interruptor maestro. Inicia o detiene el puente de audio DAX. | Off | On / Off | `AutoStartDAX` |
| **DAX 1** ganancia+medidor | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 1. Arrastre el control para ajustar la ganancia. | 0,5 | 0,0–1,0 | `DaxRxGain1` |
| **DAX 2** ganancia+medidor | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 2. | 0,5 | 0,0–1,0 | `DaxRxGain2` |
| **DAX 3** ganancia+medidor | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 3. | 0,5 | 0,0–1,0 | `DaxRxGain3` |
| **DAX 4** ganancia+medidor | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 4. | 0,5 | 0,0–1,0 | `DaxRxGain4` |
| **TX** ganancia+medidor | Medidor de nivel y control deslizante de ganancia combinados para el flujo DAX TX. | 0,5 | 0,0–1,0 | `DaxTxGain` |
| Estado de asignación de slice (RX, por canal) | Indicador de solo lectura que muestra qué slice está enrutado a cada canal DAX RX. Muestra `—` cuando no está asignado, o `Slice A` a `Slice H` cuando está asignado. | — | `—` o `Slice A`–`Slice H` | — |
| Estado de asignación de TX | Indicador de solo lectura que muestra qué slice posee actualmente los privilegios de TX y maneja el flujo DAX TX. Muestra `—` cuando no hay ningún slice TX activo. | — | `—` o `Slice A`–`Slice H` | — |

## Consejos

- Los ajustes de ganancia de todos los canales se guardan inmediatamente en cada evento de arrastre — no es necesario hacer clic en ningún botón de guardado.
- Para que el puente DAX se inicie cada vez que AetherSDR se abra, use `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en **Enable** manualmente en cada sesión.

## Relacionados

- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Autostart DAX on launch](autostart-dax-on-launch.md)
- [Set DAX RX gain per channel](set-dax-rx-gain-per-channel.md)
- [Set DAX TX gain](set-dax-tx-gain.md)
- [See which slice is currently using each DAX channel](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identify which slice is the TX slice](identify-which-slice-is-the-tx-slice.md)
- [Setting up digital modes (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
