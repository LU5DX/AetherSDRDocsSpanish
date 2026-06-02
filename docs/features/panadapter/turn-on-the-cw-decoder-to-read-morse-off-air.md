# Activar el decodificador CW para leer Morse en el aire

El panel de decodificación CW aparece debajo del panadapter y muestra el código Morse entrante como texto legible en tiempo real. Úselo para copiar CW en el aire sin un programa de decodificación aparte. En la versión 26.5.2.1, el decodificador también muestra su propia transmisión en un color cian distintivo, para que pueda separar visualmente su envío del CW entrante cuando ambas direcciones alimentan el mismo panel (#2417).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El audio de la PC debe estar enrutado a AetherSDR. El panel mismo muestra el recordatorio "(requires PC Audio)"; la decodificación no funcionará sin esto.
- Sintonice una señal CW y establezca el modo en CW en el slice activo.

## Pasos

1. En la barra de título del panadapter, confirme que el slice correcto aparezca en la etiqueta "Slice" (por ejemplo, "Slice A").
2. Abra el panel de decodificación CW. El panel aparece debajo del área de espectro/waterfall y está oculto de forma predeterminada; busque un control o botón CW que lo muestre para el slice activo. Una vez visible, el panel muestra la etiqueta **CW** en azul junto con la sugerencia "(requires PC Audio)".
3. Observe el área de **texto decodificado CW** en la parte inferior del panel. A medida que el decodificador sigue la señal, los caracteres decodificados aparecen y se colorean según la confianza: verde (alta), amarillo, naranja o rojo (baja). Los caracteres decodificados de su propia transmisión aparecen en cian (#5fc8ff) y se separan del texto entrante por un espacio.
4. Verifique la **etiqueta de estadísticas CW** sobre el área de texto. Muestra el tono y la velocidad detectados en el formato `<Hz>  <WPM>`, por ejemplo `600 Hz  20 WPM`. Confirme que coinciden con la señal que está escuchando antes de confiar en la decodificación.

## Función de cada control

| Control                    | Función                                                                                                                                                                     | Valor predeterminado |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| Deslizador **Sens** | Filtra caracteres de baja confianza. Valores más altos rechazan más decodificaciones inciertas. | 30      |
| Alternar **🔒P (Lock Pitch)** | Bloquea el decodificador al tono detectado actual para que deje de buscar. | Off     |
| Alternar **🔒S (Lock Speed)** | Bloquea el decodificador a la velocidad detectada actual (PPM). | Off     |
| Deslizador **Lo** | Tono mínimo que busca el decodificador. Limitado para ser ≤ **Hi**. | 500 Hz  |
| Deslizador **Hi** | Tono máximo que busca el decodificador. Limitado para ser ≥ **Lo**. | 700 Hz  |
| **CPY ALL**                | Copia todo el búfer de texto decodificado al portapapeles. | —       |
| **CPY VIS**                | Copia solo el texto visible actualmente en el área de desplazamiento al portapapeles. | —       |
| **CLR**                    | Limpia el búfer de decodificación CW. | —       |
| **× (close CW)**           | Oculta el panel de decodificación CW. | —       |
| **Etiqueta de estadísticas CW** | Indicador que muestra el tono y la velocidad detectados. Solo lectura. | —       |
| **Texto decodificado CW** | Pantalla de solo lectura con desplazamiento de caracteres decodificados, coloreados por confianza. Al hacer clic derecho se abre un menú contextual con una opción **Clear** además de las acciones de texto estándar. | —       |

## Cómo aparece la decodificación TX

Cuando transmite CW, el decodificador captura su manipulación y la muestra en texto cian. Esto le permite verificar su propio envío junto con las señales entrantes. El decodificador aplica el mismo filtro de confianza que en la ruta RX; los caracteres de baja confianza se suprimen. Se inserta un espacio al cambiar entre decodificación TX y RX para evitar que las líneas de color se fusionen visualmente.

## Congelación del waterfall durante la transmisión

En la versión 26.6.1, el waterfall ahora se congela cuando cualquier cliente (no solo esta radio) comienza a transmitir. La congelación se activa por el estado de interbloqueo TRANSMITTING de la radio en lugar del flanco de MOX local, eliminando el artefacto de rastro TX de 10 a 23 segundos que aparecía anteriormente al desactivar la transmisión.

Cuando la radio se reconecta, se reafirman (mediante reconciliación interna) los FPS del panadapter deseados y la duración de la línea del waterfall para evitar que caigan silenciosamente al valor predeterminado de 10 Hz de la radio.

## Consejos

- Si el área de texto se llena de caracteres de baja confianza (naranja o rojo), aumente **Sens** para filtrarlos. Comience alrededor de 50 y suba hasta que desaparezcan los caracteres de ruido.
- Reduzca el rango de búsqueda de tono con **Lo** y **Hi** para que coincida con el tono de la estación que está copiando. Esto reduce las activaciones falsas de señales cercanas.
- Una vez que la **etiqueta de estadísticas CW** se estabilice en un tono y velocidad estables, active **🔒P (Lock Pitch)** y **🔒S (Lock Speed)** para evitar que el decodificador se desvíe hacia otra señal.
- Use **CLR** antes de un nuevo QSO para mantener el área de texto legible. También puede hacer clic derecho en el área de **texto decodificado CW** y elegir **Clear** en el menú contextual.

## Solución de problemas

- **No aparece texto en el área de decodificación** — Verifique que el audio de la PC esté enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio. Sin esto, el decodificador no recibe audio y no produce salida.
- **El texto decodificado es mayormente rojo o naranja** — La confianza de la señal es baja. Aumente **Sens** o reduzca el rango de tono **Lo**/**Hi** para que coincida con la frecuencia de tono real mostrada en la **etiqueta de estadísticas CW**.
- **Tono o velocidad incorrectos en la etiqueta de estadísticas CW** — No active **🔒P (Lock Pitch)** ni **🔒S (Lock Speed)** hasta que la etiqueta de estadísticas se haya estabilizado en la señal objetivo.
- **El waterfall tiene un rastro TX largo después de desactivar la transmisión** — En la versión 26.6.1, esto está corregido. Si aún ve rastros de artefactos, asegúrese de estar ejecutando la versión más reciente. Una reconexión de la radio reafirma los FPS correctos y la duración de la línea del waterfall.

## Relacionado

- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Resumen del panadapter](overview.md)
