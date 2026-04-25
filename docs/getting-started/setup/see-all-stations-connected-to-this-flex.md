# Ver todas las estaciones conectadas a este FLEX

El panel multiFLEX Dashboard muestra todos los clientes que comparten el radio en ese momento, indicando el nombre de cada estación, la antena de transmisión y la frecuencia de transmisión. Úselo para verificar quién más está en el radio antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. La opción de menú no está disponible sin una conexión de radio activa.
- multiFLEX debe estar habilitado en el radio. Si no lo está, la tabla Stations aparecerá vacía o mostrará únicamente su propia estación.

## Pasos

1. Haga clic en `Settings > multiFLEX...`.
2. Se abre el **multiFLEX Dashboard**. La **tabla Stations** lista cada cliente conectado en cuatro columnas: **LOCAL PTT**, **STATION**, **TX ANT** y **TX FREQ (MHz)**.
3. Revise la tabla. Su propia estación aparece resaltada en azul. Una marca de verificación en la columna **LOCAL PTT** indica qué estación tiene actualmente la autoridad de PTT.
4. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Qué hace |
|---|---|
| Botón **Enabled** / **Disabled** | Activa o desactiva multiFLEX en el radio. Muestra **Enabled** (verde) o **Disabled** (rojo) para reflejar el estado actual. |
| **Tabla Stations** | Lista cada cliente multiFLEX conectado. Columnas: **LOCAL PTT** (marca si esta estación tiene PTT), **STATION** (programa y nombre de estación), **TX ANT** (antena de transmisión), **TX FREQ (MHz)** (frecuencia de transmisión en MHz). |
| **Enable** (PTT) | Reclama la autoridad de PTT local para su estación. Solo es visible cuando otra estación tiene el PTT y usted no. |
| **Close** | Cierra el cuadro de diálogo. |

## Consejos

- La fila de su propia estación se muestra en azul. Las demás estaciones se muestran con el color predeterminado.
- Si solo hay una estación conectada, la etiqueta de PTT y el botón **Enable** están ocultos: el PTT no está en disputa.
- La antena TX y la frecuencia muestran `----` si el radio aún no ha reportado datos de slice para esa estación.

## Solución de problemas

- **La tabla Stations muestra solo una fila o está vacía** — Es posible que multiFLEX no esté habilitado en el radio. Haga clic en el botón **Disabled** para habilitarlo y verifique si aparecen otros clientes.
- **TX ANT y TX FREQ muestran `----` para una estación** — Los datos de estado de slice de ese cliente aún no han llegado desde el radio. Espere un momento; la tabla se actualizará automáticamente cuando se reciban los datos.

## Temas relacionados

- [Descripción general del multiFLEX Dashboard](../../features/multi-flex/overview.md)
- [Habilitar multiFLEX en el radio](../../features/multi-flex/enable-multiflex-on-the-radio.md)
- [Otorgar o revocar el PTT local](../../features/multi-flex/grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](../../features/multi-flex/check-which-antenna-and-frequency-each-tx-station-is-using.md)
