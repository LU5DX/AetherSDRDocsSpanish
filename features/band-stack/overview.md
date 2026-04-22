# Descripción general del Band Stack

El Band Stack es una franja vertical de marcadores de frecuencia que se muestra junto a cada panadapter. Úselo para guardar frecuencias a las que regresa con frecuencia y recupérelas con un solo clic.

## Antes de comenzar

- Es necesario tener conectada una radio FLEX-8600. El panel Band Stack no es visible cuando no hay ninguna radio conectada.

## Cómo funciona

El panel Band Stack aparece como una franja estrecha a un lado de cada panadapter en la ventana principal. Siempre es visible cuando hay una radio conectada y no requiere ninguna configuración manual para mostrarse.

Cada botón de marcador muestra una frecuencia en MHz, redondeada a tres decimales. El color del botón refleja el segmento del plan de banda que contiene esa frecuencia — por ejemplo, las porciones de fonía, CW o datos de una banda se muestran cada una con el color definido por el plan de banda activo. Las frecuencias que quedan fuera de cualquier segmento definido en el plan de banda aparecen en un gris oscuro neutro.

Los marcadores se almacenan por radio, identificados por número de serie, mediante el ajuste `BandStack_<serial>`. El archivo se guarda automáticamente cada vez que se agrega o elimina un marcador. Si conecta una radio diferente, su propio conjunto de marcadores se carga de forma independiente.

El panel se desplaza verticalmente si tiene más marcadores de los que caben en el área visible. Cuando es necesario, aparece una barra de desplazamiento delgada en el borde derecho del panel.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter en la frecuencia almacenada. Haga clic derecho para abrir un menú contextual con la opción **Remove**. | El color del botón refleja el segmento del plan de banda para esa frecuencia. El tooltip muestra la frecuencia completa en MHz, el modo y la antena de RX. |
| **+** | Agrega un nuevo marcador en la frecuencia actual del slice activo. | Está ubicado en la parte inferior del panel. Almacena la frecuencia, el modo, los bordes del filtro, las antenas, los ajustes de AGC, la ganancia de audio y el estado de reducción de ruido. |

## Consejos

- Los marcadores de cada radio se almacenan por separado. Al conectar una segunda FLEX-8600 se carga la lista de marcadores propia de esa radio sin afectar la primera.
- Los tooltips de los botones de marcador muestran la frecuencia con seis decimales completos, el modo y la antena de RX. Pase el cursor sobre un botón para confirmar lo que recuperará antes de hacer clic.
- Si reorganiza las regiones de su plan de banda, los colores de los marcadores existentes se actualizan para coincidir con el nuevo plan en la siguiente carga.

## Relacionados

- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
