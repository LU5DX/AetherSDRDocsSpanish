# Conectar un controlador MIDI

Esta página explica cómo seleccionar y conectar un controlador MIDI en AetherSDR para que los potenciómetros físicos, faders y botones del dispositivo estén disponibles para asignaciones de parámetros.

## Antes de comenzar

- Su controlador MIDI debe estar enchufado y reconocido por el sistema operativo antes de abrir AetherSDR.
- AetherSDR debe haber sido compilado con soporte MIDI (`Settings > MIDI Mapping...` debe estar presente en el menú; si falta, su compilación no incluye MIDI).

## Pasos

1. Vaya a `Settings > MIDI Mapping...`. Se abre el diálogo **MIDI Controller Mapping**.
2. En la sección **MIDI Device**, abra la lista desplegable **Port:** y seleccione su controlador de la lista.
3. Si su controlador no aparece, haga clic en **Refresh**. AetherSDR vuelve a escanear los puertos MIDI disponibles y actualiza la lista **Port:**.
4. Haga clic en **Connect**. AetherSDR abre el puerto seleccionado. El área de estado del puerto cambia a **Connected:** seguido del nombre del dispositivo, y la etiqueta del botón **Connect** cambia a **Disconnect**.
5. Mueva un potenciómetro o presione un botón en el controlador. El indicador de actividad junto al estado del puerto debe mostrar el mensaje MIDI más reciente recibido (por ejemplo, `Ch 1 CC #7 = 64`). Esto confirma que el dispositivo está enviando datos.
6. Para que AetherSDR vuelva a abrir este puerto cada vez que se inicie, marque **Auto-connect on startup**.
7. Haga clic en **Close** cuando haya terminado.

## Función de cada control

| Control | Tipo | Comportamiento | Ajuste persistente |
|---|---|---|---|
| **Port:** | Desplegable | Selecciona el dispositivo de entrada MIDI a usar. | `MidiPort` |
| **Refresh** | Botón | Vuelve a escanear los puertos MIDI disponibles y actualiza la lista **Port:**. | — |
| **Connect** | Botón | Abre el puerto MIDI seleccionado. La etiqueta cambia a **Disconnect** mientras el puerto está abierto; al hacer clic de nuevo lo cierra. | — |
| **Auto-connect on startup** | Casilla de verificación | Cuando está marcada, AetherSDR vuelve a abrir el último puerto MIDI conectado al iniciarse. | `MidiAutoConnect` |
| **Category** | Desplegable | Filtra el cuadro combinado de **Parameter** para mostrar solo parámetros de la categoría seleccionada. Categorías disponibles: All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency. | — |
| **Parameter** | Desplegable | Elige el parámetro a asignar vía MIDI. Cuando **Category** está configurado en "Phone/CW", hay tres acciones momentáneas (Gate) disponibles: "Trigger straight key" (id: `cwkey`), "Trigger CW Left Paddle" (id: `cwdit`), "Trigger CW Right Paddle" (id: `cwdah`). Los IDs con puntos heredados (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al leerlos. | — |
| **Learn** | Botón | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado. | — |
| **Bindings table** | Lista | Muestra las asignaciones existentes con controles por fila de **Invert**, **Relative** y eliminación. Columnas: Parameter, MIDI Source, Channel, Invert, Relative, (eliminar). | — |
| **Invert** | Casilla de verificación | Invierte la dirección del control para la fila. | — |
| **Relative** | Casilla de verificación | Trata el control como un codificador sin fin. | — |
| **× (eliminar fila)** | Botón | Elimina esa asignación. | — |
| **Clear All** | Botón | Elimina todas las asignaciones. | — |
| **Profile:** | Desplegable | Selecciona un perfil de asignación MIDI guardado. | — |
| **Save** | Botón | Guarda las asignaciones actuales como un perfil. | — |
| **Load** | Botón | Carga el perfil seleccionado. | — |
| **Close** | Botón | Cierra el diálogo. | — |
| Estado del puerto | Indicador | Muestra **Connected:** seguido del nombre del dispositivo cuando el puerto está abierto, o **Disconnected** cuando está cerrado. | — |
| Indicador de actividad | Indicador | Muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). | — |

## Consejos

- Use la lista desplegable **Category** para reducir la lista de parámetros al crear asignaciones. Las categorías incluyen Mode, Band, Filter, Slice, Display y Frequency además del conjunto original.
- Si el estado del puerto muestra **Connected** pero el indicador de actividad nunca se actualiza, verifique que su controlador esté configurado para transmitir en un canal MIDI y que ninguna otra aplicación tenga el puerto bloqueado exclusivamente.
- El indicador de actividad se actualiza en tiempo real. Úselo para verificar que el puerto correcto esté seleccionado antes de crear asignaciones.

## Solución de problemas

- **`Settings > MIDI Mapping...` no está en el menú** — Su compilación de AetherSDR fue compilada sin soporte MIDI. Obtenga una compilación que incluya la funcionalidad `HAVE_MIDI`.
- **El controlador no aparece en la lista Port:** — Haga clic en **Refresh**. Si el dispositivo aún no aparece, verifique que el sistema operativo lo reconozca (compruébelo en la configuración de dispositivos MIDI o de audio de su sistema) y que ninguna otra aplicación tenga un bloqueo exclusivo en el puerto.
- **El estado del puerto muestra Connected pero el indicador de actividad está en blanco** — El dispositivo está abierto pero no envía datos. Verifique la alimentación del controlador, la conexión USB o DIN, y que esté configurado para emitir MIDI.

## Relacionado

- [MIDI Controller Mapping overview](../../features/midi-mapping/overview.md)
- [Auto-connect MIDI controller on startup](auto-connect-midi-controller-on-startup.md)
- [Record a new binding with Learn mode](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Load a previously saved MIDI profile](../../features/midi-mapping/load-a-previously-saved-midi-profile.md)
