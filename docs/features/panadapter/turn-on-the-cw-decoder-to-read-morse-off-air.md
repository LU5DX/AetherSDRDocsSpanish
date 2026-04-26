# Activar el decodificador de CW para leer Morse en el aire

El panel de decodificación de CW aparece debajo del panadapter y muestra el código Morse entrante como texto legible en tiempo real. Úselo para copiar CW del aire sin necesidad de un programa de decodificación independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El audio de la PC debe estar enrutado hacia AetherSDR. El panel muestra el aviso "(requires PC Audio)" — la decodificación no funcionará sin él.
- Sintonice una señal CW y establezca el modo CW en el slice activo.

## Pasos

1. En la barra de título del panadapter, confirme que el slice correcto aparece en la etiqueta "Slice" (por ejemplo, "Slice A").
2. Abra el panel de decodificación de CW. El panel aparece debajo del área del espectro/waterfall y está oculto de forma predeterminada — busque un control de CW o un botón de modo que lo muestre para el slice activo. Una vez visible, el panel muestra la etiqueta **CW** en azul junto al aviso **(requires PC Audio)**.
3. Observe el área de **texto decodificado de CW** en la parte inferior del panel. A medida que el decodificador rastrea la señal, los caracteres decodificados aparecen en secuencia y se colorean según la confianza: verde (alta), amarillo, naranja o rojo (baja).
4. Revise la **etiqueta de estadísticas de CW** sobre el área de texto. Muestra el tono detectado y la velocidad en el formato `<Hz>  <WPM>`, por ejemplo `600 Hz  20 WPM`. Confirme que coincidan con la señal que está escuchando antes de confiar en la decodificación.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango / unidad | Clave persistente |
|---|---|---|---|---|
| Control deslizante **Sens** | Filtra los caracteres de baja confianza. Valores más altos rechazan más decodificaciones inciertas. | 30 | 0–100 | `CwDecoderSensitivity` |
| Interruptor **🔒P (Lock Pitch)** | Fija el decodificador al tono detectado actualmente para que deje de buscarlo. | Off | On / Off | — |
| Interruptor **🔒S (Lock Speed)** | Fija el decodificador a la velocidad detectada actualmente (WPM). | Off | On / Off | — |
| Control deslizante **Lo** | Tono mínimo que el decodificador busca. Limitado a ser ≤ **Hi**. | 500 Hz | 300–1200 Hz | — |
| Control deslizante **Hi** | Tono máximo que el decodificador busca. Limitado a ser ≥ **Lo**. | 700 Hz | 300–1200 Hz | — |
| **CPY ALL** | Copia todo el buffer de texto decodificado al portapapeles. | — | — | — |
| **CPY VIS** | Copia únicamente el texto visible en el área de desplazamiento al portapapeles. | — | — | — |
| **CLR** | Borra el buffer de decodificación de CW. | — | — | — |
| **× (close CW)** | Oculta el panel de decodificación de CW. | — | — | — |
| Etiqueta de estadísticas de CW | Indicador que muestra el tono y la velocidad detectados. Solo lectura. | — | `<Hz>  <WPM>` | — |
| Texto decodificado de CW | Pantalla continua de solo lectura con los caracteres decodificados, coloreados según la confianza. | — | — | — |

## Consejos

- Si el área de texto se llena de caracteres de baja confianza (naranja o rojo), aumente **Sens** para filtrarlos. Comience alrededor de 50 y suba hasta que desaparezcan los caracteres de ruido.
- Estreche el rango de búsqueda de tono con **Lo** y **Hi** para que coincida con el tono lateral de la estación que está copiando. Esto reduce las detecciones falsas provocadas por señales cercanas.
- Una vez que la etiqueta de estadísticas de CW se estabilice en un tono y velocidad constantes, active **🔒P (Lock Pitch)** y **🔒S (Lock Speed)** para evitar que el decodificador se desvíe hacia otra señal.
- Use **CLR** antes de un nuevo QSO para mantener el área de texto legible.

## Solución de problemas

- **No aparece texto en el área de decodificación** — Verifique que el audio de la PC esté enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio. Sin él, el decodificador no recibe audio y no produce ninguna salida.
- **El texto decodificado es mayormente rojo o naranja** — La confianza en la señal es baja. Aumente **Sens** o estreche el rango de tono **Lo**/**Hi** para que coincida con la frecuencia real del tono lateral que muestra la etiqueta de estadísticas de CW.
- **El tono o la velocidad mostrados en la etiqueta de estadísticas de CW son incorrectos** — No active **🔒P (Lock Pitch)** ni **🔒S (Lock Speed)** hasta que la etiqueta de estadísticas se haya estabilizado en la señal objetivo.

## Relacionado

- [Ajustar la sensibilidad del decodificador de CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador de CW cuando el rastreo es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto de CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
