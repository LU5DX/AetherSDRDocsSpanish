# Eliminar un marcador que ya no necesita

Elimine un marcador de frecuencia de la Pila de Banda cuando ya no sea útil. Los marcadores eliminados se borran de la configuración persistente `BandStack_<serial>` de la radio conectada.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel de Pila de Banda solo es visible cuando hay una radio conectada.
- Localice el panel de Pila de Banda, la estrecha franja vertical de botones de frecuencia de colores que se encuentra junto al panadapter.

## Pasos

1. Encuentre el botón de marcador que desea eliminar en el panel de Pila de Banda.
2. Haga clic derecho en el botón de marcador.
3. Haga clic en **Remove** en el menú contextual que aparece.

El marcador desaparece inmediatamente del panel y se elimina de la configuración almacenada.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Botones de marcador | Clic izquierdo recupera la frecuencia almacenada. Clic derecho abre un menú contextual con la opción **Remove**. El color refleja el segmento del plan de bandas para esa frecuencia. |
| **+** | Agrega un nuevo marcador en la frecuencia actual del slice activo. |

La lista de marcadores se guarda en `BandStack_<serial>`, donde `<serial>` es el número de serie de la FLEX-8600 conectada.

## Consejos

- Si desea eliminar todos los marcadores de una vez, haga clic en **×** en la parte inferior del panel de Pila de Banda en lugar de borrar las entradas una por una.
- Si "Group by band" está habilitado (a través del menú ⚙), los marcadores se ordenan por banda en lugar de por orden de inserción. El clic derecho sigue funcionando de la misma manera independientemente de la agrupación actual.
- Para evitar acumular marcadores que rara vez visita, considere habilitar **Auto-expiry** en el menú ⚙. Las opciones son Off, 5 min, 15 min, 30 min y 60 min.

## Relacionado

- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un clic](recall-a-stored-bookmark-with-one-click.md)
- [Examinar visualmente las frecuencias almacenadas de la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
