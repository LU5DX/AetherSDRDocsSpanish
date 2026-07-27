# Lea la transcripción en vivo con texto codificado por niveles de confianza

Lea la transcripción continua de voz a texto en el panel Copy Assist, donde cada palabra está codificada por colores según el nivel de confianza del motor whisper.cpp.

## Antes de comenzar

- La radio debe estar conectada y un slice activo debe estar recibiendo audio.
- El panel Copy Assist debe estar abierto (`View > Copy Assist`, o presione `Ctrl+Shift+T`).

## Pasos

1. En el panel Copy Assist, haga clic en **Enable** para iniciar el motor de voz a texto en el audio del slice activo.
2. Espere a que el indicador de estado del motor muestre "Listening".
3. Hable al micrófono o reciba audio en el slice activo.
4. Lea la transcripción. Cada palabra o frase se muestra en un color que representa la confianza del motor whisper:
   - **Verde** — confianza alta
   - **Amarillo** — confianza media
   - **Rojo** — confianza baja

## Función de cada control

| Control | Comportamiento |
|---------|----------------|
| **Enable / Disable** | Botón de alternancia. Inicia o detiene el motor de voz a texto whisper.cpp en el audio del slice activo. Valor predeterminado: Deshabilitado. |
| **Transcript** | Campo de texto continuo de solo lectura. Muestra el habla decodificada con colores basados en la confianza. |
| **Model tier** | Cuadro combinado. Selecciona el tamaño del modelo whisper: tiny (predeterminado), base, small o medium. Los modelos más grandes mejoran la precisión pero usan más VRAM/RAM y son más lentos. |
| **Compute device** | Cuadro combinado. Selecciona GPU (CUDA/Metal) o CPU para el procesamiento whisper. Valor predeterminado: GPU (CUDA/Metal). |
| **Backlog indicator** | Muestra los segundos de audio recibido aún no transcritos. Escala de ámbar a rojo a medida que crece el atraso. |
| **Settings button** | Abre el diálogo de configuración de Copy Assist para el nivel del modelo, dispositivo de cómputo y configuración del motor. |
| **Clear** | Vacía el búfer de transcripción actual. |

## Consejos

- El indicador de atraso muestra qué tan rezagado está el motor. Si permanece en rojo por más de unos segundos, un nivel de modelo más pequeño o el cómputo por CPU pueden ayudar en equipos de gama baja.

## Relacionados

- [Copy Assist — Resumen de voz a texto](overview.md)
- [Habilitar la transcripción de voz a texto en un slice](enable-speech-to-text-transcription-on-a-slice.md)
- [Cambiar el nivel del modelo whisper para precisión vs velocidad](change-the-whisper-model-tier-for-accuracy-vs-speed.md)
- [Elegir GPU o CPU para reconocimiento de voz](choose-gpu-or-cpu-for-speech-recognition.md)
- [Limpiar el búfer de transcripción](clear-the-transcript-buffer.md)
