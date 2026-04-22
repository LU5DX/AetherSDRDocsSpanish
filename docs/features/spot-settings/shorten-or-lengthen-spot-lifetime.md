# Acortar o alargar la duración de los spots

Use esta página para controlar cuánto tiempo permanecen visibles los spots de DX en el panadapter antes de que expiren. Una duración más corta mantiene la pantalla despejada; una duración más larga es útil durante condiciones de banda lentas cuando los spots llegan con poca frecuencia.

## Antes de comenzar

- El diálogo Spot Settings no está en el menú principal. Debe abrirlo desde el menú contextual del panadapter o desde la superposición de spots.
- Los spots deben estar habilitados (`IsSpotsEnabled`) para que el ajuste de duración tenga algún efecto visible.

## Pasos

1. Haga clic derecho en el panadapter (o haga clic en la superposición de spots) para abrir el diálogo **Spot Settings**.
2. Localice el control deslizante **Spot Lifetime:**.
3. Arrastre el control hacia la izquierda para acortar la duración o hacia la derecha para alargarla. La etiqueta a la derecha del control se actualiza de inmediato y muestra el valor actual en segundos, minutos u horas (por ejemplo, `30 secs`, `5 mins`, `1 hr`).
4. Suelte el control. El nuevo valor se guarda automáticamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave persistida |
|---|---|---|---|
| Control deslizante **Spot Lifetime:** | Establece cuánto tiempo permanece un spot en el panadapter antes de desaparecer. La escala no es lineal: la parte izquierda avanza de 10 a 55 segundos en incrementos de 5 segundos, la parte central avanza de 5 a 55 minutos en incrementos de 5 minutos, y la parte derecha avanza de 1 a 24 horas en incrementos de 1 hora. | 30 minutos | `SpotsLifetime` |

## Consejos

- La etiqueta del control deslizante redondea al valor de paso más cercano, por lo que no es posible ingresar un número arbitrario de segundos — utilice el paso más cercano.
- Si configuró previamente la duración de los spots en una versión anterior de AetherSDR que almacenaba el valor en minutos, el diálogo migra ese valor a segundos automáticamente la primera vez que se abre.
- En el extremo derecho del rango del control, la etiqueta muestra `1 day` (24 horas), que es la duración máxima.

## Relacionado

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
