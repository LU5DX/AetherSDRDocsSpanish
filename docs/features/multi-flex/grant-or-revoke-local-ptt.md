# Conceder o revocar PTT local

Use el panel multiFLEX para reclamar la autoridad PTT local para su estación o para ver qué estación la posee actualmente. Esto es necesario cuando varios clientes comparten el mismo FLEX-8600 y solo una estación puede transmitir a la vez.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel multiFLEX requiere una conexión activa a la radio.
- multiFLEX debe estar habilitado en la radio. Si el panel muestra "Disabled", consulte primero [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md).
- Deben estar conectadas al menos dos estaciones para que aparezcan los controles PTT. Con una sola estación presente, el botón PTT está oculto.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el panel multiFLEX.
2. Revise la tabla de estaciones. La columna LOCAL PTT muestra una marca de verificación junto a la estación que actualmente posee PTT.
3. Si su estación no posee PTT, la etiqueta debajo de la tabla muestra `Enable Local PTT for this station (<nombre de su estación>):` y el botón Enable está visible.
4. Haga clic en `Enable` para reclamar PTT local para su estación.

Si otra estación ya posee PTT, el botón Enable está oculto. La etiqueta, en su lugar, identifica la otra estación y señala que debe reclamar o liberar PTT desde su propio cliente. No puede forzar la salida de PTT de otra estación a través de este cuadro de diálogo.

5. Haga clic en `Close` cuando haya terminado.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Enable (superior) | Habilita o deshabilita multiFLEX en la radio. Muestra "Enabled" (verde) o "Disabled" (rojo) para reflejar el estado actual. |
| Tabla de estaciones | Enumera cada cliente multiFLEX conectado. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz) y una columna de acción Disconnect. Su propia estación aparece resaltada. Una marca de verificación en LOCAL PTT indica qué estación posee PTT. |
| Etiqueta PTT local | Describe el estado actual de PTT en relación con su estación, o nombra la otra estación que debe actuar. Oculto cuando solo una estación está conectada. |
| Enable (PTT) | Reclama autoridad PTT local para su estación. Visible solo cuando su estación no posee PTT actualmente y al menos dos estaciones están conectadas. |
| Botón Disconnect | Aparece en la última columna de la tabla de estaciones para cada entrada de cliente. Haga clic para enviar una solicitud de desconexión para ese cliente. La etiqueta del botón cambia a "Pending..." mientras la radio confirma la desconexión. El botón está deshabilitado para su propia estación. |
| Close | Cierra el cuadro de diálogo. |

## Desconectar un cliente

Para desconectar otro cliente de la radio:

1. Localice el cliente en la tabla de estaciones.
2. Haga clic en el botón **Disconnect** en la última columna de la fila de ese cliente. La etiqueta del botón cambia a "Pending..." hasta que la radio confirme la desconexión y el cliente se elimine de la tabla.
3. El botón Disconnect está deshabilitado para su propia estación — no puede desconectarse a sí mismo desde este cuadro de diálogo.

## Consejos

- Su estación está resaltada en la columna STATION, lo que facilita encontrarla en una tabla con muchas entradas.
- La columna STATION muestra las entradas como `programa: estación` cuando el nombre del programa y el nombre de la estación difieren. Si solo se proporciona el nombre de la estación, aparece sin el prefijo del programa. Si no hay ningún nombre disponible, se muestra un identificador alternativo como `cliente 0x12345678` (identificador hexadecimal del cliente).
- TX ANT y TX FREQ (MHz) reflejan el slice de transmisión de cada estación. Si esos datos aún no están disponibles, las columnas muestran `----`.
- El cuadro de diálogo recuerda su tamaño y posición entre sesiones.

## Solución de problemas

- **El botón Enable (PTT) no es visible** — Su estación ya posee PTT, solo una estación está conectada (el modo de estación única concede PTT automáticamente), u otra estación posee PTT y debe liberarlo desde su propio cliente.
- **Los controles PTT faltan por completo** — Solo una estación está conectada actualmente. Los controles aparecen solo cuando hay dos o más estaciones presentes en la tabla de estaciones.
- **La tabla de estaciones está vacía** — La conexión a la radio puede haberse perdido, o multiFLEX no está habilitado. Verifique que el botón Enable en la parte superior del cuadro de diálogo muestre "Enabled".
- **El botón Disconnect muestra "Pending..." durante un tiempo prolongado** — La radio puede estar procesando la solicitud de desconexión. Si el cliente permanece visible, la solicitud de desconexión no pudo procesarse. Cierre y vuelva a abrir el cuadro de diálogo para actualizar la lista de estaciones.

## Relacionados

- [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md)
- [Check which antenna and frequency each TX station is using](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [See all stations connected to this FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
