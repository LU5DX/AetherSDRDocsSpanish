# Habilitar la transcripción de voz a texto en un slice

La transcripción de voz a texto en tiempo real transcribe el audio de voz recibido del slice activo mediante el motor whisper.cpp. La transcripción aparece en el panel Copy Assist con niveles de confianza codificados por colores.

## Antes de comenzar

- Conéctese a una radio FLEX-8600 y tenga al menos un slice activo
- Asegúrese de que la radio esté recibiendo audio (debe haber una señal presente en el slice)

## Pasos

1. Abra el panel Copy Assist: `View > Copy Assist` o presione `Ctrl+Shift+T`.
2. Haga clic en **Enable / Disable** para iniciar el motor de voz a texto whisper.cpp.
   - El indicador de estado del motor cambia de "Idle" a "Downloading model" (si es necesario), luego "Loading model" y después "Listening".
   - Si no hay un modelo disponible, el motor descarga automáticamente el nivel de modelo seleccionado (predeterminado: `tiny`).
3. Hable al micrófono de la radio o reciba una transmisión en el slice activo.
   - El texto decodificado aparece en el campo **Transcript**, codificado por colores según la confianza (verde = alta, amarillo = media, rojo = baja).
   - El indicador **Backlog** muestra los segundos de audio aún no transcritos; se mantiene cerca de `0.0s` en funcionamiento normal.

Para detener la transcripción, haga clic nuevamente en **Enable / Disable**. El estado del motor vuelve a "Idle".

## Qué hace cada control

| Control | Predeterminado | Comportamiento | Clave de configuración |
|---------|---------|----------|-------------|
| Enable / Disable | Deshabilitado | Inicia o detiene el motor de voz a texto whisper.cpp en el audio del slice activo | Ninguna |
| Transcript | — | Transcripción desplazable y de solo lectura del habla decodificada. El texto está codificado por colores según la confianza: verde (alta), amarillo (media), rojo (baja). El botón Clear vacía el búfer | Ninguna |
| Model tier | `tiny` | Tamaño del modelo Whisper. Los modelos más grandes son más precisos pero más lentos y usan más VRAM/RAM | Ninguna |
| Compute device | GPU (CUDA/Metal) | Selecciona si whisper se ejecuta en GPU (más rápido, necesita VRAM) o CPU (más lento, funciona en todas partes). Oculto en equipos sin GPU | Ninguna |
| Backlog indicator | 0.0s | Segundos de audio recibido aún no transcritos. El color cambia de ámbar a rojo a medida que crece el retraso | Ninguna |
| Settings button | — | Abre el diálogo de configuración no modal de Copy Assist para el nivel de modelo, dispositivo de cómputo y configuración del motor | Ninguna |
| Clear | — | Limpia el búfer de transcripción actual | Ninguna |

## Estado del motor

El indicador de estado del motor muestra el estado actual del motor de voz a texto whisper.cpp:

| Estado | Significado |
|-------|-------------|
| Idle | El motor está detenido |
| Downloading model | Se está descargando el modelo |
| Loading model | Se está cargando el modelo en memoria |
| Listening | El motor está transcribiendo activamente |
| Error | Ocurrió una falla durante la operación |

## Selección del dispositivo de cómputo

El selector de dispositivo de cómputo se muestra siempre que exista una GPU, para que pueda seleccionar una GPU (o varias) o forzar la CPU. En equipos sin GPU, el selector está oculto y siempre se usa la CPU.

Cuando la radio se inicia, el motor usa el dispositivo de cómputo predeterminado de la plataforma hasta que se completa la verificación asincrónica de GPU. En macOS, la primera consulta de GPU puede tardar varios segundos en compilar la biblioteca de sombreadores Metal integrada, por lo que la selección inicial del dispositivo se resuelve en segundo plano.

## Arrastre de contexto

La función de arrastre de contexto solo está disponible cuando el backend whisper está activo. Si cambia al backend sherpa-onnx o remoto, el interruptor de arrastre de contexto se deshabilita porque esos backends no implementan este comportamiento.

## Consejos

- La transcripción se desplaza automáticamente a medida que aparece texto nuevo. Use el botón **Clear** para vaciar el búfer en cualquier momento.
- Si el dispositivo de cómputo está configurado en GPU pero no hay suficiente VRAM, el motor podría no cargarse. Cambie a CPU en el diálogo de configuración o elija un nivel de modelo más pequeño.
- Limpiar la transcripción también limpia cualquier contexto de decodificación arrastrado, por lo que la próxima sesión de transcripción comienza con un prompt nuevo.

## Relacionados

- [Copy Assist — Descripción general de voz a texto](overview.md)
- [Cambiar el nivel del modelo whisper entre precisión y velocidad](change-the-whisper-model-tier-for-accuracy-vs-speed.md)
- [Elegir GPU o CPU para el reconocimiento de voz](choose-gpu-or-cpu-for-speech-recognition.md)
- [Limpiar el búfer de transcripción](clear-the-transcript-buffer.md)
- [Leer la transcripción en vivo con texto coloreado por confianza](read-the-live-transcript-with-confidence-colored-text.md)
