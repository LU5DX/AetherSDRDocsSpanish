# Ver todas las estaciones conectadas a este FLEX

El multiFLEX Dashboard muestra todos los clientes de SmartSDR que comparten su FLEX-8600 en este momento, junto con sus detalles de transmisión. Ábralo para confirmar qué estaciones están usando el radio y cuál tiene el PTT local.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El multiFLEX Dashboard requiere una conexión activa con el radio.
- multiFLEX debe estar habilitado en el radio. Si no lo está, la tabla Stations estará vacía o mostrará únicamente su propia estación.

## Pasos

1. Haga clic en `Settings > multiFLEX...`.
2. Se abre el **multiFLEX Dashboard**. La tabla Stations lista todos los clientes conectados con cuatro columnas: **LOCAL PTT**, **STATION**, **TX ANT** y **TX FREQ (MHz)**.
3. Revise las filas. Su propia estación aparece resaltada en azul en la columna **STATION**. Una marca de verificación en la columna **LOCAL PTT** indica qué estación tiene actualmente la autoridad de PTT.
4. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Función |
|---|---|
| Botón **Enabled** / **Disabled** | Indica si multiFLEX está activo en el radio. Haga clic para activarlo o desactivarlo. |
| Tabla Stations | Lista cada cliente multiFLEX conectado. Columnas: **LOCAL PTT**, **STATION**, **TX ANT**, **TX FREQ (MHz)**. |
| **Enable** (PTT) | Toma la autoridad de PTT local para su estación. Solo es visible cuando otra estación tiene el PTT o cuando hay más de una estación conectada y usted no tiene el PTT en ese momento. |
| **Close** | Cierra el diálogo. |
| Etiqueta Local PTT | Muestra qué estación tiene el PTT, o le indica que habilite el PTT para su estación. |

## Consejos

- La columna **STATION** muestra el nombre del programa remoto y el nombre de la estación con el formato `program: station`. Su propia entrada aparece en azul.
- Si solo hay una estación conectada, el botón **Enable** (PTT) y la etiqueta Local PTT están ocultos: el PTT es implícitamente suyo.
- Si otra estación tiene el PTT y usted selecciona su fila, la etiqueta indica que esa otra estación debe tomar el PTT desde su propio cliente. No es posible otorgar el PTT a otra estación desde este diálogo.
- La antena TX y la frecuencia muestran `----` si el radio aún no ha reportado datos de slice para ese cliente.

## Solución de problemas

- **La tabla Stations está vacía o muestra solo su estación** — multiFLEX puede estar deshabilitado. Haga clic en el botón **Disabled** para habilitarlo y verifique si aparecen otros clientes.
- **La columna LOCAL PTT no muestra ninguna marca de verificación en ninguna fila** — Ninguna estación tiene el PTT en este momento. Haga clic en **Enable** para tomarlo para su estación.
- **TX ANT y TX FREQ muestran `----` para una estación** — El estado del slice aún no ha llegado para ese cliente. Espere un momento y vuelva a abrir el diálogo; la tabla se actualiza automáticamente cuando cambia la información del cliente.

## Temas relacionados

- [Descripción general del multiFLEX Dashboard](../../features/multi-flex/overview.md)
- [Habilitar multiFLEX en el radio](../../features/multi-flex/enable-multiflex-on-the-radio.md)
- [Otorgar o revocar el PTT local](../../features/multi-flex/grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](../../features/multi-flex/check-which-antenna-and-frequency-each-tx-station-is-using.md)
