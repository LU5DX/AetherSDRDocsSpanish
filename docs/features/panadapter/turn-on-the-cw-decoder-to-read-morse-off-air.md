# Active el decodificador de CW para leer Morse en el aire

El panel de decodificación de CW aparece debajo del panadapter y muestra el código Morse entrante como texto legible en tiempo real. Úselo para copiar CW en el aire sin un programa de decodificación independiente. En la v26.5.2.1, el decodificador también muestra su propia transmisión en un color cian distintivo, para que pueda separar visualmente su envío del CW entrante cuando ambas direcciones alimentan el mismo panel (#2417).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El audio de la PC debe estar dirigido a AetherSDR. El propio panel muestra el recordatorio "(requires PC Audio)" — la decodificación no funcionará sin esto.
- Sintonice una señal CW y configure el modo en CW en el slice activo.

## Pasos

1. En la barra de título del panadapter, confirme que el slice correcto se muestre en la etiqueta de título "Slice" (por ejemplo, "Slice A").
2. Abra el panel de decodificación de CW. El panel aparece debajo del área de espectro/waterfall y está oculto de forma predeterminada; busque un control o botón de modo CW que lo muestre para el slice activo. Una vez visible, el panel muestra la etiqueta **CW** en azul junto con la sugerencia **(requires PC Audio)**.
3. Observe el área **CW decode text** en la parte inferior del panel. A medida que el decodificador sigue la señal, los caracteres decodificados aparecen y se colorean según la confianza: verde (alta), amarillo, naranja o rojo (baja). Los caracteres decodificados de su propia transmisión aparecen en cian (#5fc8ff) y están separados del texto entrante por un espacio.
4. Verifique la etiqueta **CW stats label** sobre el área de texto. Muestra el tono y la velocidad detectados en el formato `<Hz>  <WPM>`, por ejemplo `600 Hz  20 WPM`. Confirme que coincidan con la señal que está escuchando antes de confiar en la decodificación.

## Función de cada control

| Control                    | Qué hace                                                                                                                                                                   | Predet. |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| Deslizador **Sens**        | Filtra caracteres de baja confianza. Valores más altos rechazan decodificaciones más inciertas.                                                                            | 30      |
| Alternar **🔒P (Lock Pitch)**  | Bloquea el decodificador al tono detectado actual para que deje de buscar.                                                                                                | Apagado |
| Alternar **🔒S (Lock Speed)** | Bloquea el decodificador a la velocidad detectada actual (WPM).                                                                                                             | Apagado |
| Deslizador de rango **Pitch** | Establece el tono mínimo y máximo que busca el decodificador. Un único deslizador de doble manija reemplaza los deslizadores Lo/Hi separados anteriores. Rango: 300–1200 Hz. | 500–700 Hz |
| Deslizador de rango **WPM**   | Establece la velocidad mínima y máxima que busca el decodificador. Un único deslizador de doble manija. Rango: 5–60 WPM.                                                  | 15–40 WPM |
| **CPY ALL**                | Copia todo el búfer de texto decodificado al portapapeles.                                                                                                                | —       |
| **CPY VIS**                | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.                                                                                     | —       |
| **CLR**                    | Borra el búfer de decodificación de CW.                                                                                                                                     | —       |
| **× (close CW)**           | Oculta el panel de decodificación de CW.                                                                                                                                   | —       |
| **CW stats label**         | Indicador que muestra el tono y la velocidad detectados. Solo lectura.                                                                                                     | —       |
| **CW decode text**         | Visualización dinámica de solo lectura de caracteres decodificados, coloreados según la confianza. El clic derecho abre un menú contextual con una opción **Clear** además de las acciones de texto estándar. | —       |

## Cómo aparece la decodificación de TX

Cuando transmite CW, el decodificador captura su manipulación y la muestra en texto cian. Esto le permite verificar su propio envío junto con las señales entrantes. El decodificador aplica el mismo filtro de confianza que la ruta de RX: los caracteres de baja confianza se suprimen. Se inserta un espacio al cambiar entre la decodificación de TX y RX para evitar que las series de colores se fusionen visualmente.

## Congelación del waterfall durante la transmisión

En la v26.6.1, el waterfall ahora se congela cuando cualquier cliente (no solo esta radio) comienza a transmitir. La congelación se activa por el estado de interbloqueo TRANSMITTING de la radio en lugar del borde MOX local, eliminando el artefacto de estela de TX de 10 a 23 segundos que aparecía anteriormente después de dejar de manipular.

Cuando la radio se reconecta, la FPS deseada del panadapter y la duración de la línea del waterfall se reafirman (mediante conciliación interna) para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio.

## Consejos

- Si el área de texto se llena de caracteres de baja confianza (naranja o rojo), aumente **Sens** para filtrarlos. Comience alrededor de 50 y súbalo hasta que los caracteres de ruido desaparezcan.
- Reduzca el rango de búsqueda de tono con el deslizador **Pitch** para que coincida con el tono lateral de la estación que está copiando. Esto reduce las falsas activaciones de señales cercanas.
- Reduzca el rango de velocidad con el deslizador **WPM** para que coincida con la velocidad de envío de la estación que está copiando. Esto mejora la precisión de la decodificación.
- Una vez que la **CW stats label** se estabilice en un tono y velocidad estables, active **🔒P (Lock Pitch)** y **🔒S (Lock Speed)** para evitar que el decodificador se desvíe hacia otra señal.
- Use **CLR** antes de un nuevo QSO para mantener el área de texto legible. También puede hacer clic derecho en el área **CW decode text** y elegir **Clear** en el menú contextual.

## Solución de problemas

- **No aparece texto en el área de decodificación** — Verifique que el audio de la PC esté dirigido a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio. Sin esto, el decodificador no recibe audio y no produce salida.
- **El texto decodificado es principalmente rojo o naranja** — La confianza de la señal es baja. Aumente **Sens**, o reduzca el rango **Pitch** para que coincida con la frecuencia de tono lateral real que se muestra en la **CW stats label**. También reduzca el rango **WPM** para que coincida con la velocidad de envío.
- **Tono o velocidad incorrectos en la etiqueta CW stats label** — No active **🔒P (Lock Pitch)** ni **🔒S (Lock Speed)** hasta que la etiqueta de estadísticas se haya estabilizado en la señal objetivo.
- **El waterfall tiene una larga estela de TX después de dejar de manipular** — En la v26.6.1, esto está corregido. Si aún ve artefactos de estela, asegúrese de estar ejecutando la versión más reciente. Una reconexión de la radio reafirma la FPS correcta y la duración de la línea del waterfall.

## Relacionado

- [Ajuste la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquee el tono o la velocidad del decodificador CW una vez que el seguimiento sea bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copie el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
