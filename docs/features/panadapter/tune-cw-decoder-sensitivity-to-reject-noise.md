# Ajustar la sensibilidad del decodificador CW para rechazar ruido

El control deslizante Sens determina con qué rigor el decodificador CW filtra las decodificaciones de baja confianza. Aumentarlo reduce el ruido y la salida confusa, a costa de perder ocasionalmente caracteres débiles pero válidos.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y visible debajo del panadapter. Si no está visible, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio de la PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del panadapter.
2. Encuentre la etiqueta "Sens:" y el control deslizante horizontal corto inmediatamente a su derecha.
3. Arrastre el control hacia la derecha para aumentar la sensibilidad (filtrado más estricto, menos decodificaciones de ruido) o hacia la izquierda para reducirla (más permisivo, muestra caracteres de menor confianza).
4. Observe el texto decodificado en el área de texto del decodificador CW para confirmar que el nivel de ruido cambia según lo esperado.

El nuevo valor se guarda inmediatamente en `CwDecoderSensitivity` y persiste entre reinicios.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Sens | 30 | 0–100 | `CwDecoderSensitivity` | Se asigna a un umbral de costo interno: 0 = umbral 1.0 (mostrar todo); 100 = umbral 0.1 (solo alta confianza). Los valores más altos rechazan más ruido. |

## Consejos

- Los caracteres decodificados se colorean según la confianza. El verde indica un costo inferior a 0.15; el amarillo, inferior a 0.35; el naranja, inferior a 0.60; el rojo, en 0.60 o superior. Si ve principalmente rojo o naranja, aumente Sens hasta que la salida sea predominantemente verde o amarilla.
- Con una señal limpia y una nota CW fuerte, un valor de Sens de 30–50 suele ser suficiente. En una banda ruidosa o con una señal débil, experimente primero con valores más bajos para evitar perder caracteres antes de aumentar Sens para suprimir el ruido.
- Si el decodificador sigue con seguimiento deficiente después de ajustar Sens, considere reducir la ventana de búsqueda de tono con Lo y Hi, o bloquee el tono una vez que el decodificador lo haya encontrado. Consulte [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento sea correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md).

## Solución de problemas

- **Aumentar Sens elimina toda la salida, incluida la que parece ser una señal correcta** — El costo interno del decodificador para esa señal supera el umbral. Reduzca Sens ligeramente hasta que reaparezcan los caracteres válidos y luego auméntelo de nuevo en pequeños pasos.
- **La salida no cambia después de mover el control deslizante** — Confirme que el panel de decodificación CW está activo y que se está recibiendo audio de la PC. El indicador "(requires PC Audio)" en el encabezado del panel indica que el audio aún no está llegando al decodificador.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento sea correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
