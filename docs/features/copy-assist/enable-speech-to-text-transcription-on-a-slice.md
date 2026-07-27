# Habilitar la transcripción de voz a texto en un slice

La transcripción de voz a texto en tiempo real transcribe el audio de voz recibido del slice activo utilizando el motor whisper.cpp. La transcripción aparece en el panel Copy Assist con niveles de confianza codificados por colores.

## Antes de comenzar

- Conéctese a una radio FLEX-8600 y tenga al menos un slice activo
- Asegúrese de que la radio esté recibiendo audio (debe haber una señal presente en el slice)

## Pasos

1. Abra el panel Copy Assist: `View > Copy Assist` o presione `Ctrl+Shift+T`.
2. Haga clic en **Enable / Disable** para iniciar el motor de voz a texto whisper.cpp.
   - El indicador de estado del motor cambia de "Idle" a "Downloading model" (si es necesario), luego a "Loading model" y después a "Listening".
   - Si no hay un modelo disponible, el motor descarga automáticamente el nivel de modelo seleccionado (predeterminado: `tiny`).
3. Hable por el micrófono de la radio o reciba una transmisión en el slice activo.
   - El texto decodificado aparece en el campo **Transcript**, codificado por colores según la confianza (verde = alta, amarillo = media, rojo = baja).
   - El indicador **Backlog** muestra los segundos de audio aún no transcritos; permanece cerca de `0.0s` en condiciones normales de operación.

Para detener la transcripción, haga clic en **Enable / Disable** nuevamente. El estado del motor vuelve a "Idle".

## Qué hace cada control

| Control | Predeterminado | Comportamiento | Clave de configuración |
|---------|----------------|----------------|------------------------|
| Enable / Disable | Deshabilitado | Inicia o detiene el motor de voz a texto whisper.cpp en el audio del slice activo | Ninguna |
| Model tier | `tiny` | Selecciona el tamaño del modelo whisper: `tiny`, `base`, `small` o `medium`. Los modelos más grandes son más precisos pero más lentos | Ninguna |
| Compute device | GPU (CUDA/Metal) | Elige GPU (más rápida, necesita VRAM) o CPU (más lenta, funciona en todas partes) | Ninguna |
| Settings button | — | Abre el cuadro de diálogo de configuración de Copy Assist no modal para el nivel del modelo, dispositivo de cómputo y configuración del motor | Ninguna |
| Clear | — | Limpia el búfer de transcripción actual | Ninguna |
| Transcript | — | Transcripción de solo lectura desplazable con texto coloreado por confianza (verde/amarillo/rojo) | Ninguna |
| Backlog indicator | 0.0s | Segundos de audio no atendido; se colorea de ámbar a rojo a medida que crece el atraso | Ninguna |
| Engine status | Idle | Estados: Idle, Downloading model, Loading model, Listening, Error | Ninguna |

## Consejos

- La transcripción se desplaza automáticamente a medida que aparece texto nuevo. Use el botón **Clear** para vaciar el búfer en cualquier momento.
- Si el dispositivo de cómputo está configurado en GPU pero no hay suficiente VRAM, el motor podría no cargarse. Cambie a CPU en el cuadro de diálogo de configuración o elija un nivel de modelo más pequeño.

## Relacionado

- [Copy Assist — Speech to Text overview](overview.md)
- [Change the whisper model tier for accuracy vs speed](change-the-whisper-model-tier-for-accuracy-vs-speed.md)
- [Choose GPU or CPU for speech recognition](choose-gpu-or-cpu-for-speech-recognition.md)
- [Clear the transcript buffer](clear-the-transcript-buffer.md)
- [Read the live transcript with confidence-colored text](read-the-live-transcript-with-confidence-colored-text.md)
