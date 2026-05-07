# Conceder o revocar el PTT local

Use el panel multiFLEX para reclamar la autoridad de PTT local para su estación o para ver qué estación la posee actualmente. Esto es necesario cuando varios clientes comparten el mismo FLEX-8600 y solo una estación puede transmitir a la vez.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel multiFLEX requiere una conexión activa con la radio.
- multiFLEX debe estar habilitado en la radio. Si el panel muestra "Disabled", primero consulte [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md).
- Deben estar conectadas al menos dos estaciones para que aparezcan los controles de PTT. Con una sola estación, el botón de PTT está oculto.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el panel multiFLEX.
2. Revise la tabla Stations. La columna LOCAL PTT muestra una marca de verificación junto a la estación que actualmente posee el PTT.
3. Si su estación no posee el PTT, la etiqueta debajo de la tabla muestra `Enable Local PTT for this station (<nombre de su estación>):` y el botón Enable está visible.
4. Haga clic en `Enable` para reclamar el PTT local para su estación.

Si otra estación ya posee el PTT, el botón Enable estará oculto. En su lugar, la etiqueta identifica a la otra estación e indica que debe reclamar o liberar el PTT desde su propio cliente. No puede forzar la salida del PTT de otra estación a través de este cuadro de diálogo.

5. Haga clic en `Close` cuando termine.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Enable (superior) | Habilita o deshabilita multiFLEX en la radio. Muestra "Enabled" (verde) o "Disabled" (rojo) para reflejar el estado actual. |
| Tabla Stations | Enumera todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Su propia estación aparece resaltada. Una marca de verificación en LOCAL PTT indica qué estación posee el PTT. |
| Etiqueta Local PTT | Describe el estado actual del PTT en relación con su estación, o nombra la otra estación que debe actuar. Se oculta cuando solo hay una estación conectada. |
| Enable (PTT) | Reclama la autoridad de PTT local para su estación. Visible solo cuando su estación no posee actualmente el PTT y hay al menos dos estaciones conectadas. |
| Close | Cierra el cuadro de diálogo. |

## Consejos

- Su estación aparece resaltada en la columna STATION, lo que facilita encontrarla en una tabla con muchas entradas.
- La columna STATION muestra las entradas como `programa: estación` cuando el nombre del programa y el nombre de la estación difieren.
- TX ANT y TX FREQ (MHz) reflejan el slice de transmisión de cada estación. Si esos datos aún no están disponibles, las columnas muestran `----`.

## Solución de problemas

- **El botón Enable (PTT) no está visible** — Su estación ya posee el PTT, solo hay una estación conectada (el modo de estación única concede el PTT automáticamente), u otra estación posee el PTT y debe liberarlo desde su propio cliente.
- **Los controles de PTT faltan por completo** — Solo hay una estación conectada actualmente. Los controles aparecen solo cuando hay dos o más estaciones en la tabla Stations.
- **La tabla Stations está vacía** — La conexión con la radio puede haberse perdido, o multiFLEX no está habilitado. Verifique que el botón Enable en la parte superior del cuadro de diálogo muestre "Enabled".

## Relacionados

- [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md)
- [Check which antenna and frequency each TX station is using](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [See all stations connected to this FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
