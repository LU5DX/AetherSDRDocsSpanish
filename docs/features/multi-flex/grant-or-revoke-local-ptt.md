# Otorgar o revocar PTT local

Use el multiFLEX Dashboard para reclamar la autoridad de PTT local para su estación o para ver qué estación la tiene actualmente. Esto es necesario cuando varios clientes comparten el mismo FLEX-8600 y solo una estación puede transmitir a la vez.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El multiFLEX Dashboard requiere una conexión activa con la radio.
- multiFLEX debe estar habilitado en la radio. Si el panel muestra "Disabled", consulte primero [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md).
- Deben estar conectadas al menos dos estaciones antes de que aparezcan los controles de PTT. Con una sola estación presente, el botón de PTT está oculto.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. Revise la tabla Stations. La columna LOCAL PTT muestra una marca de verificación junto a la estación que actualmente tiene el PTT.
3. Si su estación no tiene el PTT, la etiqueta debajo de la tabla muestra `Enable Local PTT for this station (<your station name>):` y el botón Enable es visible.
4. Haga clic en `Enable` para reclamar el PTT local para su estación.

Si otra estación ya tiene el PTT, el botón Enable está oculto. La etiqueta, en cambio, identifica a la otra estación e indica que esta debe reclamar o liberar el PTT desde su propio cliente. No es posible forzar la transferencia del PTT desde otra estación a través de este cuadro de diálogo.

5. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Enable (superior) | Habilita o deshabilita multiFLEX en la radio. Muestra "Enabled" (verde) o "Disabled" (rojo) para reflejar el estado actual. |
| Tabla Stations | Lista todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Su propia estación aparece resaltada. Una marca de verificación en LOCAL PTT indica qué estación tiene el PTT. |
| Etiqueta Local PTT | Describe el estado actual del PTT en relación con su estación, o indica el nombre de la otra estación que debe actuar. Está oculta cuando solo hay una estación conectada. |
| Enable (PTT) | Reclama la autoridad de PTT local para su estación. Visible únicamente cuando su estación no tiene el PTT en ese momento y hay al menos dos estaciones conectadas. |
| Close | Cierra el cuadro de diálogo. |

## Consejos

- Su estación aparece resaltada en la columna STATION, lo que facilita encontrarla en una tabla con muchas entradas.
- La columna STATION muestra las entradas como `program: station` cuando el nombre del programa y el nombre de la estación son diferentes.
- TX ANT y TX FREQ (MHz) reflejan el slice (receptor/transmisor activo) de transmisión de cada estación. Si esos datos aún no están disponibles, las columnas muestran `----`.

## Solución de problemas

- **El botón Enable (PTT) no es visible** — Su estación ya tiene el PTT, solo hay una estación conectada (en modo de estación única el PTT se otorga automáticamente), o bien otra estación tiene el PTT y debe liberarlo desde su propio cliente.
- **Los controles de PTT no aparecen** — Solo hay una estación conectada en este momento. Los controles aparecen únicamente cuando hay dos o más estaciones presentes en la tabla Stations.
- **La tabla Stations está vacía** — Es posible que la conexión con la radio se haya interrumpido, o que multiFLEX no esté habilitado. Verifique que el botón Enable en la parte superior del cuadro de diálogo muestre "Enabled".

## Relacionados

- [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
