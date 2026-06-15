# Resumen de audio DAX

El applet DAX (Digital Audio eXchange) proporciona un puente de audio por software entre su FLEX-8600 y otras aplicaciones ejecutándose en su computadora, como software de modos digitales y programas de registro. Le ofrece control de ganancia de RX por canal y medición de nivel para cuatro flujos de recepción, más un flujo de TX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que el applet DAX funcione.
- El applet DAX está oculto por defecto. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para mostrarlo.

## Cómo funciona

El applet DAX crea un puente de audio entre la radio y el subsistema de audio de su sistema operativo. Cuando hace clic en **DAX Enable**, AetherSDR inicia el puente de audio DAX, haciendo que el audio de los slices de la radio esté disponible como dispositivos de audio virtuales que otras aplicaciones pueden seleccionar como su entrada o salida.

El applet muestra cuatro canales de RX (DAX 1–4) y un canal de TX. Cada canal de RX puede asignarse a un slice en la radio; la asignación se muestra en el indicador de estado junto a cada canal. El canal de TX transporta audio desde su computadora al transmisor de la radio y muestra qué slice tiene actualmente los privilegios de TX.

Cada canal tiene un medidor combinado con un control deslizante de ganancia (MeterSlider). La barra de fondo muestra el nivel de audio en vivo después del fader — el nivel RMS suavizado multiplicado por la ganancia actual — por lo que la barra refleja el nivel de salida real. Un control deslizante ajustable permite establecer la ganancia. Los cambios de ganancia se guardan inmediatamente.

También puede configurar DAX para que se inicie automáticamente cada vez que se lance AetherSDR mediante `Settings > Autostart DAX with AetherSDR`.

## Funciones de cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **DAX Enable** | Interruptor principal. Inicia o detiene el puente de audio DAX. La etiqueta del botón es "Enable". | Off | On / Off | `AutoStartDAX` |
| **DAX 1 gain+meter** | Medidor de nivel combinado y control deslizante de ganancia para el canal DAX RX 1. Arrastre el control para ajustar la ganancia. Nombre accesible: "DAX RX 1 gain". | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| **DAX 2 gain+meter** | Medidor de nivel combinado y control deslizante de ganancia para el canal DAX RX 2. Nombre accesible: "DAX RX 2 gain". | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| **DAX 3 gain+meter** | Medidor de nivel combinado y control deslizante de ganancia para el canal DAX RX 3. Nombre accesible: "DAX RX 3 gain". | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| **DAX 4 gain+meter** | Medidor de nivel combinado y control deslizante de ganancia para el canal DAX RX 4. Nombre accesible: "DAX RX 4 gain". | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| **TX gain+meter** | Medidor de nivel combinado y control deslizante de ganancia para el flujo DAX TX. Nombre accesible: "DAX TX gain". | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Estado de asignación de slice (RX, por canal) | Indicador de solo lectura que muestra qué slice está enrutado a cada canal DAX RX. Muestra `—` cuando no está asignado, o una letra de slice de la A a la H cuando está asignado. La letra del slice se muestra con formato de texto enriquecido para mejorar la legibilidad. | — | `—` o `Slice A`–`Slice H` | — |
| Estado de asignación de TX | Indicador de solo lectura que muestra qué slice tiene actualmente los privilegios de TX y maneja el flujo DAX TX. Muestra `—` cuando no hay ningún slice de TX activo. La letra del slice se muestra con formato de texto enriquecido. | — | `—` o `Slice A`–`Slice H` | — |

## Notas de rendimiento

En Linux, a partir de AetherSDR v26.5.2.1, la ruta de audio DAX RX utiliza una fuente nativa `pw_stream` de PipeWire, reemplazando el cliente PulseAudio anterior. Esto reduce la latencia de DAX RX de aproximadamente 400 ms a aproximadamente 200 ms.

## Consejos

- Los ajustes de ganancia para todos los canales se guardan inmediatamente en cada evento de arrastre — no necesita hacer clic en un botón de guardar.
- Para que el puente DAX se inicie cada vez que se abra AetherSDR, use `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en **Enable** manualmente en cada sesión.
- Los indicadores de estado de asignación de slice ahora usan formato de texto enriquecido para mostrar las letras de los slices con mayor claridad.
- El applet utiliza estilo adaptativo al tema; la apariencia visual se ajusta al tema seleccionado.
- Cada control deslizante de ganancia tiene un nombre accesible configurado para compatibilidad con lectores de pantalla: "DAX RX N gain" para canales de RX y "DAX TX gain" para el canal de TX.

## Relacionados

- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Autostart DAX on launch](autostart-dax-on-launch.md)
- [Set DAX RX gain per channel](set-dax-rx-gain-per-channel.md)
- [Set DAX TX gain](set-dax-tx-gain.md)
- [See which slice is currently using each DAX channel](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identify which slice is the TX slice](identify-which-slice-is-the-tx-slice.md)
- [Setting up digital modes (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
