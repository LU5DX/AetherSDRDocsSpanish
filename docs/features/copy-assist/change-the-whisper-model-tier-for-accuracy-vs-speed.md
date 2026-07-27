# Cambiar el nivel del modelo whisper para equilibrar precisión y velocidad

El panel Copy Assist utiliza un modelo whisper.cpp para transcribir el audio recibido. Los modelos más grandes producen transcripciones más precisas, pero usan más VRAM/RAM y procesan el audio más lentamente. Esta página le muestra cómo cambiar entre niveles de modelo para equilibrar la precisión con la velocidad.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Copy Assist debe estar visible (ábralo con `View > Copy Assist` o presione `Ctrl+Shift+T`).

## Pasos

1. En el panel Copy Assist, haga clic en el **botón Settings** (icono de engranaje). Esto abre el cuadro de diálogo de configuración de Copy Assist.
2. En el cuadro de diálogo, localice el cuadro combinado **Model tier**.
3. Haga clic en el cuadro combinado y seleccione una de las siguientes opciones:
   - **tiny** — El más rápido, menor precisión, menos memoria utilizada.
   - **base** — Velocidad razonable con precisión moderada.
   - **small** — Buena precisión, notablemente más lento.
   - **medium** — Mayor precisión, rendimiento más lento, más VRAM/RAM requerida.
4. Cierre el cuadro de diálogo de configuración. El nuevo nivel de modelo se aplica inmediatamente después de que el motor subyacente se recargue.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Cuadro combinado Model tier | `tiny` | tiny / base / small / medium | Selecciona el tamaño del modelo whisper. Los modelos más grandes mejoran la precisión pero aumentan la latencia y el uso de memoria. |

## Consejos

- Si nota que el **indicador Backlog** aumenta (ámbar→rojo), cambie a un nivel de modelo más pequeño para ayudar al motor a ponerse al día.
- Los archivos del modelo se descargan automáticamente cuando cambia a un nivel por primera vez. Espere una breve demora y se requiere conexión a internet para la descarga inicial.

## Relacionado

- [Copy Assist — Descripción general de voz a texto](overview.md)
- [Elegir GPU o CPU para el reconocimiento de voz](choose-gpu-or-cpu-for-speech-recognition.md)
- [Habilitar la transcripción de voz a texto en un slice](enable-speech-to-text-transcription-on-a-slice.md)
