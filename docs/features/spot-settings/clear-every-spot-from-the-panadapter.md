# Eliminar todos los spots del panadapter

Esta página explica cómo quitar todos los spots DX que se muestran actualmente en el panadapter en una sola acción. Úsela cuando la capa de spots esté saturada y desee empezar desde cero sin modificar ninguna otra configuración de spots.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Al menos un panadapter debe estar abierto con spots visibles.

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual y, a continuación, seleccione la opción que abre la capa **Spot Settings**.
2. En el cuadro de diálogo **Spot Settings**, haga clic en **Clear All Spots**.

Todos los spots se eliminan inmediatamente del panadapter. Los spots nuevos seguirán llegando y mostrándose normalmente según su configuración actual.

## Consejos

- **Clear All Spots** no afecta a los spots entrantes provenientes de su cluster DX u otras fuentes. Los spots volverán a aparecer a medida que se reciban nuevos.
- El indicador **Total Spots:** en la parte inferior del cuadro de diálogo **Spot Settings** muestra la cantidad de spots activos que se están rastreando en ese momento. Tras limpiar, este contador reflejará únicamente los spots recibidos después de la acción de limpieza.
- Para evitar que los spots aparezcan por completo, use el interruptor **Spots:** y configúrelo en **Disabled**. Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Relacionado

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Acortar o alargar la duración de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
