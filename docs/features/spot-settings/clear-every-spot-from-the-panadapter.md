# Eliminar todos los puntos del panadapter

Esta página explica cómo eliminar todos los puntos de DX mostrados actualmente en el panadapter con una sola acción. Utilice esto cuando la superposición de puntos esté saturada y desee tener una pizarra limpia sin cambiar ninguna otra configuración de puntos.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Al menos un panadapter debe estar abierto con puntos visibles.

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual, luego seleccione la opción que abre la superposición Spot Settings.
2. En el cuadro de diálogo **Spot Settings**, haga clic en **Clear All Spots**.

Todos los puntos se eliminan inmediatamente del panadapter. Los nuevos puntos continuarán llegando y mostrándose normalmente según su configuración actual.

## Consejos

- **Clear All Spots** no afecta los puntos entrantes desde su clúster DX u otras fuentes. Los puntos reaparecerán a medida que se reciban nuevos.
- El indicador **Total Spots:** en la parte inferior del cuadro de diálogo Spot Settings muestra el recuento de puntos activos que se están rastreando actualmente. Después de eliminar, este recuento reflejará solo los puntos recibidos después de la acción de eliminación.
- Para evitar que los puntos aparezcan por completo, use la alternancia **Spots:** para configurarla en **Disabled**. Consulte [Activar o desactivar puntos](turn-spots-on-or-off.md).
- La alternancia **Spot Lines:** controla si se dibujan líneas verticales desde la línea base del espectro hasta cada etiqueta de punto. Esta configuración es independiente de **Clear All Spots**. Si el panadapter se siente visualmente recargado durante un concurso, configure **Spot Lines:** en **Disabled** antes o después de eliminar puntos para reducir la saturación sin quitar las etiquetas de los puntos.

## Relacionado

- [Activar o desactivar puntos](turn-spots-on-or-off.md)
- [Acortar o alargar la vida útil de los puntos](shorten-or-lengthen-spot-lifetime.md)
- [Cambiar la densidad y la posición vertical de los puntos](change-spot-density-and-vertical-position.md)
