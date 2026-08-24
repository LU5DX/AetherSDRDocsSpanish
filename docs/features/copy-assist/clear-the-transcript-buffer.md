# Asistente de Copia — Voz a Texto

El panel de Asistente de Copia proporciona transcripción de voz a texto en tiempo real para el slice activo. Utiliza el motor whisper.cpp para decodificar el audio de voz recibido en una transcripción deslizante que se colorea según la confianza: verde para confianza alta, amarillo para media y rojo para baja. El panel incluye un diálogo de configuración para seleccionar el nivel del modelo y el dispositivo de cómputo.

## Habilitar o deshabilitar la transcripción

El panel de Asistente de Copia funciona de forma independiente para el slice activo. Cuando está habilitado, decodifica el audio recibido y muestra la transcripción en tiempo real.

### Antes de comenzar

- Verifique que el panel de Asistente de Copia esté abierto (**View > Copy Assist**, o presione Ctrl+Shift+T).
- Confirme que un slice esté activo y recibiendo audio.

### Pasos

1. Abra el panel **Copy Assist**: **View > Copy Assist** (Ctrl+Shift+T).
2. Localice el botón de alternancia **Enable / Disable** en la parte superior del panel.
3. Haga clic en el botón para iniciar el motor de voz a texto. El indicador de estado del motor cambia de **Idle** a **Listening** cuando la decodificación está activa.
4. Haga clic nuevamente en el botón para detener el motor. El indicador de estado del motor vuelve a **Idle**.

### Estado del motor

El indicador muestra el estado actual del motor whisper.cpp:

| Estado | Significado |
|-------|-------------|
| Idle | El motor está detenido. |
| Downloading model | El modelo seleccionado se está descargando en el primer uso. |
| Loading model | El archivo del modelo se está cargando en memoria. |
| Listening | El motor está decodificando activamente el audio del slice. |
| Error | El motor no pudo iniciarse o encontró un error en tiempo de ejecución. |

## Leer la transcripción en vivo con texto coloreado por confianza

La transcripción muestra el habla decodificada a medida que se produce. Cada línea se colorea según la puntuación de confianza que whisper asignó al texto decodificado.

### Codificación de colores

| Color | Confianza | Significado |
|-------|-----------|-------------|
| Verde | Alta | El motor tiene alta confianza en el texto decodificado. |
| Amarillo | Media | El motor tiene confianza moderada: el texto puede contener errores. |
| Rojo | Baja | El motor no tiene confianza: verifique el texto contra el audio. |

### Pasos

1. Habilite la transcripción como se describió anteriormente.
2. Observe el campo de transcripción para ver el habla decodificada.
3. Use la codificación de colores para evaluar la fiabilidad:
   - El texto verde puede considerarse preciso.
   - El texto amarillo probablemente sea correcto pero puede contener errores menores.
   - El texto rojo debe verificarse contra el audio recibido.
4. La transcripción se desplaza automáticamente a medida que se decodifica nuevo texto.

## Seleccionar el nivel del modelo y el dispositivo de cómputo

El diálogo de configuración controla qué modelo de whisper se utiliza y dónde se ejecuta la decodificación.

### Antes de comenzar

- El panel de Asistente de Copia debe estar abierto.
- Para decodificación por GPU, debe estar presente una GPU CUDA o Metal compatible.

### Nivel del modelo

El tamaño del modelo determina la precisión y el uso de recursos.

| Modelo | Precisión | Velocidad | Memoria |
|--------|-----------|-----------|---------|
| tiny | La más baja | La más rápida | Mínima |
| base | Baja | Rápida | Baja |
| small | Media | Moderada | Moderada |
| medium | Alta | Lenta | Alta |

### Dispositivo de cómputo

| Dispositivo | Velocidad | Requisitos |
|-------------|-----------|------------|
| GPU (CUDA/Metal) | Rápida | GPU compatible con VRAM suficiente |
| CPU | Más lenta | Funciona en todos los sistemas |

En el primer arranque, AetherSDR detecta una GPU de forma asíncrona y selecciona la decodificación por GPU cuando está disponible; de lo contrario, recurre a la CPU. Puede anular esta elección en cualquier momento desde el diálogo de configuración.

### Pasos

1. Abra el panel **Copy Assist**.
2. Haga clic en el **botón de Configuración** (⚙) en la parte superior del panel. El diálogo de configuración de Copy Assist se abre como una ventana no modal.
3. Seleccione un **nivel de Modelo** en el menú desplegable:
   - Elija un modelo más grande (medium > small > base > tiny) para mayor precisión cuando la CPU/VRAM lo permita.
   - Elija un modelo más pequeño para una decodificación más rápida en hardware limitado.
