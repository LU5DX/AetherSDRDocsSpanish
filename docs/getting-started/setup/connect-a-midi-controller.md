# Conectar un controlador MIDI

Esta página explica cómo seleccionar y conectar un controlador MIDI en AetherSDR para que los mandos físicos, faders y botones del dispositivo estén disponibles para asignaciones de parámetros.

## Antes de comenzar

- El controlador MIDI debe estar conectado y reconocido por el sistema operativo antes de abrir AetherSDR.
- AetherSDR debe haberse compilado con soporte MIDI (`Settings > MIDI Mapping...` debe estar presente en el menú; si no aparece, su versión no incluye MIDI).

## Pasos

1. Vaya a `Settings > MIDI Mapping...`. Se abre el diálogo **MIDI Controller Mapping**.
2. En la sección **MIDI Device**, abra el menú desplegable **Port:** y seleccione su controlador de la lista.
3. Si su controlador no aparece, haga clic en **Refresh**. AetherSDR vuelve a examinar los puertos MIDI disponibles y actualiza la lista **Port:**.
4. Haga clic en **Connect**. AetherSDR abre el puerto seleccionado. El área de estado del puerto cambia a **Connected:** seguido del nombre del dispositivo, y la etiqueta del botón **Connect** cambia a **Disconnect**.
5. Mueva un mando o presione un botón en el controlador. El indicador de actividad junto al estado del puerto debe mostrar el mensaje MIDI más reciente recibido (por ejemplo, `Ch 1 CC #7 = 64`). Esto confirma que el dispositivo está enviando datos.
6. Para que AetherSDR reabra este puerto cada vez que inicie, marque **Auto-connect on startup**.
7. Haga clic en **Close** cuando termine.

## Función de cada control

| Control | Tipo | Comportamiento | Configuración persistente |
|---|---|---|---|
| **Port:** | Menú desplegable | Selecciona el dispositivo de entrada MIDI a usar. | `MidiPort` |
| **Refresh** | Botón | Vuelve a examinar los puertos MIDI disponibles y actualiza la lista **Port:**. | — |
| **Connect** | Botón | Abre el puerto MIDI seleccionado. La etiqueta cambia a **Disconnect** mientras el puerto está abierto; al hacer clic de nuevo lo cierra. | — |
| **Auto-connect on startup** | Casilla de verificación | Cuando está marcada, AetherSDR reabre el último puerto MIDI conectado al iniciar. | `MidiAutoConnect` |
| Estado del puerto | Indicador | Muestra **Connected:** seguido del nombre del dispositivo cuando el puerto está abierto, o **Disconnected** cuando está cerrado. | — |
| Indicador de actividad | Indicador | Muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). | — |

## Consejos

- Si el estado del puerto muestra **Connected** pero el indicador de actividad nunca se actualiza, verifique que su controlador esté configurado para transmitir en un canal MIDI y que ninguna otra aplicación tenga el puerto bloqueado en modo exclusivo.
- El indicador de actividad se actualiza en tiempo real. Úselo para verificar que el puerto correcto esté seleccionado antes de crear asignaciones.

## Solución de problemas

- **`Settings > MIDI Mapping...` no está en el menú** — Su versión de AetherSDR fue compilada sin soporte MIDI. Obtenga una versión que incluya la función `HAVE_MIDI`.
- **El controlador no aparece en la lista Port:** — Haga clic en **Refresh**. Si el dispositivo sigue sin aparecer, verifique que el sistema operativo lo reconozca (compruebe en la configuración de dispositivos MIDI o de audio de su sistema) y que ninguna otra aplicación tenga un bloqueo exclusivo sobre el puerto.
- **El estado del puerto muestra Connected pero el indicador de actividad está en blanco** — El dispositivo está abierto pero no envía datos. Verifique la alimentación del controlador, la conexión USB o DIN, y que esté configurado para enviar MIDI.

## Relacionados

- [Descripción general de MIDI Controller Mapping](../../features/midi-mapping/overview.md)
- [Conectar automáticamente el controlador MIDI al iniciar](auto-connect-midi-controller-on-startup.md)
- [Registrar una nueva asignación con el modo Learn](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Cargar un perfil MIDI guardado anteriormente](../../features/midi-mapping/load-a-previously-saved-midi-profile.md)
