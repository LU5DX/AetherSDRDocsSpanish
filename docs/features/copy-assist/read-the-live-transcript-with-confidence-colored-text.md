# Lea la transcripción en vivo con texto coloreado por confianza

Lea la transcripción de voz a texto en el panel Copy Assist, donde cada palabra está codificada por color según el nivel de confianza del motor whisper.cpp.

## Antes de comenzar

- La radio debe estar conectada y un slice activo debe estar recibiendo audio.
- El panel Copy Assist debe estar abierto (`View > Copy Assist`, o presione `Ctrl+Shift+T`).

## Pasos

1. En el panel Copy Assist, haga clic en **Enable / Disable** para iniciar el motor de voz a texto en el audio del slice activo.
2. Espere a que el indicador de estado del motor muestre "Listening".
3. Hable al micrófono o reciba audio en el slice activo.
4. Lea la transcripción. Cada palabra o frase se muestra en un color que representa la confianza del motor whisper:
   - **Verde** — confianza alta
   - **Amarillo** — confianza media
   - **Rojo** — confianza baja

## Qué hace cada control

| Control | Comportamiento |
|---------|----------------|
| **Enable / Disable** | Botón de alternancia. Inicia o detiene el motor de voz a texto whisper.cpp en el audio del slice activo. Valor predeterminado: Deshabilitado. |
| **Transcript** | Campo de texto de solo lectura con desplazamiento. Muestra el habla decodificada con colores basados en la confianza. El botón **Clear** que se encuentra junto a él vacía el búfer y también elimina el contexto de decodificación acumulado, de modo que la siguiente transcripción comience desde una indicación limpia. |
| **Model tier** | Cuadro combinado. Selecciona el tamaño del modelo whisper: tiny (predeterminado), base, small o medium. Los modelos más grandes mejoran la precisión pero usan más VRAM/RAM y son más lentos. |
| **Compute device** | Cuadro combinado. Selecciona GPU (CUDA/Metal) o CPU para el procesamiento whisper. Valor predeterminado: GPU (CUDA/Metal). |
| **Backlog indicator** | Muestra los segundos de audio recibido que aún no se han transcrito. Cambia de ámbar a rojo a medida que el atraso aumenta. |
| **Settings button** | Abre el diálogo de configuración de Copy Assist para el nivel de modelo, el dispositivo de cómputo y la configuración del motor. |
| **Clear** | Vacía el búfer de transcripción actual y elimina el contexto de decodificación acumulado. |

## Estado del motor

El indicador de estado del motor muestra el estado actual del motor de voz a texto whisper.cpp:

| Estado | Significado |
|--------|-------------|
| **Idle** | El motor está detenido o aún no se ha iniciado. |
| **Downloading model** | El motor está descargando el archivo de modelo seleccionado. |
| **Loading model** | El motor está cargando el modelo en memoria. |
| **Listening** | El motor está decodificando activamente el audio recibido. |
| **Error** | El motor encontró un problema y no puede continuar. |

## Consejos

- El indicador de atraso muestra qué tan rezagado está el motor. Si permanece en rojo por más de unos segundos, un nivel de modelo más pequeño o cómputo por CPU puede ayudar en hardware de gama baja.
- En el primer uso, el motor puede necesitar descargar el modelo seleccionado. Espere a que el indicador de estado muestre "Listening" antes de esperar una transcripción.

## Relacionado

- [Copy Assist — Descripción general de voz a texto](overview.md)
- [Habilitar la transcripción de voz a texto en un slice](enable-speech-to-text-transcription-on-a-slice.md)
- [Cambiar el nivel del modelo whisper para precisión frente a velocidad](change-the-whisper-model-tier-for-accuracy-vs-speed.md)
- [Elegir GPU o CPU para el reconocimiento de voz](choose-gpu-or-cpu-for-speech-recognition.md)
- [Limpiar el búfer de transcripción](clear-the-transcript-buffer.md)
