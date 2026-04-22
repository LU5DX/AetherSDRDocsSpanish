# Conectar un controlador MIDI

Use esta página para seleccionar su dispositivo de entrada MIDI, abrir el puerto y confirmar que AetherSDR está recibiendo mensajes de su controlador.

## Antes de comenzar

- El controlador MIDI debe estar conectado a la computadora y reconocido por el sistema operativo antes de abrir AetherSDR.
- La compatibilidad con MIDI debe estar compilada (`HAVE_MIDI`). Si `Settings > MIDI Mapping...` no aparece en el menú, su versión de compilación no incluye MIDI.

## Pasos

1. Vaya a `Settings > MIDI Mapping...`. Se abre el diálogo MIDI Controller Mapping.
2. En el cuadro combinado Port:, seleccione su controlador MIDI de la lista de dispositivos disponibles. Si la lista está vacía o su dispositivo no aparece, haga clic en Refresh para volver a buscar.
3. Haga clic en Connect. La etiqueta de estado del puerto cambia a **Connected:** seguida del nombre del dispositivo. Si la conexión falla, la etiqueta permanece como **Disconnected**.
4. Mueva un mando, fader o botón en su controlador. El indicador de actividad muestra el mensaje más reciente recibido, por ejemplo `Ch 1 CC #7 = 64`. Esto confirma que AetherSDR está recibiendo datos MIDI.
5. Si desea que AetherSDR abra este dispositivo automáticamente en cada inicio, marque Auto-connect on startup. Esta configuración se guarda como `MidiAutoConnect`.
6. Haga clic en Close.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Port: | Cuadro combinado | Selecciona el dispositivo de entrada MIDI. | `MidiPort` |
| Refresh | Botón | Vuelve a buscar los puertos MIDI disponibles. | — |
| Connect | Botón | Abre o cierra el puerto MIDI seleccionado. La etiqueta cambia a **Disconnect** cuando el puerto está abierto. | — |
| Auto-connect on startup | Casilla de verificación | Reabre el puerto MIDI guardado cada vez que AetherSDR se inicia. | `MidiAutoConnect` |
| Port status | Indicador | Muestra **Connected:** con el nombre del dispositivo, o **Disconnected**. | — |
| Activity indicator | Indicador | Muestra el mensaje MIDI más reciente recibido (canal, tipo, número, valor). | — |

## Solución de problemas

- **La lista de Port: está vacía** — El sistema operativo aún no ha enumerado el dispositivo. Desconecte y vuelva a conectar el controlador, luego haga clic en Refresh.
- **Connect falla y el estado permanece en Disconnected** — Es posible que otra aplicación tenga acceso exclusivo al puerto MIDI. Cierre cualquier DAW, enrutador MIDI virtual u otra aplicación SDR que pueda mantener el puerto abierto y, a continuación, haga clic de nuevo en Connect.
- **El indicador de actividad no muestra mensajes después de conectar** — Verifique que el controlador esté enviando en el canal y tipo de mensaje que espera. Pruebe moviendo un control diferente. Si no aparece nada, es posible que el puerto se haya abierto pero el dispositivo no esté transmitiendo.

## Relacionados

- [Descripción general de MIDI Controller Mapping](../../features/midi-mapping/overview.md)
- [Registrar un nuevo enlace con el modo Learn](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Conectar automáticamente el controlador MIDI al inicio](auto-connect-midi-controller-on-startup.md)
- [Cargar un perfil MIDI guardado anteriormente](../../features/midi-mapping/load-a-previously-saved-midi-profile.md)
- [Guardar la asignación actual como un perfil con nombre](../../features/midi-mapping/save-the-current-mapping-as-a-named-profile.md)
