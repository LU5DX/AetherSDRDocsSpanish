# Conceder o revocar el PTT local

Use el panel multiFLEX para solicitar la autoridad de PTT local para su estación o para ver qué estación la posee actualmente. Esto es necesario cuando varios clientes comparten el mismo FLEX-8600 y solo una estación puede transmitir a la vez.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel multiFLEX requiere una conexión activa con la radio.
- multiFLEX debe estar habilitado en la radio. Si el panel muestra "Disabled", consulte primero [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md).
- Deben estar conectadas al menos dos estaciones antes de que aparezcan los controles de PTT. Con solo una estación presente, el botón de PTT está oculto.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el panel multiFLEX.
2. Revise la tabla de estaciones. La columna LOCAL PTT muestra una marca de verificación junto a la estación que actualmente posee el PTT.
3. Si su estación no posee el PTT, la etiqueta debajo de la tabla muestra `Enable Local PTT for this station (<nombre de su estación>):` y el botón Enable está visible.
4. Haga clic en `Enable` para solicitar el PTT local para su estación.

Si otra estación ya posee el PTT, el botón Enable está oculto. La etiqueta, en cambio, identifica a la otra estación e indica que debe solicitar o liberar el PTT desde su propio cliente. No puede forzar el PTT de otra estación a través de este cuadro de diálogo.

5. Haga clic en `Close` al terminar.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Enable (superior) | Activa o desactiva multiFLEX en la radio. Muestra "Enabled" (verde) o "Disabled" (rojo) para reflejar el estado actual. |
| Tabla de estaciones | Enumera cada cliente multiFLEX conectado. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Su propia estación aparece resaltada. Una marca de verificación en LOCAL PTT indica qué estación posee el PTT. |
| Etiqueta de PTT local | Describe el estado actual del PTT en relación con su estación, o nombra la otra estación que debe actuar. Se oculta cuando solo hay una estación conectada. |
| Enable (PTT) | Solicita la autoridad de PTT local para su estación. Visible solo cuando su estación no posee actualmente el PTT y hay al menos dos estaciones conectadas. |
| Close | Cierra el cuadro de diálogo. |

## Consejos

- Su estación está resaltada en la columna STATION, lo que facilita encontrarla en una tabla con muchos elementos.
- La columna STATION muestra las entradas como `programa: estación` cuando el nombre del programa y el nombre de la estación son diferentes.
- TX ANT y TX FREQ (MHz) reflejan el slice de transmisión de cada estación. Si esos datos aún no están disponibles, las columnas muestran `----`.
- El cuadro de diálogo recuerda su tamaño y posición entre sesiones.

## Solución de problemas

- **El botón Enable (PTT) no está visible** — O su estación ya posee el PTT, solo hay una estación conectada (el modo de estación única concede el PTT automáticamente), u otra estación posee el PTT y debe liberarlo desde su propio cliente.
- **Los controles de PTT faltan por completo** — Solo hay una estación conectada actualmente. Los controles aparecen solo cuando hay dos o más estaciones presentes en la tabla de estaciones.
- **La tabla de estaciones está vacía** — La conexión con la radio puede haberse perdido, o multiFLEX no está habilitado. Verifique que el botón Enable en la parte superior del cuadro de diálogo muestre "Enabled".

## Relacionado

- [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md)
- [Check which antenna and frequency each TX station is using](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [See all stations connected to this FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
