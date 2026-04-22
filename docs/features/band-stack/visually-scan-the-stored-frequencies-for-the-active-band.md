# Explorar visualmente las frecuencias almacenadas para la banda activa

El panel Band Stack muestra todas las frecuencias marcadas como botones de colores dispuestos en una franja vertical junto al panadapter. Al observar el panel, puede ver de un vistazo qué frecuencias tiene almacenadas y en qué segmento del plan de banda se encuentra cada una, sin necesidad de sintonizar ninguna de ellas.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Debe existir al menos un marcador almacenado para la radio activa. Si el panel está vacío, consulte [Marcar la frecuencia actual](bookmark-the-current-frequency.md).

## Pasos

1. Observe la franja vertical estrecha (80 px de ancho) que se encuentra junto al panadapter en la ventana principal. Este es el panel Band Stack.
2. Lea las etiquetas de frecuencia en los botones de marcador. Cada botón muestra la frecuencia almacenada en MHz con tres decimales (por ejemplo, `14.225`).
3. Pase el cursor sobre cualquier botón de marcador para ver un tooltip con la frecuencia completa a seis decimales, el modo almacenado y la antena de recepción (RX).
4. Observe el color de fondo de cada botón. El color refleja el segmento del plan de banda que contiene esa frecuencia. Los botones de frecuencias que no pertenecen a ningún segmento definido en el plan de banda aparecen en gris oscuro.
5. Si hay más marcadores de los que caben en el área visible, desplace el panel verticalmente para ver los botones adicionales. El panel permite desplazamiento vertical; no hay desplazamiento horizontal disponible.

## Qué hace cada control

| Control | Comportamiento | Configuración persistente |
|---|---|---|
| Botones de marcador | Cada botón muestra una frecuencia almacenada. El color refleja el segmento del plan de banda para esa frecuencia. Haga clic para recuperarla; haga clic derecho para eliminarla. | `BandStack_<serial>` |
| + | Agrega un nuevo marcador en la frecuencia actual del slice activo. | `BandStack_<serial>` |

## Consejos

- El texto del tooltip incluye el modo y la antena RX almacenados con cada marcador, por lo que puede distinguir dos marcadores en la misma frecuencia guardados con diferentes modos o antenas sin necesidad de recuperar ninguno de ellos.
- Los datos de los marcadores se almacenan por número de serie de la radio. Si conecta una radio diferente, aparecerá su propia lista de marcadores independiente.

## Relacionado

- [Descripción general del Band Stack](overview.md)
- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
