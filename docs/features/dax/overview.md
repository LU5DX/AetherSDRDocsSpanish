# Descripción general del audio DAX

El applet DAX (Digital Audio eXchange) proporciona un puente de audio por software entre su FLEX-8600 y otras aplicaciones que se ejecutan en su computadora, como software de modos digitales y programas de registro. Le brinda control de ganancia de RX por canal y medidores para hasta ocho flujos de recepción, además de un único flujo de TX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que el applet DAX sea funcional.
- El applet DAX está oculto por defecto. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para mostrarlo.

## Cómo funciona

El applet DAX conecta el audio entre la radio y el subsistema de audio de su sistema operativo. Cuando hace clic en **DAX Enable**, AetherSDR inicia el puente de audio DAX, haciendo que el audio de los slices de la radio esté disponible como dispositivos de audio virtuales que otras aplicaciones pueden seleccionar como su entrada o salida.

El applet muestra hasta ocho canales de RX (DAX 1–8) y un canal de TX. Cada canal de RX puede asignarse a un slice en la radio; la asignación se muestra en el indicador de estado junto a cada canal. El canal de TX transporta audio desde su computadora al transmisor de la radio y muestra qué slice tiene actualmente los privilegios de TX.

Cada canal tiene un medidor y control deslizante de ganancia combinados (un MeterSlider). La barra de fondo muestra el nivel de audio en vivo post-fader — el nivel RMS suavizado multiplicado por la ganancia actual — de modo que la barra refleja el nivel de salida real. Los niveles de los medidores de RX utilizan suavizado exponencial con ataque rápido y caída lenta. Un control deslizante arrastrable ajusta la ganancia. Los cambios de ganancia se guardan inmediatamente.

También puede configurar DAX para que se inicie automáticamente cada vez que AetherSDR se abre mediante `Settings > Autostart DAX with AetherSDR`.

## Comportamiento específico por plataforma

En **Windows**, AetherSDR no incluye un controlador de puente de audio DAX incorporado. El botón **DAX Enable**, todos los medidores de canal y de TX, y los controles deslizantes de ganancia están ocultos. El applet muestra únicamente una nota informativa: "No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX." La funcionalidad DAX aún puede utilizarse a través de los controladores SmartSDR DAX de FlexRadio o mediante TCI. Para obtener orientación sobre la configuración, consulte Help > Configuring Data Modes.

En **macOS y Linux**, el applet DAX completo está disponible como se describe a continuación.

## Qué hace cada control

