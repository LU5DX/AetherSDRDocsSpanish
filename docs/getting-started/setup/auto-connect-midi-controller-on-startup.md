# Conexión automática del controlador MIDI al iniciar

Cuando AetherSDR se inicia, puede reabrir automáticamente el último puerto MIDI utilizado, de modo que su controlador esté listo sin intervención manual en cada sesión.

## Antes de comenzar

- AetherSDR debe haber sido compilado con soporte MIDI (la opción `Settings > MIDI Mapping...` debe aparecer en el menú Settings).
- Su controlador MIDI debe estar físicamente conectado y reconocido por el sistema operativo.
- Debe haberse conectado al puerto al menos una vez de forma manual para que AetherSDR tenga un dispositivo que reabrir. Consulte [Conectar un controlador MIDI](connect-a-midi-controller.md).

## Pasos

1. Vaya a `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Port:**, seleccione su controlador MIDI.
3. Haga clic en **Connect**. El estado del puerto cambia para mostrar el nombre del dispositivo conectado.
4. Active la casilla **Auto-connect on startup**.

AetherSDR guarda tanto `MidiPort` como `MidiAutoConnect` de inmediato. En el siguiente inicio, el puerto se reabre automáticamente sin ninguna acción adicional.

## Función de cada control

| Control | Tipo | Comportamiento | Ajuste guardado |
|---|---|---|---|
| **Port:** | Cuadro combinado | Selecciona el dispositivo de entrada MIDI a utilizar | `MidiPort` |
| **Refresh** | Botón | Vuelve a explorar los puertos MIDI disponibles | — |
| **Connect** | Botón | Abre o cierra el puerto MIDI seleccionado | — |
| **Auto-connect on startup** | Casilla de verificación | Reabre el puerto MIDI guardado cada vez que AetherSDR se inicia | `MidiAutoConnect` |

## Consejos

- Si desconecta y vuelve a conectar el controlador, haga clic en **Refresh** para actualizar la lista **Port:** antes de hacer clic en **Connect**.
- El estado del puerto y el indicador de actividad se actualizan en tiempo real. Confirme que el indicador de actividad muestra mensajes entrantes antes de cerrar el diálogo.

## Solución de problemas

- **La lista de puertos está vacía después de conectar el controlador** — Haga clic en **Refresh** para volver a explorar. Si el puerto sigue sin aparecer, verifique que el sistema operativo reconoce el dispositivo.
- **La conexión automática no funciona en el siguiente inicio** — Confirme que hizo clic en **Connect** y vio un estado de conexión establecida antes de activar **Auto-connect on startup**. El ajuste guarda el nombre del puerto abierto más recientemente; si el nombre del dispositivo cambió (por ejemplo, al usar un puerto USB diferente en algunos sistemas), seleccione el puerto correcto manualmente, conéctese de nuevo y vuelva a activar **Auto-connect on startup**.

## Temas relacionados

- [Conectar un controlador MIDI](connect-a-midi-controller.md)
- [Descripción general de la asignación de controladores MIDI](../../features/midi-mapping/overview.md)
- [Registrar un enlace nuevo con el modo Learn](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Guardar la asignación actual como perfil con nombre](../../features/midi-mapping/save-the-current-mapping-as-a-named-profile.md)
