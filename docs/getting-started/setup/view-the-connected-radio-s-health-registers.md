# Ver los registros de salud de la radio conectada

Abra el diálogo de Salud de la Radio para ver en tiempo real los registros de salud y estado, de solo lectura, que reporta la radio conectada. Esto resulta útil para diagnosticar problemas como sobrecargas del ADC o para verificar que un FIFO se está moviendo.

## Antes de comenzar

- Una radio debe estar conectada a AetherSDR.

## Pasos

1. Seleccione **Help > Radio Health...**.
2. Lea los valores actuales en la tabla de registros de salud. La tabla se actualiza automáticamente cada 500 ms.
3. (Opcional) Haga clic en **Copy** para copiar la instantánea actual al portapapeles y pegarla en una solicitud de soporte o en un registro.

## Qué hace cada control

| Control | Comportamiento |
| --- | --- |
| Tabla de registros de salud | Muestra los registros de salud/estado de la radio según los reporta el backend. Los valores se agrupan por encabezados de sección. Un registro que la radio no ha reportado muestra un guion (—), no cero. Los valores booleanos se muestran como Sí o No. |
| Copy | Copia la instantánea de salud, incluidos los encabezados de sección, al portapapeles. La etiqueta de estado cambia brevemente a "Copied to clipboard". |
| Close | Cierra el diálogo. |

## Consejos

- Un guion significa que la radio no ha reportado ese valor; no es lo mismo que un valor de cero.
- Las filas de la tabla se reconstruyen solo cuando cambia el conjunto de registros, por lo que su posición de desplazamiento y la selección de filas se mantienen mientras lee.
- Nada en este diálogo escribe en la radio; es solo lectura de diagnóstico.
- Si la radio no reporta registros de salud, la etiqueta de estado muestra "This radio reports no health registers." en lugar de una tabla vacía.

## Solución de problemas

- **El estado muestra "Not connected."** — No hay ninguna radio conectada, o la conexión se perdió. Conéctese primero a una radio ([Connect to a local LAN radio](connect-to-a-local-lan-radio.md) o uno de los otros temas de conexión) y vuelva a abrir el diálogo.

## Relacionados

- [Radio Health overview](../../features/radio-health/overview.md)
- [Check how many external clients are connected to each channel](check-how-many-external-clients-are-connected-to-each-channel.md)
