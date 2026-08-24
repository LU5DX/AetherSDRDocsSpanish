# Cambiar el nivel del modelo whisper para precisión frente a velocidad

El panel **Copy Assist** utiliza un modelo whisper.cpp para transcribir el audio recibido. Los modelos más grandes producen transcripciones más precisas, pero utilizan más VRAM/RAM y procesan el audio más lentamente. Esta página le muestra cómo cambiar entre los niveles de modelo para equilibrar la precisión frente a la velocidad.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- **Copy Assist** debe estar visible (ábralo con `View > Copy Assist` o presione `Ctrl+Shift+T`).

## Pasos

1. En el panel **Copy Assist**, haga clic en el **botón Settings** (ícono de engranaje). Esto abre el diálogo de configuración de Copy Assist.
2. En el diálogo, localice el cuadro combinado **Model tier**.
3. Haga clic en el cuadro combinado y seleccione una de las opciones:
   - **tiny** — Más rápido, menor precisión, menos memoria utilizada.
   - **base** — Velocidad razonable con precisión moderada.
   - **small** — Buena precisión, notablemente más lento.
   - **medium** — Mayor precisión, rendimiento más lento, más VRAM/RAM requerida.
4. Cierre el diálogo de configuración. El nuevo nivel de modelo surte efecto inmediatamente después de que el motor subyacente se recargue.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|----------------|--------------|----------------|
| Cuadro combinado Model tier | `tiny` | tiny / base / small / medium | Selecciona el tamaño del modelo whisper. Los modelos más grandes mejoran la precisión, pero aumentan la latencia y el uso de memoria. |
| Cuadro combinado Compute device | `GPU (CUDA/Metal)` | GPU / CPU | Selecciona si whisper se ejecuta en GPU (más rápido, necesita VRAM) o CPU (más lento, funciona en cualquier sistema). |
| Indicador de acumulación | `0.0s` | — | Segundos de audio recibido aún no transcrito. El color escala de ámbar a rojo a medida que la acumulación crece. |

## Selección de un dispositivo de cómputo

De forma predeterminada, AetherSDR ejecuta whisper en la GPU si hay una disponible. Puede forzar el uso de CPU o seleccionar explícitamente una GPU específica en el diálogo de configuración de Copy Assist.

### Pasos

1. Abra el diálogo de configuración de Copy Assist mediante el **botón Settings**.
2. Localice el cuadro combinado **Compute device**.
3. Elija:
   - **GPU (CUDA/Metal)** — Utiliza una GPU CUDA o Metal. Más rápido, pero requiere suficiente VRAM.
   - **CPU** — Se ejecuta completamente en la CPU. Más lento, pero funciona en cualquier sistema.

> **Nota:** En macOS, la primera consulta a la GPU puede tardar varios segundos porque la biblioteca de shaders de Metal se compila bajo demanda. Esto ocurre en segundo plano y no bloquea el panel Copy Assist.

## Comportamiento de arrastre de contexto

El interruptor **Context-carry** en el panel Copy Assist continúa el prompt decodificado a lo largo de la transcripción. Esto solo está disponible con el backend whisper; al usar backends Sherpa o remotos, el interruptor está deshabilitado.

## Consejos

- Si nota que el **indicador de acumulación** sube (ámbar → rojo), cambie a un nivel de modelo más pequeño o a CPU para ayudar al motor a ponerse al día.
- Los archivos de modelo se descargan automáticamente la primera vez que cambia a un nivel. Espere una breve demora y se requiere conexión a internet para la descarga inicial.
- Si la transcripción es constantemente imprecisa, pruebe primero un nivel de modelo más grande antes de cambiar el dispositivo de cómputo.
- Cuando el **indicador de acumulación** se mantenga alto en GPU, considere cambiar a CPU; algunos sistemas tienen presión de memoria de GPU incluso cuando la GPU está nominalmente disponible.

## Relacionados

- [Copy Assist — descripción general de voz a texto](overview.md)
- [Elegir GPU o CPU para el reconocimiento de voz](choose-gpu-or-cpu-for-speech-recognition.md)
- [Habilitar la transcripción de voz a texto en un slice](enable-speech-to-text-transcription-on-a-slice.md)
