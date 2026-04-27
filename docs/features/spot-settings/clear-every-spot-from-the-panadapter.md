# Borrar todos los spots del panadapter

Esta página explica cómo eliminar todos los spots de DX que se muestran actualmente en el panadapter en una sola acción. Úsela cuando la superposición de spots esté saturada y desee empezar desde cero sin modificar ninguna otra configuración de spots.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Debe haber al menos un panadapter abierto con spots visibles.

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual y, a continuación, seleccione la opción que abre la superposición de Spot Settings.
2. En el diálogo **Spot Settings**, haga clic en **Clear All Spots**.

Todos los spots se eliminan inmediatamente del panadapter. Los nuevos spots seguirán llegando y mostrándose con normalidad según su configuración actual.

## Consejos

- **Clear All Spots** no afecta a los spots entrantes provenientes de su clúster de DX u otras fuentes. Los spots volverán a aparecer a medida que se reciban nuevos.
- El indicador **Total Spots:** en la parte inferior del diálogo Spot Settings muestra la cantidad de spots activos que se están rastreando en ese momento. Después de borrarlos, este contador reflejará únicamente los spots recibidos después de la acción de borrado.
- Para impedir que los spots aparezcan por completo, use el interruptor **Spots:** y configúrelo en **Disabled**. Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
