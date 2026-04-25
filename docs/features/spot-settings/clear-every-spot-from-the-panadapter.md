# Borrar todos los spots del panadapter

Use esta página para eliminar al instante todos los spots de DX que se muestran actualmente en el panadapter. Esto resulta útil cuando la lista de spots se ha vuelto desordenada u obsoleta y desea una vista limpia sin modificar ningún otro ajuste de spots.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- El diálogo Spot Settings debe estar accesible desde el menú contextual del panadapter o desde la superposición (overlay) de Spots.

## Pasos

1. Haga clic derecho sobre el panadapter (o la superposición de Spots) para abrir el menú contextual.
2. Seleccione la opción que abre el diálogo **Spot Settings**.
3. Haga clic en **Clear All Spots**.

Todos los spots se eliminan inmediatamente del panadapter. No se modifica ningún ajuste: los spots seguirán apareciendo a medida que lleguen nuevos desde las fuentes configuradas.

## Consejos

- **Clear All Spots** elimina únicamente los spots que se muestran en ese momento. No afecta a `IsSpotsEnabled` ni a ningún otro ajuste persistente. Los nuevos spots provenientes de su clúster de DX u otras fuentes volverán a poblar el panadapter a medida que lleguen.
- El indicador **Total Spots:** en el diálogo Spot Settings muestra cuántos spots activos se están rastreando en ese momento. Tras hacer clic en **Clear All Spots**, este contador se reinicia.
- Para impedir que aparezcan nuevos spots por completo, utilice el interruptor **Spots:** en su lugar. Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Cambiar la densidad y posición vertical de los spots](change-spot-density-and-vertical-position.md)
