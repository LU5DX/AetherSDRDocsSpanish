# Activar o desactivar los spots

Los spots de DX aparecen como superposiciones en el panadapter, mostrando indicativos y frecuencias de las fuentes de spots configuradas. Esta página explica cómo habilitar o deshabilitar la superposición de spots y la superposición de memorias relacionada, usando los controles maestros en Spot Settings.

## Antes de comenzar

- Abra un panadapter. Se accede al diálogo Spot Settings desde el menú contextual del panadapter.
- Los spots solo aparecerán si tiene al menos una fuente de spots configurada. Consulte `Settings > SpotHub...` para configurar un clúster de DX u otras fuentes.

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el diálogo **Spot Settings**.
3. Localice la fila **Spots:**. Haga clic en el botón de alternancia para cambiar entre **Enabled** y **Disabled**.
4. Para mostrar también los canales de memoria como superposiciones en el panadapter, localice la fila **Memories:** y haga clic en su botón de alternancia para cambiar entre **Enabled** y **Disabled**.
5. Cierre el diálogo. El cambio surte efecto de inmediato.

## Qué hace cada control

| Etiqueta | Tipo | Predeterminado | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Spots:** | Botón de alternancia | Enabled | `IsSpotsEnabled` | Control maestro para la superposición de spots de DX en el panadapter. |
| **Memories:** | Botón de alternancia | Disabled | `IsMemoriesShownOnPanadapter` | Activa o desactiva las superposiciones de canales de memoria en el panadapter. |

## Consejos

- El indicador **Total Spots:** en la parte inferior del diálogo muestra cuántos spots activos se están rastreando en ese momento, lo cual es útil para confirmar que las fuentes de spots están entregando datos incluso cuando la superposición está deshabilitada.
- Deshabilitar **Spots:** oculta la superposición sin desconectar las fuentes de spots ni vaciar la caché de spots.

## Relacionado

- [Descripción general de Spot Settings](overview.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
