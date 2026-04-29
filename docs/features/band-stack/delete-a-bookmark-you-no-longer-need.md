# Eliminar un marcador que ya no necesita

Elimine un marcador de frecuencia del Band Stack cuando ya no sea útil. Los marcadores eliminados se borran de la configuración persistente `BandStack_<serial>` del radio conectado.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El panel Band Stack solo es visible cuando hay un radio conectado.
- Localice el panel Band Stack, la estrecha franja vertical de botones de frecuencia de colores que se encuentra junto al panadapter.

## Pasos

1. Encuentre el botón de marcador que desea eliminar en el panel Band Stack.
2. Haga clic derecho sobre el botón del marcador.
3. Haga clic en **Remove** en el menú contextual que aparece.

El marcador desaparece inmediatamente del panel y se elimina de la configuración almacenada.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Botones de marcador | Clic izquierdo recupera la frecuencia almacenada. Clic derecho abre un menú contextual con la opción **Remove**. |
| **+** | Agrega un nuevo marcador en la frecuencia actual del slice activo. |
| **×** | Borra todos los marcadores del radio conectado. |

La lista de marcadores se conserva bajo `BandStack_<serial>`, donde `<serial>` es el número de serie del FLEX-8600 conectado.

## Consejos

- Si desea eliminar todos los marcadores a la vez, haga clic en **×** en la parte inferior del panel Band Stack en lugar de eliminar las entradas una por una.
- Si "Group by band" está habilitado (mediante el menú ⚙), los marcadores se ordenan por banda en lugar de por orden de inserción. El clic derecho sigue funcionando de la misma manera independientemente de la agrupación actual.
- Para evitar acumular marcadores que raramente consulta, considere habilitar **Auto-expiry** en el menú ⚙. Las opciones son Off, 5 min, 15 min, 30 min y 60 min.

## Relacionados

- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un clic](recall-a-stored-bookmark-with-one-click.md)
- [Explorar visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
