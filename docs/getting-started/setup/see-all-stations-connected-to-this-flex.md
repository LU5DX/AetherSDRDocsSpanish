# Ver todas las estaciones conectadas a este FLEX

El panel multiFLEX muestra todos los clientes SmartSDR que están compartiendo actualmente su FLEX-8600. Úselo para verificar qué estaciones están en línea, qué antena y frecuencia utiliza cada una, quién tiene el PTT local y desconectar clientes individuales.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel multiFLEX no está disponible cuando no hay ninguna radio conectada.
- multiFLEX debe estar habilitado en la radio. Si aún no lo está, consulte [Habilitar multiFLEX en la radio](../../features/multi-flex/enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...`.
2. Se abre el diálogo **multiFLEX Dashboard**, que muestra la tabla de estaciones con todos los clientes actualmente conectados.
3. Revise la tabla. Cada fila corresponde a una estación conectada.
4. Haga clic en `Close` cuando termine.

## Descripción de cada control

| Control | Función |
|---|---|
| Botón `Enable` | Habilita o deshabilita multiFLEX en la radio. Haga clic para activar o desactivar multiFLEX. |
| Tabla de estaciones | Enumera cada cliente multiFLEX conectado. Columnas: **LOCAL PTT**, **STATION**, **TX ANT**, **TX FREQ (MHz)** y una columna de desconexión. Su propia estación se resalta en azul. Una marca de verificación (✔) en la columna **LOCAL PTT** identifica qué estación tiene actualmente la autoridad de PTT. |
| `Enable` (PTT) | Aparece cuando hay más de una estación conectada y su estación no tiene el PTT. Haga clic para reclamar la autoridad de PTT local para su estación. |
| Etiqueta Local PTT | Texto que indica qué estación tiene el PTT actualmente. |
| `Close` | Cierra el diálogo. |
| Botón de desconexión (en la tabla) | Un botón rojo en la quinta columna de cada fila de estación. Haga clic para desconectar esa estación cliente de la radio. El botón está deshabilitado para su propia estación. |

## Consejos

- La columna STATION muestra el nombre del programa y el nombre de la estación en el formato `programa: estación`. Si el nombre de la estación coincide con el nombre del programa, solo se muestra el nombre del programa. Si solo está disponible un nombre de estación, se muestra ese nombre únicamente. Si no se reportan datos de nombre, se muestra el identificador del cliente (ej., `client 0x00000000`).
- TX ANT y TX FREQ (MHz) muestran `----` si la radio aún no ha reportado esos datos para una estación determinada.
- La tabla se actualiza automáticamente a medida que las estaciones se conectan o desconectan. No es necesario volver a abrir el diálogo.
- Si solo hay una estación conectada, el botón `Enable` (PTT) y la etiqueta Local PTT están ocultos; no son necesarios cuando usted es el único cliente.
- El botón de desconexión aparece atenuado y deshabilitado para su propia estación. No puede desconectarse a sí mismo.
- El diálogo recuerda su posición y tamaño entre sesiones.

## Solución de problemas

- **`Settings > multiFLEX...` está atenuado o no aparece** — AetherSDR no está conectado a una radio. Conéctese a una radio primero y luego vuelva a abrir el menú.
- **La tabla de estaciones está vacía** — multiFLEX puede estar deshabilitado. Haga clic en `Enable` para habilitarlo y luego verifique si aparecen otras estaciones.
- **TX ANT y TX FREQ muestran `----` para todas las estaciones** — La radio aún no ha enviado el estado de las slices para esos clientes. Espere un momento y la tabla se actualizará automáticamente.

## Relacionados

- [Descripción general del panel multiFLEX](../../features/multi-flex/overview.md)
- [Habilitar multiFLEX en la radio](../../features/multi-flex/enable-multiflex-on-the-radio.md)
- [Conceder o revocar el PTT local](../../features/multi-flex/grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](../../features/multi-flex/check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Desconectar una estación cliente](../../features/multi-flex/disconnect-a-client-station.md)
