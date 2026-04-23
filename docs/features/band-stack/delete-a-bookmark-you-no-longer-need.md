# Eliminar un marcador que ya no necesita

Elimine un marcador de frecuencia almacenado en el panel Band Stack cuando ya no le resulte útil. Los marcadores eliminados se borran de la configuración persistente `BandStack_<serial>` del radio conectado.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El panel Band Stack solo es visible cuando hay un radio conectado.
- Confirme que puede ver el panel Band Stack: la franja vertical estrecha de botones de frecuencia ubicada junto al panadapter (adaptador panorámico).

## Pasos

1. Localice el botón de marcador que desea eliminar en el panel Band Stack.
2. Haga clic derecho sobre el botón del marcador.
3. Haga clic en **Remove** en el menú contextual que aparece.

El botón desaparece de inmediato y el cambio se guarda en `BandStack_<serial>`.

## Consejos

- Para eliminar todos los marcadores a la vez, haga clic en el botón **×** ubicado en la parte inferior del panel Band Stack. Su tooltip indica "Clear all bookmarks".
- Si la opción "Group by band" está activada, los marcadores se agrupan bajo encabezados de banda. Puede hacer clic derecho sobre un encabezado de banda para borrar todos los marcadores de esa banda sin afectar las demás.

## Temas relacionados

- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Descripción general del Band Stack](overview.md)
