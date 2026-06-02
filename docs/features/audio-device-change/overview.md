# Resumen de cambio de dispositivo de audio

La función de cambio de dispositivo de audio detecta automáticamente cuando se agregan o eliminan dispositivos de audio del sistema mientras AetherSDR está en ejecución y le solicita que confirme o cambie la ruta de audio antes de que se interrumpa el audio.

## Cómo funciona

AetherSDR supervisa el sistema para detectar cambios en los dispositivos de audio mientras está en ejecución. Cuando se agrega o elimina un dispositivo — por ejemplo, cuando se desconecta o reconecta una interfaz de audio USB — el diálogo de cambio de dispositivo de audio aparece automáticamente. El diálogo muestra los dispositivos de audio actuales y disponibles uno al lado del otro para que pueda verificar la ruta o seleccionar un dispositivo diferente antes de que se interrumpa el audio.

El diálogo utiliza un contenedor con estilo temático para mantener la coherencia visual con el resto de la interfaz de la aplicación.

Los dispositivos seleccionados se guardan en AppSettings, por lo que sus elecciones se recuerdan para futuras sesiones.

## Qué hace cada control

| Control                      | Comportamiento                                                                                                                                                | Notas                                         |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------|
| **Available Input Devices**  | Enumera todos los dispositivos de audio de entrada detectados. El dispositivo seleccionado actualmente se resalta.                                            | Nuevo en v26.5.2.1.                           |
| **Available Output Devices** | Enumera todos los dispositivos de audio de salida detectados. El dispositivo seleccionado actualmente se resalta.                                             |                                               |
| **Apply**                    | Aplica los dispositivos de audio seleccionados y cierra el diálogo. Guarda la elección en AppSettings. Estilizado como botón de acción principal.             |                                               |
| **Cancel**                   | Cierra el diálogo sin cambiar los dispositivos de audio.                                                                                                      |                                               |
| Don't ask me again           | Cuando está marcado y se hace clic en Apply, guarda la bandera de supresión para que el diálogo no se muestre en futuros eventos de conexión en caliente mientras la selección actual siga funcionando. | Nuevo en v26.5.3 (#2926).                     |

## Consejos

- El diálogo aparece automáticamente — no es necesario abrirlo manualmente. Si necesita cambiar los dispositivos de audio en otros momentos, use **Settings > Radio Setup...** y navegue hasta la sección de configuración de audio.
- Los cambios se guardan en AppSettings inmediatamente cuando hace clic en **Apply**.

## Solución de problemas

- **El diálogo de cambio de dispositivo de audio no aparece cuando conecto un nuevo dispositivo de audio USB** — Asegúrese de que el dispositivo esté correctamente conectado y reconocido por su sistema operativo. Algunos dispositivos pueden requerir la instalación de controladores antes de que AetherSDR pueda detectarlos.
- **Se pierde el audio después de cambiar un dispositivo** — Haga clic en **Apply** para confirmar la nueva selección de dispositivo; el diálogo no aplicará los cambios hasta que usted lo haga explícitamente.