4. Seleccione un **Dispositivo de cómputo**:
   - **GPU (CUDA/Metal)** — decodificación más rápida; requiere VRAM suficiente para el modelo seleccionado.
   - **CPU** — funciona en todas partes; más lenta para modelos grandes.
5. El motor aplica la nueva configuración en la siguiente ejecución de decodificación. Si el motor está escuchando, deténgalo y vuelva a habilitarlo para aplicar los cambios de inmediato.

### Arrastre de contexto

El diálogo de configuración de Copy Assist incluye una opción **Context carry** que solo está disponible cuando el backend de whisper está activo. Cuando está habilitada, el contexto decodificado de segmentos anteriores se traslada a la decodificación posterior para mejorar la precisión. Esta opción está deshabilitada cuando el backend sherpa-onnx o remoto está activo porque esos backends no implementan el arrastre de contexto.

## Supervisar el atraso

El indicador de atraso muestra cuántos segundos de audio recibido aún no se han transcrito.

### Comportamiento

- El indicador muestra el atraso en segundos (por ejemplo, `0.0s`).
- Operación normal: el atraso se mantiene cerca de cero.
- Escalamiento: a medida que el atraso crece, el color del indicador cambia:
  - Ámbar — el atraso está aumentando; el motor se está quedando atrás.
  - Rojo — el atraso es significativo; la calidad de decodificación puede verse afectada.

### Pasos

1. Habilite la transcripción.
2. Observe el indicador de atraso junto a la transcripción.
3. Si el atraso aumenta y se mantiene alto:
   - Seleccione un nivel de modelo más pequeño para aumentar la velocidad de decodificación.
   - Cambie el dispositivo de cómputo a GPU si actualmente está en CPU.
   - Verifique el estado del motor: un estado de **Error** puede indicar que el motor se detuvo.

## Limpiar el búfer de transcripción

Limpie la transcripción acumulada entre contactos o para comenzar de nuevo.

### Antes de comenzar

- El panel de Asistente de Copia debe estar abierto (**View > Copy Assist**, o presione Ctrl+Shift+T).
- La transcripción no necesita estar activa para limpiar el búfer.

### Pasos

1. Abra el panel **Copy Assist**: **View > Copy Assist** (Ctrl+Shift+T).
2. Busque el botón **Clear** en la parte inferior del panel de Copy Assist.
3. Haga clic en **Clear**. El campo de texto de transcripción se vacía inmediatamente y cualquier contexto de decodificación arrastrado se elimina para que la nueva transcripción comience desde un prompt limpio.

### Consejos

- Limpiar no detiene la transcripción: el motor continúa escuchando y comenzará a llenar el búfer desde donde quedó.
- La limpieza es instantánea; no aparece ningún diálogo de confirmación.

## Solución de problemas

- **El motor permanece en Idle después de Enable** — Verifique que un slice esté activo y recibiendo audio. Compruebe el indicador de estado del motor para ver un estado de **Error**.
- **El motor muestra Error** — Intente cambiar el dispositivo de cómputo a CPU o seleccione un nivel de modelo más pequeño. Verifique que el archivo del modelo se haya descargado por completo.
- **El atraso aumenta continuamente** — El motor no puede mantener el ritmo del audio. Seleccione un modelo más pequeño o cambie a decodificación por GPU.
- **No aparece transcripción pero el audio es audible** — Revise la codificación de colores de la transcripción; el texto de baja confianza puede ser escaso. Pruebe un nivel de modelo más grande para mayor precisión.
- **Falta la opción de GPU** — No se detectó una GPU CUDA o Metal compatible. Solo está disponible la decodificación por CPU.
- **Context carry está atenuado** — El backend activo (sherpa-onnx o remoto) no implementa el arrastre de contexto. Cambie al backend de whisper para habilitarlo.
- **El botón Clear no responde** — Asegúrese de que el panel esté abierto mediante **View > Copy Assist**. Si el botón sigue sin responder, intente cerrar y volver a abrir el panel.

## Relacionados

- [Habilitar la transcripción de voz a texto en un slice](enable-speech-to-text-transcription-on-a-slice.md)
- [Leer la transcripción en vivo con texto coloreado por confianza](read-the-live-transcript-with-confidence-colored-text.md)
