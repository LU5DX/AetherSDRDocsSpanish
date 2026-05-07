# FlexControl

`Settings > FlexControl...` abre la configuración del puerto serie para la interfaz de hardware FlexControl, permitiéndole asignar y configurar el puerto serie que AetherSDR utiliza para comunicarse con un control de perilla FlexControl.

## Antes de comenzar

- Un dispositivo de hardware FlexControl debe estar físicamente conectado a su computadora mediante un puerto serie o un adaptador USB-serie.
- AetherSDR debe haber sido compilado con soporte para puerto serie (`HAVE_SERIALPORT`). Si `FlexControl...` no aparece en el menú `Settings`, su compilación no incluye esta funcionalidad.
- AetherSDR debe estar en ejecución.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `FlexControl...`.
3. En el cuadro de diálogo que se abre, seleccione el puerto serie al que está conectado su dispositivo FlexControl.
4. Ajuste cualquier parámetro adicional del puerto serie según sea necesario.
5. Haga clic en el control de confirmación para aplicar la configuración.

## Relacionado

- [USB Cables](usb-cables.md)
- [Configuring AetherSDR Controls](configuring-aethersdr-controls.md)
- [Getting Started](getting-started.md)