| Control                                   | Descripción                                                                                                                                                                                                                                | Predeterminado                                                                                                                       |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| **DAX Enable**                            | Interruptor principal. Inicia o detiene el puente de audio DAX. La etiqueta del botón dice "Enabled" cuando está activo y "Disabled" cuando está inactivo.                                                                                   | Off                                                                                                                                  |
| **DAX 1 gain+meter**                      | Medidor de nivel y control deslizante de ganancia combinados para el canal de RX DAX 1. Arrastre el control para ajustar la ganancia. Nombre accesible: "DAX RX 1 gain".                                                                   | 0.5                                                                                                                                  |
| **DAX 2 gain+meter**                      | Medidor de nivel y control deslizante de ganancia combinados para el canal de RX DAX 2. Nombre accesible: "DAX RX 2 gain".                                                                                                                  | 0.5                                                                                                                                  |
| **DAX 3 gain+meter**                      | Medidor de nivel y control deslizante de ganancia combinados para el canal de RX DAX 3. Nombre accesible: "DAX RX 3 gain".                                                                                                                  | 0.5                                                                                                                                  |
| **DAX 4 gain+meter**                      | Medidor de nivel y control deslizante de ganancia combinados para el canal de RX DAX 4. Nombre accesible: "DAX RX 4 gain".                                                                                                                  | 0.5                                                                                                                                  |
| **TX gain+meter**                         | Medidor de nivel y control deslizante de ganancia combinados para el flujo de TX DAX. Nombre accesible: "DAX TX gain".                                                                                                                      | 0.5                                                                                                                                  |
| Estado de asignación de slice (RX, por canal) | Indicador de solo lectura que muestra qué slice está enrutado a cada canal de RX DAX. Muestra `—` cuando no está asignado, o una letra de slice de la A a la H cuando está asignado. La letra del slice se muestra con formato de texto enriquecido para mejorar la legibilidad. | —                                                                                                                                    |
| Estado de asignación de TX                      | Indicador de solo lectura que muestra qué slice tiene actualmente los privilegios de TX y alimenta el flujo de TX DAX. Muestra `—` cuando no hay ningún slice de TX activo. La letra del slice se muestra con formato de texto enriquecido.                                       | —                                                                                                                                    |
| DAX 5 gain+meter                          | Medidor/control deslizante combinado; arrástrelo para ajustar la ganancia de RX en el canal DAX 5.                                                                                                                                          | Visible solo cuando la radio conectada admite al menos 5 slices.                                                                    |
| DAX 6 gain+meter                          | Medidor/control deslizante combinado; arrástrelo para ajustar la ganancia de RX en el canal DAX 6.                                                                                                                                          | Visible solo cuando la radio conectada admite al menos 6 slices.                                                                    |
| DAX 7 gain+meter                          | Medidor/control deslizante combinado; arrástrelo para ajustar la ganancia de RX en el canal DAX 7.                                                                                                                                          | Visible solo cuando la radio conectada admite al menos 7 slices.                                                                    |
| DAX 8 gain+meter                          | Medidor/control deslizante combinado; arrástrelo para ajustar la ganancia de RX en el canal DAX 8.                                                                                                                                          | Visible solo en una radio con capacidad de 8 slices.                                                                                            |
| Nota de Windows                              | En las compilaciones de Windows, el applet muestra solo la nota 'No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX.' (#4112).                                                                                                                   | Windows no tiene puente DAX incorporado (sin controlador de audio en modo kernel); todos los demás controles se omiten y sus asignadores están protegidos contra valores nulos. |

## Visibilidad de canales según el modelo de radio

Las filas de canales de RX que se muestran en el applet están limitadas según la capacidad de slices de su radio, de modo que nunca verá controles deslizantes de ganancia muertos que no enruten a ningún destino. El applet:

- Oculta las filas de DAX por encima de la capacidad de slices de la radio conectada. Por ejemplo, una radio con 2 slices (p. ej., una 6300/6400) muestra solo las filas DAX 1–2, y una radio de 4 slices (p. ej., una 6600/8600) muestra solo las filas DAX 1–4.
- Mantiene las filas ocultas asignadas en memoria — solo están ocultas, no destruidas — de modo que los mismos ajustes de ganancia persisten independientemente de qué radio conecte.
- Reevalúa la visibilidad de las filas cada vez que se conecta a una radio.

## Notas de rendimiento

En Linux, a partir de AetherSDR v26.5.2.1, la ruta de audio de RX DAX utiliza una fuente nativa `pw_stream` de PipeWire, reemplazando al cliente anterior de PulseAudio. Esto reduce la latencia de RX DAX de aproximadamente 400 ms a aproximadamente 200 ms.

## Consejos

- En Windows, la funcionalidad DAX está disponible a través de los controladores SmartSDR DAX de FlexRadio o mediante TCI — consulte Help > Configuring Data Modes para obtener instrucciones de configuración.
- Los ajustes de ganancia de todos los canales se guardan inmediatamente en cada evento de arrastre — no necesita hacer clic en un botón de guardar.
- Para que el puente DAX se inicie cada vez que AetherSDR se abre, use `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en **Enable** manualmente en cada sesión.
- Los indicadores de estado de asignación de slice ahora usan formato de texto enriquecido para mostrar las letras de los slices con mayor claridad.
- El applet utiliza estilos adaptados al tema; la apariencia visual se adapta al tema que haya seleccionado.
- Cada control deslizante de ganancia tiene un nombre accesible configurado para compatibilidad con lectores de pantalla: "DAX RX N gain" para los canales de RX y "DAX TX gain" para el canal de TX.
- Los niveles de los medidores de RX se suavizan exponencialmente (ataque rápido, caída lenta) para que los picos de audio sean visibles pero el movimiento del medidor siga siendo legible.

## Relacionados

- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Iniciar DAX automáticamente al abrir AetherSDR](autostart-dax-on-launch.md)
- [Establecer la ganancia de RX DAX por canal](set-dax-rx-gain-per-channel.md)
- [Establecer la ganancia de TX DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar qué slice es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
