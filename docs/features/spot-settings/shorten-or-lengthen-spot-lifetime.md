# Acortar o alargar la duración de los spots

Ajuste cuánto tiempo permanecen visibles los spots de DX en el panadapter antes de desvanecerse. Una duración más corta mantiene la pantalla ordenada; una duración más larga permite ver spots que llegaron hace minutos u horas.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un equipo de radio para cambiar esta configuración.
- El diálogo **Spot Settings** debe ser accesible desde el menú contextual del panadapter o desde la capa de spots (Spots overlay).

## Pasos

1. Haga clic derecho en el panadapter (o haga clic en el Spots overlay) para abrir el diálogo **Spot Settings**.
2. Localice la fila **Spot Lifetime:**.
3. Arrastre el control deslizante hacia la izquierda para reducir la duración o hacia la derecha para aumentarla. La etiqueta a la derecha del control se actualiza de forma inmediata y muestra el valor actual en segundos, minutos, horas o días.
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente en `SpotsLifetime` (`DxClusterSpotLifetimeSec`).

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Control deslizante **Spot Lifetime:** | Define cuánto tiempo permanece un spot en el panadapter antes de desvanecerse. La escala es no lineal: avanza en pasos de 10–55 sec (en pasos de 5 sec), luego de 5–55 min (en pasos de 5 min), luego de 1–24 hr (en pasos de 1 hr), y finaliza en 1 day. | 30 min | 10 sec – 24 hr (1 day) | `SpotsLifetime` / `DxClusterSpotLifetimeSec` |

## Consejos

- La etiqueta del control deslizante usa unidades legibles: los valores inferiores a 60 segundos se muestran como `sec`, los valores inferiores a una hora se muestran como `min` o `mins`, y los valores de una hora o más se muestran como `hr` o `hrs`. Las 24 horas se muestran como `1 day`.
- Si actualizó desde una versión anterior de AetherSDR, la configuración se migra automáticamente desde la clave antigua basada en minutos a la clave actual basada en segundos. No se requiere ninguna acción manual.

## Relacionado

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
