# Eliminar un marcador que ya no necesita

Elimine un marcador de frecuencia de la pila de banda cuando ya no sea útil. Los marcadores eliminados se borran de la configuración persistente `BandStack_<serial>` de la radio conectada.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel de pila de banda solo es visible cuando hay una radio conectada.
- Localice el panel de pila de banda, la estrecha franja vertical de botones de frecuencia de colores que se encuentra junto al panadapter.

## Pasos

1. Busque el botón de marcador que desea eliminar en el panel de pila de banda.
2. Haga clic derecho en el botón de marcador.
3. Haga clic en **Remove** en el menú contextual que aparece.

El marcador desaparece inmediatamente del panel y se elimina de la configuración almacenada.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Botones de marcador | Un clic izquierdo recupera la frecuencia almacenada. Un clic derecho abre un menú contextual con la opción **Remove**. |
| **+** | Agrega un nuevo marcador en la frecuencia actual del slice activo. |
| **×** | Borra todos los marcadores de la radio conectada. |

La lista de marcadores se conserva en `BandStack_<serial>`, donde `<serial>` es el número de serie de la FLEX-8600 conectada.

## Consejos

- Si desea eliminar todos los marcadores a la vez, haga clic en **×** en la parte inferior del panel de pila de banda en lugar de eliminar las entradas una por una.
- Si "Group by band" está habilitado (a través del menú ⚙), los marcadores se ordenan por banda en lugar de por orden de inserción. El clic derecho sigue funcionando de la misma manera independientemente de la agrupación actual.
- Para evitar acumular marcadores que rara vez revisita, considere habilitar **Auto-expiry** en el menú ⚙. Las opciones son Off, 5 min, 15 min, 30 min y 60 min.

## Relacionados

- [Bookmark the current frequency](bookmark-the-current-frequency.md)
- [Recall a stored bookmark with one click](recall-a-stored-bookmark-with-one-click.md)
- [Visually scan the stored frequencies for the active band](visually-scan-the-stored-frequencies-for-the-active-band.md)
