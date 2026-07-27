# Copia Asistida — Resumen de Voz a Texto

La Copia Asistida proporciona transcripción en tiempo real de voz a texto para el slice activo, impulsada por whisper.cpp. Decodifica el audio de voz recibido en un transcript desplazable con código de colores, ayudándole a capturar y revisar el contenido del QSO sin depender de notas.

## Antes de comenzar

- Debe estar conectada y activa una radio FLEX-8600.
- El motor whisper.cpp requiere un archivo de modelo; en el primer uso, descargará automáticamente el modelo seleccionado.
- La aceleración por GPU requiere una GPU NVIDIA compatible con suficiente VRAM (modo GPU) o una alternativa solo con CPU (modo CPU).

## Cómo funciona

1. **Abra el panel de Copia Asistida** mediante `View > Copy Assist` o presione `Ctrl+Shift+T`.
2. **Habilite la transcripción** haciendo clic en el botón de alternancia **Enable / Disable**. El indicador de estado del motor mostrará "Downloading model" (primer uso) → "Loading model" → "Listening".
3. **Supervise el transcript** en tiempo real mientras el texto decodificado se desplaza en el campo de solo lectura **Transcript**. El texto está codificado por colores:
   - **Verde** – alta confianza
   - **Amarillo** – confianza media
   - **Rojo** – baja confianza
4. **Vigile la salud del pipeline** mediante el **Indicador de acumulación** — muestra los segundos de audio aún no transcritos. El color del indicador pasa de ámbar a rojo a medida que la acumulación crece.
5. **Ajuste el rendimiento** haciendo clic en el **Botón de configuración** (icono de engranaje) para abrir el diálogo de configuración de Copia Asistida (no modal), donde puede ajustar:
   - **Nivel de modelo** – elija `tiny`, `base`, `small` o `medium` (más grande = más preciso pero más lento/pesado)
   - **Dispositivo de cómputo** – seleccione `GPU (CUDA/Metal)` para inferencia más rápida con GPU o `CPU` para compatibilidad universal
6. **Limpie el búfer** en cualquier momento haciendo clic en el botón **Clear**.

## Función de cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| **Enable / Disable** | botón de alternancia | Deshabilitado | Inicia o detiene el motor whisper.cpp en el audio del slice activo. |
| **Transcript** | campo de texto de solo lectura | — | Visualización de texto desplazable del habla decodificada. Codificado por colores según la confianza (verde/amarillo/rojo). Contiene un botón Clear para vaciar el búfer. |
| **Nivel de modelo** | cuadro combinado | `tiny` | Selecciona el tamaño del modelo whisper. Valores válidos: `tiny`, `base`, `small`, `medium`. |
| **Dispositivo de cómputo** | cuadro combinado | `GPU (CUDA/Metal)` | Selecciona el dispositivo de inferencia. Valores válidos: `GPU` o `CPU`. |
| **Indicador de acumulación** | indicador de estado | 0.0s | Muestra los segundos de audio en el pipeline aún no transcritos. El color cambia de ámbar a rojo a medida que la acumulación crece. |
| **Botón de configuración** | botón pulsador | — | Abre el diálogo de configuración de Copia Asistida (no modal) para nivel de modelo, dispositivo de cómputo y configuración del motor. |
| **Clear** | botón pulsador | — | Limpia el búfer de transcript actual. |

## Consejos

- Comience con el modelo `tiny` para la menor latencia y uso mínimo de recursos. Cambie a `base` o `small` si la precisión es insuficiente y su sistema puede soportar la carga.
- El modo GPU es significativamente más rápido, pero requiere una GPU compatible. Si experimenta tiempos de acumulación elevados, intente cambiar a `GPU` (si está disponible) o reduzca el tamaño del modelo.

## Relacionados

- [Enable speech-to-text transcription on a slice](enable-speech-to-text-transcription-on-a-slice.md)
- [Change the whisper model tier for accuracy vs speed](change-the-whisper-model-tier-for-accuracy-vs-speed.md)
- [Choose GPU or CPU for speech recognition](choose-gpu-or-cpu-for-speech-recognition.md)
- [Read the live transcript with confidence-colored text](read-the-live-transcript-with-confidence-colored-text.md)
- [Clear the transcript buffer](clear-the-transcript-buffer.md)
