# Conectar un controlador MIDI

Esta página explica cómo seleccionar y conectar un controlador MIDI en AetherSDR para que los mandos físicos, los deslizadores y los botones del dispositivo estén disponibles para las asignaciones de parámetros.

## Antes de empezar

- Su controlador MIDI debe estar enchufado y reconocido por el sistema operativo antes de abrir AetherSDR.
- AetherSDR debe haber sido compilado con soporte MIDI (`Settings > MIDI Mapping...` debe estar presente en el menú; si falta, su compilación no incluye MIDI).

## Pasos

1. Vaya a `Settings > MIDI Mapping...`. Se abre el diálogo **MIDI Controller Mapping**.
2. En la sección **MIDI Device**, abra la lista desplegable **Port:** y seleccione su controlador de la lista.
3. Si su controlador no aparece, haga clic en **Refresh**. AetherSDR vuelve a escanear los puertos MIDI disponibles y actualiza la lista **Port:**.
4. Haga clic en **Connect**. AetherSDR abre el puerto seleccionado. El área de estado del puerto cambia a **Connected:** seguido del nombre del dispositivo, y la etiqueta del botón **Connect** cambia a **Disconnect**.
5. Gire un mando o presione un botón en el controlador. El indicador de actividad junto al estado del puerto debería mostrar el mensaje MIDI más reciente recibido (por ejemplo, `Ch 1 CC #7 = 64`). Esto confirma que el dispositivo está enviando datos.
6. Para que AetherSDR vuelva a abrir este puerto cada vez que se inicie, marque **Auto-connect on startup**.
7. Haga clic en **Close** cuando haya terminado.

## Función de cada control

| Control | Tipo | Comportamiento | Configuración persistente |
|---|---|---|---|
| **Port:** | Desplegable | Selecciona el dispositivo de entrada MIDI a utilizar. | `MidiPort` |
| **Refresh** | Botón | Vuelve a escanear los puertos MIDI disponibles y actualiza la lista **Port:**. | — |
| **Connect** | Botón | Abre el puerto MIDI seleccionado. La etiqueta cambia a **Disconnect** mientras el puerto está abierto; al hacer clic de nuevo se cierra. | — |
| **Auto-connect on startup** | Casilla de verificación | Cuando está marcada, AetherSDR vuelve a abrir el último puerto MIDI conectado al iniciarse. | `MidiAutoConnect` |
| Estado del puerto | Indicador | Muestra **Connected:** seguido del nombre del dispositivo cuando el puerto está abierto, o **Disconnected** cuando está cerrado. | — |
| Indicador de actividad | Indicador | Muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). | — |

## Consejos

- Si el estado del puerto muestra **Connected** pero el indicador de actividad nunca se actualiza, verifique que su controlador esté configurado para transmitir en un canal MIDI y que ninguna otra aplicación tenga el puerto bloqueado exclusivamente.
- El indicador de actividad se actualiza en tiempo real. Úselo para verificar que el puerto correcto esté seleccionado antes de crear asignaciones.

## Solución de problemas

- **`Settings > MIDI Mapping...` no está en el menú** — Su compilación de AetherSDR se realizó sin soporte MIDI. Obtenga una compilación que incluya la característica `HAVE_MIDI`.
- **El controlador no aparece en la lista Port:** — Haga clic en **Refresh**. Si el dispositivo aún no aparece, verifique que el sistema operativo lo reconozca (consulte en la configuración de dispositivos MIDI o de audio de su sistema) y que ninguna otra aplicación mantenga un bloqueo exclusivo en el puerto.
- **El estado del puerto muestra Connected pero el indicador de actividad está en blanco** — El dispositivo está abierto pero no envía datos. Verifique la alimentación del controlador, la conexión USB o DIN, y que esté configurado para emitir MIDI.

## Relacionado

- [MIDI Controller Mapping overview](../../features/midi-mapping/overview.md)
- [Auto-connect MIDI controller on startup](auto-connect-midi-controller-on-startup.md)
- [Record a new binding with Learn mode](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Load a previously saved MIDI profile](../../features/midi-mapping/load-a-previously-saved-midi-profile.md)
