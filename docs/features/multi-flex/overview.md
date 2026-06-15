# Descripción general del panel multiFLEX

El panel multiFLEX muestra cada estación cliente que actualmente comparte su FLEX-8600 y le permite gestionar la autoridad de PTT entre esas estaciones. Úselo cuando opere en un entorno multioperador o con múltiples programas y necesite ver quién está transmitiendo, en qué antena y a qué frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel multiFLEX no está disponible sin una conexión activa a la radio.
- El firmware de su FLEX-8600 debe ser compatible con la función multiFLEX de SmartSDR.

## Cómo funciona

Abra el panel desde `Settings > multiFLEX...`. El cuadro de diálogo muestra el encabezado **multiFLEX Stations** y se actualiza automáticamente cada vez que un cliente se conecta o desconecta, o cuando cambia el estado de un slice en la radio. El cuadro de diálogo recuerda su tamaño y posición entre sesiones.

En la parte superior del cuadro de diálogo, el botón **Enable** refleja el estado actual de multiFLEX en la radio. Al hacer clic en él, se activa o desactiva multiFLEX y la etiqueta del botón se actualiza inmediatamente para reflejar el nuevo estado.

La **Stations table** enumera cada cliente multiFLEX conectado en cinco columnas:

| Columna | Contenido |
|---|---|
| LOCAL PTT | Una marca de verificación (✔) aparece en verde cuando esa estación posee actualmente la autoridad de PTT local. |
| STATION | Muestra el nombre del programa cliente y el nombre de la estación. Si ambos están presentes y son diferentes, muestra *programa: estación*. Si solo está presente la estación, muestra el nombre de la estación. Si ninguno está disponible, muestra el identificador del cliente como `cliente 0xHHHHHHHH`. Su propia estación está resaltada en azul. |
| TX ANT | La antena de transmisión asignada al slice TX de esa estación. Muestra `----` si no está disponible. |
| TX FREQ (MHz) | La frecuencia de transmisión del slice TX de esa estación en MHz con tres decimales. Muestra `----` si no está disponible. |
| (vacío) | Contiene un botón **Disconnect** para cada cliente remoto. Este botón está deshabilitado para su propia estación. |

Cada fila de estación tiene un botón **Disconnect** con fondo rojo. Haga clic en **Disconnect** para expulsar forzosamente a un cliente multiFLEX remoto de la radio. El botón se deshabilita mientras la solicitud de desconexión está pendiente, y el identificador del cliente se rastrea hasta que la radio confirme la expulsión. Una vez que el cliente se desconecta por completo, su entrada desaparece de la tabla. El botón **Disconnect** está deshabilitado para su propia entrada de cliente.

Debajo de la tabla, la etiqueta **Local PTT label** y el botón **Enable (PTT)** aparecen solo cuando hay más de un cliente conectado. Su contenido depende del estado actual de PTT:

- Si su estación no posee PTT, la etiqueta dice *Enable Local PTT for this station (nombre de la estación):* y se muestra el botón **Enable (PTT)**. Al hacer clic en **Enable (PTT)** se solicita la autoridad de PTT local para su estación.
- Si su estación ya posee PTT y selecciona la fila de otra estación, la etiqueta le informa que la estación seleccionada debe reclamar PTT desde su propio cliente. El botón **Enable (PTT)** está oculto en este estado.
- Si solo hay un cliente conectado, tanto la etiqueta como el botón **Enable (PTT)** están ocultos.

Al hacer clic en **Close** se cierra el cuadro de diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable** | Botón | Activa o desactiva multiFLEX en la radio. Muestra **Enabled** (verde) cuando multiFLEX está activo, **Disabled** (rojo) cuando está inactivo. |
| **Stations table** | Lista | Muestra todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz) y una columna de acción Disconnect. Al seleccionar una fila se actualiza la sección de PTT debajo. |
| **Disconnect** | Botón | Aparece en la última columna de cada fila de cliente remoto. Desconecta forzosamente a ese cliente de la radio. Deshabilitado para su propia estación. Deshabilitado mientras la solicitud de desconexión está pendiente. |
| **Enable (PTT)** | Botón | Solicita la autoridad de PTT local para su estación. Visible solo cuando su estación no posee actualmente PTT y hay más de un cliente conectado. |
| Local PTT label | Indicador | Muestra texto dependiente del contexto sobre el estado de PTT para la estación seleccionada. Oculto cuando solo hay un cliente conectado. |
| **Close** | Botón | Cierra el cuadro de diálogo del panel multiFLEX. |

## Consejos

- El cuadro de diálogo recuerda su tamaño y posición entre sesiones.
- La fila de su propia estación en la tabla de estaciones está resaltada en azul, lo que facilita identificar su entrada entre múltiples clientes.
- Los datos de antena TX y frecuencia para su propia estación se toman directamente de su slice TX activo, por lo que reflejan el estado actual incluso si la información del cliente desde la radio aún no se ha actualizado.
- La tabla se actualiza automáticamente; no necesita cerrar y volver a abrir el cuadro de diálogo para ver nuevos clientes.
- Para desconectar un cliente remoto, haga clic en el botón **Disconnect** en su fila. El botón se deshabilita mientras la solicitud está pendiente; una vez que la radio confirma la expulsión, la fila del cliente se elimina de la tabla.

## Relacionados

- [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md)
- [Grant or revoke local PTT](grant-or-revoke-local-ptt.md)
- [Check which antenna and frequency each TX station is using](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [See all stations connected to this FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
- Disconnect a remote multiFLEX client
