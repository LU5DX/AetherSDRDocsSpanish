# Resumen de audio DAX

El applet DAX (Digital Audio eXchange) proporciona un puente de audio por software entre su FLEX-8600 y otras aplicaciones que se ejecutan en su computadora, como software de modos digitales y programas de registro. Ofrece control de ganancia RX por canal y medidores para cuatro flujos de recepción, además de un único flujo TX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 para que el applet DAX funcione.
- El applet DAX está oculto de forma predeterminada. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para mostrarlo.

## Cómo funciona

El applet DAX conecta el audio entre la radio y el subsistema de audio de su sistema operativo. Cuando hace clic en **DAX Enable**, AetherSDR inicia el puente de audio DAX, haciendo que el audio del slice de la radio esté disponible como dispositivos de audio virtuales que otras aplicaciones pueden seleccionar como su entrada o salida.

El applet muestra cuatro canales RX (DAX 1–4) y un canal TX. Cada canal RX puede asignarse a un slice de la radio; la asignación se muestra en el indicador de estado junto a cada canal. El canal TX transporta el audio desde su computadora al transmisor de la radio y muestra qué slice tiene actualmente los privilegios TX.

Cada canal tiene un medidor combinado y un control deslizante de ganancia (un MeterSlider). La barra de fondo muestra el nivel de audio en vivo después del fader — el nivel RMS suavizado multiplicado por la ganancia actual —, por lo que la barra refleja el nivel de salida real. Un control deslizante ajustable establece la ganancia. Los cambios de ganancia se guardan inmediatamente.

También puede configurar DAX para que se inicie automáticamente cada vez que AetherSDR se abre mediante `Settings > Autostart DAX with AetherSDR`.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **DAX Enable** | Encendido/apagado principal. Inicia o detiene el puente de audio DAX. La etiqueta del botón es "Enable". | Off | On / Off | `AutoStartDAX` |
| **DAX 1** ganancia+medidor | Medidor de nivel combinado y control deslizante de ganancia para el canal RX DAX 1. Arrastre el control para establecer la ganancia. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| **DAX 2** ganancia+medidor | Medidor de nivel combinado y control deslizante de ganancia para el canal RX DAX 2. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| **DAX 3** ganancia+medidor | Medidor de nivel combinado y control deslizante de ganancia para el canal RX DAX 3. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| **DAX 4** ganancia+medidor | Medidor de nivel combinado y control deslizante de ganancia para el canal RX DAX 4. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| **TX** ganancia+medidor | Medidor de nivel combinado y control deslizante de ganancia para el flujo TX DAX. | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Estado de asignación de slice (RX, por canal) | Indicador de solo lectura que muestra qué slice está enrutado a cada canal RX DAX. Muestra `—` cuando no está asignado, o una letra de slice de la A a la H cuando está asignado. La letra del slice se renderiza con formato de texto enriquecido para mejorar la legibilidad. | — | `—` o `Slice A`–`Slice H` | — |
| Estado de asignación TX | Indicador de solo lectura que muestra qué slice tiene actualmente los privilegios TX y maneja el flujo TX DAX. Muestra `—` cuando no hay ningún slice TX activo. La letra del slice se renderiza con formato de texto enriquecido. | — | `—` o `Slice A`–`Slice H` | — |

## Notas de rendimiento

En Linux, a partir de AetherSDR v26.5.2.1, la ruta de audio RX DAX utiliza una fuente nativa `pw_stream` de PipeWire, reemplazando el cliente PulseAudio anterior. Esto reduce la latencia RX DAX de aproximadamente 400 ms a aproximadamente 200 ms.

## Consejos

- Los ajustes de ganancia de todos los canales se guardan inmediatamente en cada evento de arrastre — no necesita hacer clic en un botón de guardar.
- Para que el puente DAX se inicie cada vez que AetherSDR se abre, use `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic manualmente en **Enable** cada sesión.
- Los indicadores de estado de asignación de slice ahora usan formato de texto enriquecido para mostrar las letras de los slices con mayor claridad.

## Relacionado

- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Autostart DAX on launch](autostart-dax-on-launch.md)
- [Set DAX RX gain per channel](set-dax-rx-gain-per-channel.md)
- [Set DAX TX gain](set-dax-tx-gain.md)
- [See which slice is currently using each DAX channel](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identify which slice is the TX slice](identify-which-slice-is-the-tx-slice.md)
- [Setting up digital modes (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
