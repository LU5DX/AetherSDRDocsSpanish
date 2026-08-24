# Copia Asistida — Voz a Texto (Speech to Text)

La Copia Asistida proporciona transcripción de voz a texto en tiempo real para la slice activa, impulsada por whisper.cpp. Decodifica el audio de voz recibido en una transcripción desplazable y codificada por colores, ayudándole a capturar y revisar el contenido de los QSO sin depender de notas.

## Antes de comenzar

- Debe haber una radio FLEX-8600 conectada y activa.
- El motor whisper.cpp requiere un archivo de modelo; en el primer uso, descargará automáticamente el modelo seleccionado.
- La aceleración por GPU requiere una GPU NVIDIA compatible (con CUDA) o una Mac con chip Apple Silicon (con Metal) y suficiente VRAM. En equipos sin GPU compatible, el motor funciona en modo CPU.

## Cómo funciona

1. **Abra el panel de Copia Asistida** mediante `View > Copy Assist` o presione `Ctrl+Shift+T`.
2. **Active la transcripción** haciendo clic en el botón de alternancia **Enable / Disable**. El indicador de estado del motor mostrará "Downloading model" (primer uso) → "Loading model" → "Listening".
3. **Supervise la transcripción** en tiempo real mientras el texto decodificado se desplaza en el campo de solo lectura **Transcript**. El texto está codificado por colores según la confianza:
   - **Verde** – confianza alta
   - **Amarillo** – confianza media
   - **Rojo** – confianza baja
4. **Supervise la salud del proceso** mediante el **indicador de acumulación (Backlog)** — muestra los segundos de audio aún no transcritos. El color del indicador pasa de ámbar a rojo a medida que aumenta la acumulación.
5. **Ajuste el rendimiento** haciendo clic en el **botón de configuración (Settings)** (ícono de engranaje) para abrir el diálogo de configuración de Copia Asistida no modal, donde puede ajustar:
   - **Nivel de modelo (Model tier)** – elija `tiny`, `base`, `small` o `medium` (más grande = más preciso pero más lento y usa más VRAM/RAM)
   - **Dispositivo de cómputo (Compute device)** – seleccione `GPU (CUDA/Metal)` para una inferencia más rápida con GPU o `CPU` para compatibilidad universal. La disponibilidad de GPU se sondea de forma asíncrona al inicio; el motor usa el valor predeterminado de la plataforma hasta que la sonda se completa (en macOS, la primera consulta a la GPU puede tardar varios segundos mientras se compila la biblioteca de shaders de Metal).
6. **Limpie el búfer** en cualquier momento haciendo clic en el botón **Clear**. Esto también restablece el contexto de decodificación de whisper para que la siguiente transcripción comience con un prompt limpio.

> **Nota:** El botón **Clear** y la limpieza interna de la transcripción vacían ambos el contexto de decodificación transferido en el backend de whisper, asegurando que la pantalla nueva comience sin estado de prompt obsoleto.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enable / Disable** | botón de alternancia | Deshabilitado | Inicia o detiene el motor whisper.cpp en el audio de la slice activa. |
| **Transcript** | campo de texto de solo lectura | — | Visualización de texto desplazable del habla decodificada. Codificado por colores según la confianza: verde (alta), amarillo (media), rojo (baja). Incluye un botón Clear que vacía el búfer y restablece el contexto de decodificación. |
| **Model tier** | cuadro combinado | `tiny` | Selecciona el tamaño del modelo whisper. Valores válidos: `tiny`, `base`, `small`, `medium`. |
| **Compute device** | cuadro combinado | `GPU (CUDA/Metal)` | Selecciona el dispositivo de inferencia. Valores válidos: `GPU` o `CPU`. |
| **Backlog indicator** | indicador de estado | 0.0s | Muestra los segundos de audio en el proceso que aún no se han transcrito. El color pasa de ámbar a rojo a medida que crece la acumulación. |
| **Settings button** | botón de pulsación | — | Abre el diálogo de configuración de Copia Asistida no modal para nivel de modelo, dispositivo de cómputo y configuración del motor. |
| **Clear** | botón de pulsación | — | Limpia el búfer de transcripción actual y restablece el contexto de decodificación de whisper. |

## Indicador de estado del motor

El panel de Copia Asistida muestra el estado actual del motor de voz a texto:

| Estado | Significado |
|---|---|
| Idle | El motor no está en ejecución. |
| Downloading model | El archivo de modelo seleccionado se está descargando en el primer uso. |
| Loading model | El archivo de modelo se está cargando en memoria. |
| Listening | El motor está decodificando activamente el audio de la slice activa. |
| Error | El motor encontró un problema (por ejemplo, fallo en la descarga del modelo, backend no disponible). |

## Consejos

- Comience con el modelo `tiny` para la latencia más baja y el uso mínimo de recursos. Cambie a `base` o `small` si la precisión es insuficiente y su sistema puede soportar la carga.
- El modo GPU es significativamente más rápido pero requiere una GPU compatible. Si experimenta tiempos de acumulación altos, intente cambiar a `GPU` (si está disponible) o reduzca el tamaño del modelo.
- Una elección explícita de dispositivo de cómputo se recuerda y tiene prioridad sobre la detección automática de GPU. Si luego cambia de hardware, borre la preferencia guardada seleccionando un dispositivo diferente o eliminando la configuración mediante el archivo de configuración.

## Relacionado

- [Habilitar la transcripción de voz a texto en una slice](enable-speech-to-text-transcription-on-a-slice.md)
- [Cambiar el nivel del modelo whisper entre precisión y velocidad](change-the-whisper-model-tier-for-accuracy-vs-speed.md)
- [Elegir GPU o CPU para el reconocimiento de voz](choose-gpu-or-cpu-for-speech-recognition.md)
- [Leer la transcripción en vivo con texto codificado por colores según confianza](read-the-live-transcript-with-confidence-colored-text.md)
- [Limpiar el búfer de transcripción](clear-the-transcript-buffer.md)
