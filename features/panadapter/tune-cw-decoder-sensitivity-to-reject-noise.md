# Ajustar la sensibilidad del decodificador CW para rechazar el ruido

El control deslizante Sens establece qué tan estrictamente el decodificador CW filtra los caracteres de baja confianza. Subirlo reduce los caracteres basura causados por el ruido; bajarlo recupera señales débiles a costa de más errores.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no está visible, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio de la PC debe estar enrutado hacia AetherSDR. El panel de decodificación CW muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Encuentre la etiqueta **Sens:** y su control deslizante inmediatamente a la derecha.
3. Arrastre el control deslizante **Sens** hacia la derecha para aumentar la sensibilidad (filtrado más estricto, menos caracteres de ruido) o hacia la izquierda para disminuirla (más permisivo, pasan más caracteres).
4. Observe el área de **texto decodificado CW**. Reduzca el valor si se están descartando caracteres genuinos; auméntelo si los caracteres de ruido saturan la salida.

El nuevo valor se guarda automáticamente en `CwDecoderSensitivity` y se restaura la próxima vez que AetherSDR se inicia.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Sens | 30 | 0–100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Valores más altos aplican un umbral de costo más estricto, rechazando más caracteres. Asigna 0–100 a un umbral de costo interno de 1.0–0.1. |

## Consejos

- El área de **texto decodificado CW** colorea cada carácter decodificado según su confianza: verde (máxima confianza), amarillo, naranja y rojo (mínima confianza). Si durante un período de silencio observa mayormente caracteres rojos o anaranjados, suba Sens para suprimirlos.
- Después de encontrar un valor que funcione para las condiciones actuales de la banda, considere fijar el tono y la velocidad para evitar que el decodificador vuelva a sincronizarse con el ruido. Consulte [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md).
- Los controles deslizantes **Lo** y **Hi** reducen el rango de búsqueda de tono (predeterminado 500–700 Hz), lo que también ayuda a rechazar el ruido fuera de frecuencia de forma independiente de Sens.

## Resolución de problemas

- **Subir Sens elimina toda la salida decodificada** — La señal puede ser demasiado débil o el tono puede estar fuera del rango Lo–Hi. Baje Sens gradualmente y verifique que la **etiqueta de estadísticas CW** muestre un tono detectado y una cifra de WPM. Si la etiqueta de estadísticas está en blanco, el decodificador no está sincronizando con ninguna señal.
- **Sens vuelve a 30 después de reiniciar** — La configuración no se guardó. Verifique que AetherSDR tenga permiso de escritura en su directorio de configuración.

## Relacionado

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
