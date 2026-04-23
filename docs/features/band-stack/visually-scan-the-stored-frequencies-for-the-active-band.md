# Explorar visualmente las frecuencias almacenadas para la banda activa

El panel Band Stack muestra todos sus marcadores de frecuencia guardados como una tira vertical junto al panadapter. Esta página explica cómo leer el panel de un vistazo — entender la codificación por colores, el orden de disposición y las opciones de agrupación — para que pueda encontrar una frecuencia almacenada rápidamente sin desplazarse por una lista larga.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio Flex. El panel Band Stack solo es visible cuando hay una conexión de radio activa.
- Necesita tener al menos un marcador guardado. Si el panel está vacío, consulte [Marcar la frecuencia actual](bookmark-the-current-frequency.md).

## Pasos

1. Observe el panel Band Stack — la estrecha tira vertical situada inmediatamente junto al panadapter en la ventana principal.
2. Lea cada botón de marcador. La etiqueta del botón muestra la frecuencia en MHz con tres decimales (por ejemplo, `14.225`). Pase el cursor sobre cualquier botón para ver un tooltip con la frecuencia completa a seis decimales, el modo y la antena de recepción.
3. Observe el color del botón. El color de fondo de cada marcador refleja el segmento del plan de banda que contiene esa frecuencia, con el mismo esquema de colores utilizado en la superposición del plan de banda del panadapter.
4. Para cambiar el panel del orden de inserción al orden agrupado por banda, haga clic en el botón ⚙ en la parte inferior del panel. En el menú que aparece, haga clic en **Group by band**. El panel se reconstruye con encabezados de banda etiquetados que separan cada grupo. Los marcadores que no pertenecen a ninguna banda conocida aparecen bajo un encabezado **Other** al final.
5. Para volver al orden de inserción plano, haga clic en ⚙ nuevamente y haga clic en **Group by band** para desactivarlo.
6. Desplace la lista de marcadores hacia arriba o hacia abajo si hay más marcadores de los que caben en el área visible. La barra de desplazamiento horizontal está oculta; solo está disponible el desplazamiento vertical.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de marcador | Muestran la frecuencia almacenada en MHz (3 decimales). Haga clic para recuperarla; haga clic derecho para ver la opción **Remove**. | El color coincide con el segmento del plan de banda para esa frecuencia. |
| ⚙ (botón de engranaje) | Abre un menú con opciones de disposición y vencimiento. | Se encuentra en la fila inferior del panel. |
| **Group by band** (elemento de menú) | Alterna entre el orden de inserción plano y la disposición agrupada por banda con encabezados de nombre de banda. | Cuando está agrupado, hacer clic derecho en un encabezado de banda muestra la opción **Clear \<band\>**. |
| **Auto-expiry** (elementos de menú) | Establece cuánto tiempo se conservan los marcadores antes de su eliminación automática. Opciones: **Off**, **5 min**, **15 min**, **30 min**, **60 min**. Valor predeterminado: **Off**. | Se aplica a todos los marcadores del radio conectado. |
| × (botón borrar todo) | Elimina todos los marcadores a la vez. | Se encuentra en la fila inferior junto a + y ⚙. |
| + | Guarda la frecuencia actual del slice activo como un nuevo marcador. | Se encuentra en la fila inferior. |

Los marcadores se almacenan de forma persistente bajo la clave `BandStack_<serial>`, donde `<serial>` es el número de serie de su radio.

## Consejos

- Cuando **Group by band** está activado, los marcadores dentro de cada banda aparecen en el orden en que fueron guardados. Explorar una sola banda es más fácil porque sus marcadores son contiguos y están etiquetados con el nombre de la banda.
- Si opera en muchas bandas, activar **Group by band** evita tener que recordar a qué banda pertenece cada frecuencia — los encabezados lo hacen inmediatamente visible.
- El tooltip de cada marcador incluye el modo y la antena de recepción que estaban activos cuando se guardó el marcador, lo que le proporciona más contexto sin necesidad de recordar la frecuencia.

## Relacionado

- [Descripción general del Band Stack](overview.md)
- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
