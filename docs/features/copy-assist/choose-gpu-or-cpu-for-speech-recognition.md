# Elegir GPU o CPU para el reconocimiento de voz

Seleccione si el motor de texto-a-voz whisper.cpp utiliza la GPU o la CPU de su sistema para la transcripción. El procesamiento con GPU es más rápido pero requiere VRAM; el procesamiento con CPU funciona en cualquier sistema pero es más lento.

## Antes de empezar

- Copy Assist debe estar abierto: `View > Copy Assist` (Ctrl+Shift+T)
- Debe haber una radio conectada

## Pasos

1. Abra el cuadro de diálogo de configuración de Copy Assist haciendo clic en **Settings** en el panel de Copy Assist.
2. Localice el cuadro combinado **Compute device**.
3. Seleccione **GPU** o **CPU** en la lista desplegable.
4. Cierre el cuadro de diálogo de configuración.

El nuevo dispositivo de cómputo se utilizará la próxima vez que active la transcripción.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Compute device | GPU (CUDA/Metal) | GPU / CPU | Selecciona si whisper se ejecuta en GPU (más rápido, necesita VRAM) o CPU (más lento, funciona en todas partes) |

## Consejos

- Si observa valores altos de acumulación (ámbar/rojo) con GPU seleccionada, intente primero cambiar a un modelo de nivel más pequeño antes de recurrir a la CPU.
- En sistemas con memoria de GPU limitada (por ejemplo, gráficos integrados), el modo CPU puede ser más estable.

## Relacionados

- [Copy Assist — Descripción general de voz a texto](overview.md)
- [Habilitar la transcripción de voz a texto en una slice](enable-speech-to-text-transcription-on-a-slice.md)
- [Cambiar el nivel del modelo whisper para precisión frente a velocidad](change-the-whisper-model-tier-for-accuracy-vs-speed.md)
