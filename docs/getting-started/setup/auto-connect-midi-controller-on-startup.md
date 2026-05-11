# Conexión automática del controlador MIDI al iniciar

Cuando AetherSDR se inicia, puede reabrir automáticamente el último puerto MIDI utilizado para que su controlador esté listo sin intervención manual en cada sesión.

## Antes de comenzar

- AetherSDR debe haber sido compilado con soporte MIDI (`Settings > MIDI Mapping...` debe aparecer en el menú de Configuración).
- Su controlador MIDI debe estar físicamente conectado y reconocido por el sistema operativo.
- Debe haberse conectado al puerto al menos una vez manualmente para que AetherSDR tenga un dispositivo que reabrir. Consulte [Conectar un controlador MIDI](connect-a-midi-controller.md).

## Pasos

1. Vaya a `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Port:**, seleccione su controlador MIDI.
3. Haga clic en **Connect**. El estado del puerto cambia para mostrar el nombre del dispositivo conectado.
4. Marque **Auto-connect on startup**.

AetherSDR guarda tanto `MidiPort` como `MidiAutoConnect` inmediatamente. En el próximo inicio, el puerto se reabre automáticamente sin ninguna acción adicional.

## Función de cada control

| Control | Tipo | Comportamiento | Configuración persistente |
|---|---|---|---|
| **Port:** | Cuadro combinado | Selecciona el dispositivo de entrada MIDI a usar | `MidiPort` |
| **Refresh** | Botón | Vuelve a escanear los puertos MIDI disponibles | — |
| **Connect** | Botón | Abre o cierra el puerto MIDI seleccionado | — |
| **Auto-connect on startup** | Casilla de verificación | Vuelve a abrir el puerto MIDI guardado cada vez que AetherSDR se inicia | `MidiAutoConnect` |

## Uso del diálogo de mapeo MIDI

El diálogo **MIDI Controller Mapping** le permite configurar un controlador MIDI. Use el cuadro combinado **Category** para filtrar la lista de **Parameter**. Las categorías disponibles incluyen:

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

Seleccione un **Parameter** para asignar, luego haga clic en **Learn** para grabar un enlace desde su controlador MIDI. La tabla **Bindings** muestra los enlaces existentes con controles por fila de **Invert**, **Relative** y eliminar (**×**).

Use el cuadro combinado **Profile:** y los botones **Save** y **Load** para gestionar perfiles de mapeo con nombre.

## Consejos

- Si desconecta y vuelve a conectar el controlador, haga clic en **Refresh** para repoblar la lista **Port:** antes de hacer clic en **Connect**.
- El estado del puerto y el indicador de actividad se actualizan en tiempo real. Confirme que el indicador de actividad muestre mensajes entrantes antes de cerrar el diálogo.

## Solución de problemas

- **La lista de puertos está vacía después de conectar el controlador** — Haga clic en **Refresh** para volver a escanear. Si el puerto aún no aparece, verifique que el sistema operativo reconozca el dispositivo.
- **La conexión automática no funciona en el próximo inicio** — Confirme que hizo clic en **Connect** y vio un estado conectado antes de marcar **Auto-connect on startup**. La configuración guarda el nombre del puerto abierto más recientemente; si el nombre del dispositivo cambió (por ejemplo, en un puerto USB diferente en algunos sistemas), seleccione el puerto correcto manualmente, conéctese nuevamente y vuelva a marcar **Auto-connect on startup**.

## Relacionados

- [Conectar un controlador MIDI](connect-a-midi-controller.md)
- [Descripción general del mapeo de controlador MIDI](../../features/midi-mapping/overview.md)
- [Grabar un nuevo enlace con el modo Learn](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Guardar el mapeo actual como un perfil con nombre](../../features/midi-mapping/save-the-current-mapping-as-a-named-profile.md)
- [Disparadores para manipulador telegráfico y paddle](../../features/midi-mapping/cw-triggers.md)
