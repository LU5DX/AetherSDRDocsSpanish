# Resumen de Cambio de Dispositivo de Audio

La función de Cambio de Dispositivo de Audio detecta automáticamente cuando se agregan o eliminan dispositivos de audio del sistema mientras AetherSDR está en ejecución y le solicita que confirme o cambie la ruta de audio antes de que se interrumpa el audio.

## Cómo funciona

AetherSDR monitorea el sistema en busca de cambios en los dispositivos de audio mientras se ejecuta. Cuando se agrega o elimina un dispositivo —por ejemplo, cuando se desconecta o reconecta una interfaz de audio USB— el diálogo de Cambio de Dispositivo de Audio aparece automáticamente. El diálogo muestra los dispositivos de audio actuales y disponibles lado a lado para que pueda verificar la ruta o seleccionar un dispositivo diferente antes de que se interrumpa el audio.

El diálogo utiliza un contenedor con estilo temático para mantener la coherencia visual con el resto de la interfaz de la aplicación.

Los dispositivos seleccionados se guardan en AppSettings, por lo que sus elecciones se recuerdan para futuras sesiones.

## Función de cada control

| Control                           | Comportamiento                                                                                                                                                                      | Notas                   |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| **Available Input Devices**       | Muestra todos los dispositivos de audio de entrada detectados. El dispositivo seleccionado actualmente se resalta.                                                                  | Nuevo en v26.5.2.1.     |
| **Available Output Devices**      | Muestra todos los dispositivos de audio de salida detectados. El dispositivo seleccionado actualmente se resalta.                                                                   |                         |
| **Apply**                         | Aplica los dispositivos de audio seleccionados y cierra el diálogo. Guarda la elección en AppSettings. Está diseñado como el botón de acción principal.                              |                         |
| **Cancel**                        | Cierra el diálogo sin cambiar los dispositivos de audio.                                                                                                                            |                         |
| Don't ask me again                | Cuando está marcado y se hace clic en Apply, guarda la bandera de supresión para que el diálogo no se muestre en futuros eventos de conexión en caliente mientras la selección actual aún funcione. | Nuevo en v26.5.3 (#2926). |

## Consejos

- El diálogo aparece automáticamente — no es necesario abrirlo manualmente. Si necesita cambiar los dispositivos de audio en otros momentos, use **Settings > Radio Setup...** y navegue hasta la sección de configuración de audio.
- Los cambios se guardan en AppSettings inmediatamente cuando hace clic en **Apply**.

## Solución de problemas

- **El diálogo de Cambio de Dispositivo de Audio no aparece cuando conecto un nuevo dispositivo de audio USB** — Asegúrese de que el dispositivo esté correctamente conectado y reconocido por su sistema operativo. Es posible que algunos dispositivos requieran la instalación de controladores antes de que AetherSDR pueda detectarlos.
- **Se pierde el audio después de cambiar un dispositivo** — Haga clic en **Apply** para confirmar la selección del nuevo dispositivo; el diálogo no aplicará los cambios hasta que lo haga explícitamente.
