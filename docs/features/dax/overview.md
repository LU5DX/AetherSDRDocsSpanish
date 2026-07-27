# Descripción general de DAX Audio

El applet DAX (Digital Audio eXchange) proporciona un puente de audio por software entre su FLEX-8600 y otras aplicaciones que se ejecutan en su computadora, como programas de modos digitales y programas de registro. Le brinda control de ganancia RX por canal y medición para cuatro flujos de recepción, además de un flujo de TX único.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 para que el applet DAX funcione.
- El applet DAX está oculto de forma predeterminada. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para mostrarlo.

## Cómo funciona

El applet DAX puentea el audio entre la radio y el subsistema de audio de su sistema operativo. Cuando hace clic en **DAX Enable**, AetherSDR inicia el puente de audio DAX, poniendo el audio de los slices de la radio a disposición como dispositivos de audio virtuales que otras aplicaciones pueden seleccionar como su entrada o salida.

El applet muestra cuatro canales RX (DAX 1–4) y un canal TX. Cada canal RX puede asignarse a un slice en la radio; la asignación se muestra en el indicador de estado junto a cada canal. El canal TX transporta el audio desde su computadora al transmisor de la radio y muestra qué slice tiene actualmente los privilegios de TX.

Cada canal tiene un medidor y un control deslizante de ganancia combinados (MeterSlider). La barra de fondo muestra el nivel de audio en vivo post-fader — el nivel RMS suavizado multiplicado por la ganancia actual — por lo que la barra refleja el nivel de salida real. Un control deslizante ajustable establece la ganancia. Los cambios de ganancia se guardan de inmediato.

También puede configurar DAX para que se inicie automáticamente cada vez que se inicie AetherSDR a través de `Settings > Autostart DAX with AetherSDR`.

## Comportamiento específico de la plataforma

En **Windows**, AetherSDR no incluye un controlador de puente de audio DAX incorporado. El botón **DAX Enable**, todos los medidores por canal y TX, y los controles deslizantes de ganancia están ocultos. El applet muestra solo una nota informativa: "No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX." La funcionalidad DAX aún puede utilizarse a través de los controladores SmartSDR DAX de FlexRadio o mediante TCI. Para obtener orientación sobre la configuración, consulte Help > Configuring Data Modes.

En **macOS y Linux**, el applet DAX completo está disponible como se describe a continuación.

## Función de cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **DAX Enable** | Activación general. Inicia o detiene el puente de audio DAX. La etiqueta del botón muestra "Enabled" cuando está activo, "Disabled" cuando está inactivo. | Off | On / Off | `AutoStartDAX` |
| **DAX 1 gain+meter** | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 1. Arrastre el control para establecer la ganancia. Nombre accesible: "DAX RX 1 gain". | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| **DAX 2 gain+meter** | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 2. Nombre accesible: "DAX RX 2 gain". | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| **DAX 3 gain+meter** | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 3. Nombre accesible: "DAX RX 3 gain". | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| **DAX 4 gain+meter** | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 4. Nombre accesible: "DAX RX 4 gain". | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| **TX gain+meter** | Medidor de nivel y control deslizante de ganancia combinados para el flujo DAX TX. Nombre accesible: "DAX TX gain". | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Estado de asignación de slice (RX, por canal) | Indicador de solo lectura que muestra qué slice está enrutado a cada canal DAX RX. Muestra `—` cuando no está asignado, o una letra de slice de la A a la H cuando está asignado. La letra del slice se renderiza con formato de texto enriquecido para mejorar la legibilidad. | — | `—` o `Slice A`–`Slice H` | — |
| Estado de asignación TX | Indicador de solo lectura que muestra qué slice tiene actualmente los privilegios de TX y maneja el flujo DAX TX. Muestra `—` cuando no hay ningún slice TX activo. La letra del slice se renderiza con formato de texto enriquecido. | — | `—` o `Slice A`–`Slice H` | — |

## Notas de rendimiento

En Linux, a partir de AetherSDR v26.5.2.1, la ruta de audio DAX RX utiliza una fuente nativa `pw_stream` de PipeWire, reemplazando el cliente PulseAudio anterior. Esto reduce la latencia de DAX RX de aproximadamente 400 ms a aproximadamente 200 ms.

## Consejos

- En Windows, la funcionalidad DAX está disponible a través de los controladores SmartSDR DAX de FlexRadio o mediante TCI; consulte Help > Configuring Data Modes para obtener instrucciones de configuración.
- La configuración de ganancia de todos los canales se guarda inmediatamente en cada evento de arrastre; no es necesario hacer clic en un botón de guardar.
- Para que el puente DAX se inicie cada vez que se abra AetherSDR, use `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en **Enable** manualmente en cada sesión.
- Los indicadores de estado de asignación de slice ahora utilizan formato de texto enriquecido para mostrar las letras de los slices con mayor claridad.
- El applet utiliza un estilo adaptable al tema; la apariencia visual se adapta al tema seleccionado.
- Cada control deslizante de ganancia tiene un nombre accesible configurado para compatibilidad con lectores de pantalla: "DAX RX N gain" para los canales RX y "DAX TX gain" para el canal TX.

## Relacionados

- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Autostart DAX on launch](autostart-dax-on-launch.md)
- [Set DAX RX gain per channel](set-dax-rx-gain-per-channel.md)
- [Set DAX TX gain](set-dax-tx-gain.md)
- [See which slice is currently using each DAX channel](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identify which slice is the TX slice](identify-which-slice-is-the-tx-slice.md)
- [Setting up digital modes (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
