# FlexControl

`Settings > FlexControl...` abre la configuración del puerto serie para la interfaz de hardware FlexControl, lo que permite asignar y configurar el puerto serie que AetherSDR utiliza para comunicarse con un controlador de perilla FlexControl.

## Antes de comenzar

- El dispositivo de hardware FlexControl debe estar físicamente conectado a su computadora mediante un adaptador serie o USB-serie.
- AetherSDR debe haber sido compilado con soporte para puerto serie (`HAVE_SERIALPORT`). Si `FlexControl...` no aparece en el menú `Settings`, su versión no incluye esta función.
- AetherSDR debe estar en ejecución.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `FlexControl...`.
3. En el cuadro de diálogo que se abre, seleccione el puerto serie al que está conectado su dispositivo FlexControl.
4. Ajuste los parámetros adicionales del puerto serie según sea necesario.
5. Haga clic en el control de confirmación para aplicar la configuración.

## Relacionados

- [Cables USB](usb-cables.md)
- [Configuración de los controles de AetherSDR](configuring-aethersdr-controls.md)
- [Primeros pasos](getting-started.md)
