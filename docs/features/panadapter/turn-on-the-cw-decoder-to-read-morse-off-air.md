# Activar el decodificador de CW para leer Morse en el aire

El panel de decodificación de CW aparece debajo del panadapter y muestra el código Morse entrante como texto legible en tiempo real. Úselo para copiar CW en el aire sin necesidad de un programa de decodificación aparte. En la v26.5.2.1, el decodificador también muestra su propia señal de transmisión en color cian distintivo, de modo que puede separar visualmente su envío del CW entrante cuando ambas direcciones alimentan el mismo panel (#2417).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El audio de la PC debe estar enrutado a AetherSDR. El panel muestra el recordatorio "(requires PC Audio)" — la decodificación no funcionará sin esto.
- Sintonice una señal CW y configure el modo a CW en el slice activo.

## Pasos

1. En la barra de título del panadapter, confirme que el slice correcto se muestre en la etiqueta de título "Slice" (por ejemplo, "Slice A").
2. Abra el panel de decodificación de CW. El panel aparece debajo del área de espectro/waterfall y está oculto de forma predeterminada — busque un control o botón de modo CW que lo muestre para el slice activo. Una vez visible, el panel muestra la etiqueta **CW** en azul junto con la pista **(requires PC Audio)**.
3. Observe el área de **texto de decodificación CW** en la parte inferior del panel. A medida que el decodificador rastrea la señal, los caracteres decodificados van apareciendo y se colorean según la confianza: verde (alta), amarillo, naranja o rojo (baja). Los caracteres decodificados de su propia transmisión aparecen en cian (#5fc8ff) y se separan del texto entrante con un espacio.
4. Revise la **etiqueta de estadísticas CW** sobre el área de texto. Muestra el tono y la velocidad detectados en el formato `<Hz>  <WPM>`, por ejemplo `600 Hz  20 WPM`. Confirme que coinciden con la señal que está escuchando antes de depender de la decodificación.

## Qué hace cada control

| Control                    | Qué hace                                                                                                                                                                | Predeterminado |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| Control deslizante **Sens**            | Filtra caracteres de baja confianza. Los valores más altos rechazan más decodificaciones inciertas.                                                                                             | 30      |
| Conmutador **🔒P (Lock Pitch)** | Bloquea el decodificador al tono detectado actual para que deje de buscar.                                                                                                      | Desactivado     |
| Conmutador **🔒S (Lock Speed)** | Bloquea el decodificador a la velocidad detectada actual (WPM).                                                                                                                      | Desactivado     |
| Control deslizante de rango **Pitch**     | Establece el tono mínimo y máximo que busca el decodificador. Un solo control deslizante de doble manija reemplaza los controles Lo/Hi separados anteriores. Rango: 300–1200 Hz.                     | 500–700 Hz |
| Control deslizante de rango **WPM**       | Establece la velocidad mínima y máxima que busca el decodificador. Un solo control deslizante de doble manija. Rango: 5–60 WPM.                                                                   | 15–40 WPM |
| Botón **A-**              | Disminuye el tamaño de fuente del texto decodificado en 1 píxel (se conserva entre sesiones).                                                                                               | —       |
| Botón **A+**              | Aumenta el tamaño de fuente del texto decodificado en 1 píxel (se conserva entre sesiones).                                                                                               | —       |
| **CPY ALL**                | Copia todo el búfer de texto decodificado al portapapeles.                                                                                                                     | —       |
| **CPY VIS**                | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.                                                                                                 | —       |
| **CLR**                    | Borra el búfer de decodificación CW.                                                                                                                                                | —       |
| **× (cerrar CW)**           | Oculta el panel de decodificación CW.                                                                                                                                                  | —       |
| **Manija de arrastre (borde superior)**   | Una franja horizontal delgada sobre los controles del panel. Arrástrela hacia arriba o hacia abajo con el cursor de redimensionado vertical para ajustar la altura del panel (60–600 px) y revelar más historial de texto decodificado. Se conserva entre sesiones. | 80 px (predeterminado) |
| **Etiqueta de estadísticas CW**         | Indicador que muestra el tono y la velocidad detectados. Solo lectura.                                                                                                                      | —       |
| **Texto de decodificación CW**         | Pantalla continua de solo lectura de caracteres decodificados, coloreados según la confianza. El clic derecho abre un menú contextual con una opción **Clear** además de las acciones de texto estándar. El tamaño de fuente se controla con los botones A- / A+. | 13 px (predeterminado) |

## Cómo aparece la decodificación de TX

Cuando transmite CW, el decodificador captura su señal de manipulación y la muestra en texto cian. Esto le permite verificar su propio envío junto a las señales entrantes. El decodificador aplica el mismo filtro de confianza que la ruta de RX: los caracteres de baja confianza se suprimen. Se inserta un espacio al cambiar entre la decodificación de TX y RX para evitar que las secuencias de color se fusionen visualmente.

## Congelación del waterfall durante la transmisión

En la v26.6.1, el waterfall ahora se congela cuando cualquier cliente (no solo esta radio) comienza a transmitir. La congelación está impulsada por el estado de interbloqueo TRANSMITTING de la radio en lugar del flanco local de MOX, eliminando el artefacto de estela de TX de 10–23 segundos que aparecía anteriormente al dejar de manipular.

Cuando la radio se reconecta, los FPS deseados del panadapter y la duración de línea del waterfall se reafirman (mediante reconciliación interna) para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio.

## Rango dBm del panadapter secundario al reconectar

En la v26.8.4, los panadapters secundarios (Slices B–H) tienen su rango dBm preparado al reconectar para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano al reconectar.

## Gestos de movimiento en vivo en el lienzo

En la v26.8.4, cuando un panadapter está alojado como elemento en el lienzo del espacio de trabajo, la franja de título transmite un gesto de movimiento en vivo (el mismo mecanismo utilizado por otros elementos del lienzo). Un umbral de 6 px separa un clic (que activa el panadapter) de un arrastre; todo lo que supere ese umbral lo consume el arrastre del lienzo, de modo que el mecanismo de arrastre flotante de la franja nunca lo ve.

El botón de ventana emergente permanece disponible para los elementos del lienzo incluso en modo de pan simple, ya que la ventana emergente es una capacidad general en lugar de una opción de disposición de modo de pila.

Cuando un panadapter regresa a la pila desde el lienzo, la pila vuelve a aplicar sus reglas normales de visibilidad de botones de pan simple/múltiple.

## Preferencias del panel conservadas

En la v26.7.4, la altura del panel de decodificación CW y el tamaño de fuente ahora se guardan y restauran entre sesiones, eliminando la necesidad de reajustarlos cada vez que abre el panel. Los ajustes se almacenan en `CwDecodeSettings::panelHeight` y `CwDecodeSettings::fontPx`.

- Altura del panel: 60–600 px. Arrastre la manija de redimensionado (franja horizontal delgada en la parte superior del panel) para ajustarla.
- Tamaño de fuente: 8–32 px. Use los botones **A-** y **A+** para cambiar.

## Consejos

- Si el área de texto se llena con caracteres de baja confianza (naranja o rojo), aumente **Sens** para filtrarlos. Comience alrededor de 50 y aumente hasta que los caracteres de ruido desaparezcan.
- Reduzca el rango de búsqueda de tono con el control deslizante **Pitch** para que coincida con el tono lateral de la estación que está copiando. Esto reduce las activaciones falsas de señales cercanas.
- Reduzca el rango de velocidad con el control deslizante **WPM** para que coincida con la velocidad de envío de la estación que está copiando. Esto mejora la precisión de decodificación.
- Una vez que la **etiqueta de estadísticas CW** se estabilice en un tono y velocidad constantes, active **🔒P (Lock Pitch)** y **🔒S (Lock Speed)** para evitar que el decodificador se desvíe hacia otra señal.
- Use **CLR** antes de un nuevo QSO para mantener legible el área de texto. También puede hacer clic derecho en el área de **texto de decodificación CW** y elegir **Clear** en el menú contextual.
- Ajuste los botones **A- / A+** a un tamaño de fuente cómodo para la resolución de su monitor y la distancia de visualización. El ajuste se conserva automáticamente.
- Arrastre la **manija de redimensionado** en la parte superior del panel para mostrar más o menos historial decodificado. La nueva altura se guarda al cerrar el panel o reiniciar AetherSDR.

## Solución de problemas

- **No aparece texto en el área de decodificación** — Verifique que el audio de la PC esté enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio. Sin esto, el decodificador no recibe audio y no produce salida.
- **El texto decodificado es mayormente rojo o naranja** — La confianza de la señal es baja. Aumente **Sens**, o reduzca el rango **Pitch** para que coincida con la frecuencia de tono lateral real que se muestra en la **etiqueta de estadísticas CW**. También reduzca el rango **WPM** para que coincida con la velocidad de envío.
- **Tono o velocidad incorrectos en la etiqueta de estadísticas CW** — No active **🔒P (Lock Pitch)** ni **🔒S (Lock Speed)** hasta que la etiqueta de estadísticas se haya estabilizado en la señal deseada.
- **El waterfall tiene una estela TX larga después de dejar de manipular** — En la v26.6.1, esto está corregido. Si aún ve estelas de artefactos, asegúrese de estar ejecutando la versión más reciente. Una reconexión de la radio reafirma los FPS correctos y la duración de línea del waterfall.
- **Espectro plano en el panadapter secundario después de reconectar** — En la v26.8.4, los panadapters secundarios (Slices B–H) tienen su rango dBm preparado al reconectar. Asegúrese de estar ejecutando la versión más reciente.
- **La altura del panel o el tamaño de fuente se reinician después de reiniciar** — Asegúrese de tener la v26.7.4 o posterior. En la v26.7.4, estas preferencias se conservan automáticamente. Si aún se reinician, verifique que los valores de `CwDecodeSettings` se estén escribiendo en su archivo de configuración.

## Relacionado

- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
