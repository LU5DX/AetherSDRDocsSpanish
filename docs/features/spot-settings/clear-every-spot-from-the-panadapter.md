# Borrar todos los spots del panadapter

Esta página explica cómo eliminar todos los spots de DX que se muestran actualmente en el panadapter en una sola acción. Utilice este procedimiento cuando la visualización de spots se haya vuelto confusa o desee empezar desde cero sin esperar a que los spots expiren.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- El panadapter debe estar visible.
- Los spots deben haberse recibido desde una fuente configurada; si no hay spots cargados, el botón no tiene efecto.

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual y seleccione la opción que abre el diálogo Spot Settings.
2. En el diálogo **Spot Settings**, haga clic en **Clear All Spots**.

Todos los spots se eliminan inmediatamente del panadapter. El indicador **Total Spots:** se restablece a cero. Los nuevos spots volverán a aparecer a medida que lleguen desde sus fuentes de spots configuradas.

## Consejos

- Borrar los spots no deshabilita la visualización de spots. El ajuste `IsSpotsEnabled` no cambia; los nuevos spots entrantes seguirán apareciendo después del borrado.
- Si desea impedir que aparezcan spots por completo, en lugar de solo borrar el conjunto actual, use el botón **Spots:** para cambiarlo a Disabled. Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).
- El indicador **Total Spots:** en la parte inferior del diálogo Spot Settings muestra cuántos spots se están rastreando actualmente. Verifíquelo antes y después de hacer clic en **Clear All Spots** para confirmar que el borrado se realizó correctamente.

## Solución de problemas

- **Los spots reaparecen inmediatamente después de borrarlos** — Su fuente de spots está enviando nuevos spots de forma activa. Este es el comportamiento normal. Para pausar la recepción de spots, deshabilite la fuente de spots en `Settings > SpotHub...` o cambie **Spots:** a Disabled.

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Descripción general de Spot Settings](overview.md)
