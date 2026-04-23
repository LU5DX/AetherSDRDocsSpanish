# Ajustar la sensibilidad del decodificador CW para rechazar el ruido

El control deslizante Sens controla con qué estrictez el decodificador CW filtra las decodificaciones de baja confianza. Aumentarlo reduce el ruido y los caracteres basura en la pantalla de decodificación; reducirlo permite que pasen más caracteres inciertos.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no lo está, actívelo primero — consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio cuando el audio no está presente.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del panadapter.
2. Encuentre la etiqueta "Sens:" y el pequeño control deslizante horizontal inmediatamente a su derecha.
3. Arrastre el control deslizante Sens hacia la derecha para aumentar la sensibilidad (filtrado más estricto, menos caracteres de ruido). Arrástrelo hacia la izquierda para reducir la sensibilidad (más permisivo, se muestran más caracteres).
4. Observe el área de texto decodificado CW. Ajuste hasta que el texto decodificado sea legible sin exceso de caracteres de ruido.

La configuración se guarda automáticamente. No se necesita ningún paso de confirmación.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Sens | 30 | 0–100 | `CwDecoderSensitivity` | Asigna el rango 0–100 a un umbral de costo interno de 1.0–0.1. Los valores más altos aplican un umbral más estricto, rechazando las decodificaciones de menor confianza. |

## Consejos

- Los caracteres decodificados se colorean según la confianza: verde (mayor confianza), amarillo, naranja y rojo (menor confianza). Con valores de Sens más bajos, verá más caracteres naranja y rojo; aumentar el Sens los suprime.
- Si una señal fuerte y limpia sigue produciendo caracteres de ruido, intente también estrechar el rango de búsqueda de tono usando los controles deslizantes Lo y Hi para que el decodificador no rastree interferencias fuera del tono de la señal.
- Una vez que encuentre un valor de Sens que funcione para su piso de ruido, este persiste entre sesiones mediante `CwDecoderSensitivity`.

## Solución de problemas

- **Aumentar Sens al máximo sigue mostrando caracteres de ruido** — El decodificador puede estar rastreando la señal incorrecta. Verifique que los controles deslizantes de tono Lo y Hi encuadren únicamente el tono de la señal CW y, a continuación, considere usar 🔒P (Lock Pitch) para fijar el decodificador en la frecuencia correcta. Consulte [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md).
- **Sens está en 0 pero casi nada se decodifica** — El umbral de costo en 0 es 1.0, lo que acepta todas las decodificaciones. Si la salida sigue siendo escasa, el problema probablemente es el enrutamiento del audio y no la sensibilidad. Verifique que el audio del PC esté llegando a AetherSDR.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
