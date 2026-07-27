# Activee el decodificador de CW para leer Morse en el aire

El panel de decodificación de CW aparece debajo del panadapter y muestra el código Morse entrante como texto legible en tiempo real. Úselo para copiar CW del aire sin necesidad de un programa de decodificación independiente. En la versión v26.5.2.1, el decodificador también muestra su propia transmisión en un color cian distintivo, para que pueda separar visualmente su envío del CW entrante cuando ambas direcciones alimentan el mismo panel (#2417).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El audio de la PC debe estar enrutado a AetherSDR. El propio panel muestra el recordatorio "(requires PC Audio)"; la decodificación no funcionará sin él.
- Sintonice una señal CW y configure el modo en CW en el slice activo.

## Pasos

1. En la barra de título del panadapter, confirme que el slice correcto se muestre en la etiqueta de título "Slice" (por ejemplo, "Slice A").
2. Abra el panel de decodificación de CW. El panel aparece debajo del área de espectro/waterfall y está oculto de forma predeterminada; busque un control o botón de modo CW que lo muestre para el slice activo. Una vez visible, el panel muestra la etiqueta **CW** en azul junto con la indicación **(requires PC Audio)**.
3. Observe el área de **texto decodificado CW** en la parte inferior del panel. A medida que el decodificador sigue la señal, los caracteres decodificados aparecen y se colorean según la confianza: verde (alta), amarillo, naranja o rojo (baja). Los caracteres decodificados de su propia transmisión aparecen en cian (#5fc8ff) y están separados del texto entrante por un espacio.
4. Verifique la **etiqueta de estadísticas CW** sobre el área de texto. Muestra el tono y la velocidad detectados en el formato `<Hz> <WPM>`, por ejemplo `600 Hz 20 WPM`. Confirme que coincidan con la señal que está escuchando antes de confiar en la decodificación.

## Función de cada control

| Control                    | Qué hace                                                                                                                                                                | Valor predeterminado |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| Control deslizante **Sens** | Filtra caracteres de baja confianza. Los valores más altos rechazan más decodificaciones inciertas.                                                                                             | 30      |
| Interruptor **🔒P (Lock Pitch)** | Bloquea el decodificador al tono detectado actual para que deje de buscar.                                                                                                      | Off     |
| Interruptor **🔒S (Lock Speed)** | Bloquea el decodificador a la velocidad detectada actual (WPM).                                                                                                                      | Off     |
| Control deslizante de rango **Pitch** | Establece el tono mínimo y máximo que busca el decodificador. Un control deslizante de doble manija reemplaza los controles Hi/Lo separados anteriores. Rango: 300–1200 Hz.                     | 500–700 Hz |
| Control deslizante de rango **WPM** | Establece la velocidad mínima y máxima que busca el decodificador. Un control deslizante de doble manija. Rango: 5–60 WPM.                                                                   | 15–40 WPM |
| Botón **A-**              | Disminuye el tamaño de fuente del texto decodificado en 1 píxel (se conserva entre sesiones).                                                                                               | —       |
| Botón **A+**              | Aumenta el tamaño de fuente del texto decodificado en 1 píxel (se conserva entre sesiones).                                                                                               | —       |
| **CPY ALL**                | Copia todo el búfer de texto decodificado al portapapeles.                                                                                                                     | —       |
| **CPY VIS**                | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.                                                                                                 | —       |
| **CLR**                    | Limpia el búfer de decodificación CW.                                                                                                                                                | —       |
| **× (cerrar CW)**           | Oculta el panel de decodificación CW.                                                                                                                                                  | —       |
| **Asa de arrastre (borde superior)**   | Una fina franja horizontal sobre los controles del panel. Arrástrela hacia arriba o hacia abajo con el cursor de redimensionamiento vertical para ajustar la altura del panel (60-600 px) y revelar más historial de texto decodificado. Se conserva entre sesiones. | 80 px (predeterminado) |
| **Etiqueta de estadísticas CW**         | Indicador que muestra el tono y la velocidad detectados. Solo lectura.                                                                                                                      | —       |
| **Texto decodificado CW**         | Visualización continua de solo lectura de caracteres decodificados, coloreados según la confianza. Haga clic derecho para abrir un menú contextual con una opción **Clear** además de las acciones de texto estándar. El tamaño de fuente se controla con los botones A- / A+. | 13 px (predeterminado) |

## Cómo aparece la decodificación de TX

Cuando transmite CW, el decodificador captura su manipulación y la muestra en texto cian. Esto le permite verificar su propia transmisión junto con las señales entrantes. El decodificador aplica el mismo filtro de confianza que la ruta RX; los caracteres de baja confianza se suprimen. Se inserta un espacio al cambiar entre la decodificación de TX y RX para evitar que las series de colores se fusionen visualmente.

## Congelación del waterfall durante la transmisión

En la versión v26.6.1, el waterfall ahora se congela cuando cualquier cliente (no solo esta radio) comienza a transmitir. La congelación se activa por el estado INTERLOCK TRANSMITTING de la radio en lugar del borde MOX local, eliminando el artefacto de estela de TX de 10–23 segundos que aparecía anteriormente después de dejar de manipular.

Cuando la radio se reconecta, se reafirman el FPS deseado del panadapter y la duración de la línea del waterfall (mediante reconciliación interna) para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio.

## Preferencias del panel conservadas

En la versión v26.7.4, la altura del panel de decodificación CW y el tamaño de fuente se guardan y restauran entre sesiones, eliminando la necesidad de reajustarlos cada vez que abre el panel. La configuración se almacena en `CwDecodeSettings::panelHeight` y `CwDecodeSettings::fontPx`.

- Altura del panel: 60–600 px. Arrastre el asa de redimensionamiento (franja horizontal fina en la parte superior del panel) para ajustar.
- Tamaño de fuente: 8–32 px. Use los botones **A-** y **A+** para cambiarlo.

## Consejos

- Si el área de texto se llena de caracteres de baja confianza (naranja o rojo), aumente **Sens** para filtrarlos. Comience alrededor de 50 y aumente hasta que desaparezcan los caracteres de ruido.
- Reduzca el rango de búsqueda de tono con el control deslizante **Pitch** para que coincida con el tono lateral de la estación que está copiando. Esto reduce las falsas activaciones de señales cercanas.
- Reduzca el rango de velocidad con el control deslizante **WPM** para que coincida con la velocidad de envío de la estación que está copiando. Esto mejora la precisión de la decodificación.
- Una vez que la **etiqueta de estadísticas CW** se estabilice en un tono y velocidad estables, active **🔒P (Lock Pitch)** y **🔒S (Lock Speed)** para evitar que el decodificador se desvíe hacia otra señal.
- Use **CLR** antes de un nuevo QSO para mantener el área de texto legible. También puede hacer clic derecho en el área de **texto decodificado CW** y elegir **Clear** en el menú contextual.
- Ajuste los botones **A- / A+** a un tamaño de fuente cómodo para la resolución de su monitor y la distancia de visualización. La configuración se conserva automáticamente.
- Arrastre el **asa de redimensionamiento** en la parte superior del panel para mostrar más o menos historial decodificado. La nueva altura se guarda cuando cierra el panel o reinicia AetherSDR.

## Solución de problemas

- **No aparece texto en el área de decodificación**: Verifique que el audio de la PC esté enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio. Sin él, el decodificador no recibe audio y no produce salida.
- **El texto decodificado es principalmente rojo o naranja**: La confianza de la señal es baja. Aumente **Sens** o reduzca el rango de **Pitch** para que coincida con la frecuencia de tono lateral real que se muestra en la **etiqueta de estadísticas CW**. También reduzca el rango de **WPM** para que coincida con la velocidad de envío.
- **Tono o velocidad incorrectos mostrados en la etiqueta de estadísticas CW**: No active **🔒P (Lock Pitch)** ni **🔒S (Lock Speed)** hasta que la etiqueta de estadísticas se haya estabilizado en la señal objetivo.
- **El waterfall tiene una estela de TX larga después de dejar de manipular**: En la versión v26.6.1, esto está corregido. Si aún ve estelas de artefacto, asegúrese de estar ejecutando la versión más reciente. Una reconexión de la radio reafirma el FPS correcto y la duración de la línea del waterfall.
- **La altura del panel o el tamaño de fuente se restablecen después de reiniciar**: Asegúrese de tener la versión v26.7.4 o posterior. En v26.7.4, estas preferencias se conservan automáticamente. Si aún se restablecen, verifique que los valores de `CwDecodeSettings` se estén escribiendo en su archivo de configuración.

## Relacionado

- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
