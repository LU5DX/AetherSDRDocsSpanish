# Descripción general del Cambio de Dispositivo de Audio

La función de Cambio de Dispositivo de Audio detecta automáticamente cuando se agregan o eliminan dispositivos de audio del sistema mientras AetherSDR está en ejecución y le solicita que confirme o cambie el enrutamiento de audio antes de que el audio se interrumpa.

## Cómo funciona

AetherSDR monitorea el sistema en busca de cambios en los dispositivos de audio mientras se ejecuta. Cuando se agrega o elimina un dispositivo — por ejemplo, cuando se desconecta o reconecta una interfaz de audio USB — el diálogo de Cambio de Dispositivo de Audio aparece automáticamente. El diálogo muestra los dispositivos de audio actuales y disponibles lado a lado para que pueda verificar el enrutamiento o seleccionar un dispositivo diferente antes de que el audio se vea afectado.

Los dispositivos seleccionados se guardan en AppSettings, por lo que sus elecciones se recuerdan para sesiones futuras.

## Función de cada control

| Control | Comportamiento |
|--------|----------|
| **Available Input Devices** | Lista todos los dispositivos de audio de entrada detectados. El dispositivo actualmente seleccionado está resaltado. |
| **Available Output Devices** | Lista todos los dispositivos de audio de salida detectados. El dispositivo actualmente seleccionado está resaltado. |
| **Apply** | Aplica los dispositivos de audio seleccionados y cierra el diálogo. Guarda la elección en AppSettings. Está diseñado como el botón de acción principal. |
| **Cancel** | Cierra el diálogo sin cambiar los dispositivos de audio. |

## Consejos

- El diálogo aparece automáticamente — no necesita abrirlo manualmente. Si necesita cambiar los dispositivos de audio en otros momentos, use **Settings > Radio Setup...** y navegue hasta la sección de configuración de audio.
- Los cambios se guardan en AppSettings inmediatamente cuando hace clic en **Apply**.

## Solución de problemas

- **El diálogo de Cambio de Dispositivo de Audio no aparece cuando conecto un nuevo dispositivo de audio USB** — Asegúrese de que el dispositivo esté correctamente conectado y sea reconocido por su sistema operativo. Algunos dispositivos pueden requerir la instalación de controladores antes de que AetherSDR pueda detectarlos.
- **Se pierde el audio después de cambiar un dispositivo** — Haga clic en **Apply** para confirmar la selección del nuevo dispositivo; el diálogo no aplicará los cambios hasta que lo haga explícitamente.
