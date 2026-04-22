# Conexión automática del controlador MIDI al inicio

Configure AetherSDR para que reabra su controlador MIDI automáticamente cada vez que se inicie la aplicación, de modo que no tenga que conectarlo manualmente tras cada reinicio.

## Antes de comenzar

- El controlador MIDI ya debe estar conectado a su computadora y visible como dispositivo de entrada MIDI.
- Debe haberse conectado al dispositivo al menos una vez mediante el selector Port: y el botón Connect, para que AetherSDR tenga un nombre de dispositivo que recordar. Consulte [Conectar un controlador MIDI](connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Port:**, seleccione su controlador MIDI de la lista. Si no aparece, haga clic en Refresh.
3. Haga clic en Connect. El estado del puerto cambia para mostrar el nombre del dispositivo conectado.
4. Active **Auto-connect on startup**.

AetherSDR guarda inmediatamente tanto `MidiPort` como `MidiAutoConnect` en la configuración persistente. En el siguiente inicio, el puerto se abrirá automáticamente sin ninguna acción adicional.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Port: | Cuadro combinado | Selecciona el dispositivo de entrada MIDI que se abrirá. | `MidiPort` |
| Refresh | Botón | Vuelve a analizar los puertos MIDI disponibles y actualiza la lista Port:. | — |
| Connect | Botón | Abre o cierra el puerto MIDI seleccionado. La etiqueta cambia a Disconnect cuando el puerto está abierto. | — |
| Auto-connect on startup | Casilla de verificación | Cuando está activada, AetherSDR reabre el puerto MIDI guardado en cada inicio. | `MidiAutoConnect` |

## Consejos

- Si cambia el nombre del controlador o lo vuelve a conectar y el nombre del puerto cambia, desactive **Auto-connect on startup**, vuelva a seleccionar el puerto correcto en Port:, haga clic en Connect y active nuevamente **Auto-connect on startup** para actualizar el nombre del dispositivo guardado.
- El indicador de actividad junto al estado del puerto se actualiza con cada mensaje MIDI entrante, lo que permite confirmar rápidamente que el puerto se abrió correctamente al inicio.

## Solución de problemas

- **El puerto no aparece en Port: tras el inicio** — El controlador no estaba conectado antes de que AetherSDR arrancara. Haga clic en Refresh para volver a analizar, seleccione el puerto, haga clic en Connect y vuelva a guardar la preferencia activando **Auto-connect on startup**.
- **Auto-connect on startup está activado pero el controlador no está conectado tras el inicio** — El nombre del dispositivo guardado en `MidiPort` ya no coincide con ningún puerto disponible, probablemente porque el controlador fue renombrado por el sistema operativo o conectado a un puerto USB diferente. Seleccione el puerto correcto en Port:, haga clic en Connect y reactive **Auto-connect on startup**.

## Relacionado

- [Conectar un controlador MIDI](connect-a-midi-controller.md)
- [Descripción general de MIDI Controller Mapping](../../features/midi-mapping/overview.md)
- [Registrar un nuevo enlace con el modo Learn](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Guardar la asignación actual como perfil con nombre](../../features/midi-mapping/save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado anteriormente](../../features/midi-mapping/load-a-previously-saved-midi-profile.md)
