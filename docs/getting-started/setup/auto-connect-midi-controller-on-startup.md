# Conexión automática del controlador MIDI al inicio

Cuando AetherSDR se inicia, puede reabrir automáticamente el último puerto MIDI utilizado para que su controlador esté listo sin intervención manual en cada sesión.

## Antes de comenzar

- AetherSDR debe haber sido compilado con soporte MIDI (`Settings > MIDI Mapping...` debe aparecer en el menú Settings).
- Su controlador MIDI debe estar físicamente conectado y reconocido por el sistema operativo.
- Debe haber conectado el puerto al menos una vez manualmente para que AetherSDR tenga un dispositivo que reabrir. Consulte [Connect a MIDI controller](connect-a-midi-controller.md).

## Pasos

1. Vaya a `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Port:**, seleccione su controlador MIDI.
3. Haga clic en **Connect**. El estado del puerto cambia para mostrar el nombre del dispositivo conectado.
4. Marque **Auto-connect on startup**.

AetherSDR guarda `MidiPort` y `MidiAutoConnect` inmediatamente. En el próximo inicio, el puerto se reabre automáticamente sin necesidad de ninguna acción adicional.

## Función de cada control

| Control | Tipo | Comportamiento | Ajuste persistente |
|---|---|---|---|
| **Port:** | Cuadro combinado | Selecciona el dispositivo de entrada MIDI a usar | `MidiPort` |
| **Refresh** | Botón | Vuelve a escanear los puertos MIDI disponibles | — |
| **Connect** | Botón | Abre o cierra el puerto MIDI seleccionado | — |
| **Auto-connect on startup** | Casilla de verificación | Vuelve a abrir el puerto MIDI guardado cada vez que AetherSDR se inicia | `MidiAutoConnect` |

## Uso del cuadro de diálogo MIDI Mapping

El cuadro de diálogo **MIDI Controller Mapping** le permite configurar un controlador MIDI. Use el cuadro combinado **Category** para filtrar la lista de **Parameter**. Las categorías disponibles incluyen:

- All
- RX
- TX
- Phone/CW
- EQ
- Global
- Mode
- Band
- Filter
- Slice
- Display
- Frequency

Seleccione un **Parameter** para asignar, luego haga clic en **Learn** para grabar una vinculación desde su controlador MIDI. En la categoría Phone/CW, hay tres acciones momentáneas (Gate) disponibles: **Trigger straight key**, **Trigger CW Left Paddle** y **Trigger CW Right Paddle**. Los IDs con puntos heredados (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al leerlos.

La **Bindings table** muestra las vinculaciones existentes con controles por fila de **Invert**, **Relative** y eliminar (**×**).

Use el cuadro combinado **Profile:** y los botones **Save** y **Load** para gestionar perfiles de mapeo con nombre.

## Consejos

- Si desconecta y vuelve a conectar el controlador, haga clic en **Refresh** para repoblar la lista **Port:** antes de hacer clic en **Connect**.
- El estado del puerto y el indicador de actividad se actualizan en tiempo real. Confirme que el indicador de actividad muestra mensajes entrantes antes de cerrar el cuadro de diálogo.
- El cuadro de diálogo recuerda su tamaño y posición entre sesiones.

## Solución de problemas

- **La lista de puertos está vacía después de conectar el controlador** — Haga clic en **Refresh** para volver a escanear. Si el puerto aún no aparece, verifique que el sistema operativo reconozca el dispositivo.
- **La conexión automática no funciona en el próximo inicio** — Confirme que hizo clic en **Connect** y vio un estado de conectado antes de marcar **Auto-connect on startup**. El ajuste guarda el nombre del puerto abierto más recientemente; si el nombre del dispositivo cambió (por ejemplo, en un puerto USB diferente en algunos sistemas), seleccione el puerto correcto manualmente, conéctelo de nuevo y vuelva a marcar **Auto-connect on startup**.

## Relacionados

- [Connect a MIDI controller](connect-a-midi-controller.md)
- [MIDI Controller Mapping overview](../../features/midi-mapping/overview.md)
- [Record a new binding with Learn mode](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Save the current mapping as a named profile](../../features/midi-mapping/save-the-current-mapping-as-a-named-profile.md)
- [Triggers for CW straight key and paddles](../../features/midi-mapping/cw-triggers.md)
