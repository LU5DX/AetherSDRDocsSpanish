# Conectar un controlador MIDI

Esta página explica cómo seleccionar y conectar un controlador MIDI en AetherSDR para que las perillas, los deslizadores y los botones físicos del dispositivo estén disponibles para asignaciones de parámetros.

## Antes de comenzar

- Su controlador MIDI debe estar enchufado y reconocido por el sistema operativo antes de abrir AetherSDR.
- AetherSDR debe haber sido compilado con soporte MIDI (la opción `Settings > MIDI Mapping...` debe estar presente en el menú; si falta, su compilación no incluye MIDI).

## Pasos

1. Vaya a `Settings > MIDI Mapping...`. Se abre el diálogo **MIDI Controller Mapping**.
2. En la sección **MIDI Device**, abra la lista desplegable **Port:** y seleccione su controlador de la lista.
3. Si su controlador no aparece, haga clic en **Refresh**. AetherSDR vuelve a escanear los puertos MIDI disponibles y rellena la lista **Port:**.
4. Haga clic en **Connect**. AetherSDR abre el puerto seleccionado. El área de estado del puerto cambia a **Opened**, y la etiqueta del botón **Connect** cambia a **Disconnect**.
5. Mueva una perilla o presione un botón en el controlador. El indicador de actividad junto al estado del puerto debe mostrar el mensaje MIDI más reciente recibido (por ejemplo, `Ch 1 CC #7 = 64`). Esto confirma que el dispositivo está enviando datos.
6. Para que AetherSDR vuelva a abrir este puerto cada vez que se inicie, marque **Auto-connect on startup**.
7. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento | Ajuste persistido |
|---|---|---|---|
| **Port:** | Lista desplegable | Selecciona el dispositivo de entrada MIDI a usar. | `MidiPort` |
| **Refresh** | Botón | Vuelve a escanear los puertos MIDI disponibles y rellena la lista **Port:**. | — |
| **Connect** | Botón | Abre el puerto MIDI seleccionado. La etiqueta cambia a **Disconnect** mientras el puerto está abierto; hacer clic de nuevo lo cierra. | — |
| **Auto-connect on startup** | Casilla de verificación | Cuando está marcada, AetherSDR vuelve a abrir el último puerto MIDI conectado al iniciar. | `MidiAutoConnect` |
| **Category** | Lista desplegable | Filtra el cuadro combinado **Parameter** para mostrar solo los parámetros de la categoría seleccionada. Categorías disponibles: All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency. | — |
| **Parameter** | Lista desplegable | Elige el parámetro a asignar mediante MIDI. Cuando **Category** está configurada en "Phone/CW", hay tres acciones momentáneas (Gate) disponibles: "Trigger straight key" (id: `cwkey`), "Trigger CW Left Paddle" (id: `cwdit`), "Trigger CW Right Paddle" (id: `cwdah`). Los ID heredados con puntos (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al leer. | — |
| **Learn** | Botón | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado. | — |
| **Manual…** | Botón | Abre un diálogo para escribir el canal, el tipo de mensaje y el número de una asignación en lugar de usar el modo **Learn**. Abre el mismo editor manual que usa el botón de edición por fila. | — |
| **Bindings table** | Lista | Muestra las asignaciones existentes con controles por fila de **Invert**, **Relative**, edición (✎) y eliminación. Columnas: Parameter, MIDI Source, Channel, Invert, Relative, (edit), (delete). | — |
| **✎ (edit binding)** | Botón | Abre el editor manual para corregir el canal, el tipo y el número de esta asignación. | — |
| **Invert** | Casilla de verificación | Invierte el sentido del control para la fila. | — |
| **Relative** | Casilla de verificación | Trata el control como un codificador rotatorio sin fin. | — |
| **× (delete row)** | Botón | Elimina esa asignación. | — |
| **Clear All** | Botón | Elimina todas las asignaciones. | — |
| **Profile:** | Lista desplegable | Selecciona un perfil de asignación MIDI guardado. | — |
| **Save** | Botón | Guarda las asignaciones actuales como un perfil. | — |
| **Load** | Botón | Carga el perfil seleccionado. | — |
| **Import...** | Botón | Importa un archivo de perfil al almacén — un XML de perfil de AetherSDR o un archivo `.map` de SmartSDR. Informa cuántas asignaciones se importaron y le permite hacer clic en **Load** para aplicarlas. | `MidiImportExportPath` (directorio recordado) |
| **Export...** | Botón | Exporta las asignaciones actuales como un archivo XML de perfil de AetherSDR. | `MidiImportExportPath` (directorio recordado) |
| **Close** | Botón | Cierra el diálogo. | — |
| Estado del puerto | Indicador | Muestra **Opened** cuando el puerto está abierto, o **Closed** cuando no lo está. | — |
| Indicador de actividad | Indicador | Muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). | — |

## Crear y editar asignaciones

1. Seleccione una **Category** y un **Parameter** para asignar.
2. Cree la asignación de una de las siguientes maneras:
   - Haciendo clic en **Learn** y presionando la perilla, el deslizador o el botón de su controlador que desea usar, o
   - Haciendo clic en **Manual…** y escribiendo directamente el canal MIDI, el tipo de mensaje y el número de mensaje de la asignación. Esto es útil cuando conoce la especificación MIDI exacta de su control o cuando el controlador no está conectado en ese momento.
3. La nueva fila aparece en la **Bindings table**. Use los controles por fila para ajustarla:
   - **Invert** — marque para invertir el sentido del control.
   - **Relative** — marque si el control es un codificador rotatorio sin fin.
   - **✎** — edite el canal, el tipo de mensaje o el número de la asignación manualmente.
   - **×** — elimine esa asignación.

## Guardar y cargar perfiles

- **Save** — guarda las asignaciones actuales como un perfil con nombre en la lista **Profile:**.
- **Load** — aplica el perfil seleccionado a la sesión actual.
- **Import...** — importa un perfil de asignación desde un archivo. Puede cargar archivos XML de perfil de AetherSDR o archivos `.map` de SmartSDR. Después de la importación, haga clic en **Load** para aplicar las asignaciones importadas.
- **Export...** — guarda las asignaciones actuales como un archivo XML de perfil de AetherSDR que puede compartir o respaldar.

El directorio desde el que importó o al que exportó por última vez se recuerda para la próxima vez.

## Consejos

- Use la lista desplegable **Category** para reducir la lista de parámetros al crear asignaciones. Las categorías incluyen Mode, Band, Filter, Slice, Display y Frequency, además del conjunto original.
- Si el estado del puerto muestra **Opened** pero el indicador de actividad nunca se actualiza, verifique que su controlador esté configurado para transmitir en un canal MIDI y que ninguna otra aplicación tenga el puerto bloqueado exclusivamente.
- El indicador de actividad se actualiza en tiempo real. Úselo para verificar que el puerto correcto esté seleccionado antes de crear asignaciones.
- El botón **Manual…** y los botones de edición **✎** de cada fila abren el mismo editor, por lo que puede ingresar valores exactos de canal MIDI, tipo de mensaje y número sin mover un control físico.
- Marque **Invert** en una fila si el control se mueve en la dirección opuesta a la esperada.
- Marque **Relative** al asignar un codificador rotatorio sin fin para que AetherSDR trate los movimientos como pasos relativos.

## Solución de problemas

- **`Settings > MIDI Mapping...` no está en el menú** — Su compilación de AetherSDR se compiló sin soporte MIDI. Obtenga una compilación que incluya la característica `HAVE_MIDI`.
- **El controlador no aparece en la lista Port:** — Haga clic en **Refresh**. Si el dispositivo aún no aparece, verifique que el sistema operativo lo reconozca (compruébelo en la configuración de dispositivos MIDI o de audio de su sistema) y que ninguna otra aplicación tenga un bloqueo exclusivo del puerto.
- **El estado del puerto muestra Opened pero el indicador de actividad está en blanco** — El dispositivo está abierto pero no envía datos. Verifique la alimentación del controlador, la conexión USB o DIN, y que esté configurado para emitir MIDI.

## Relacionado

- [MIDI Controller Mapping overview](../../features/midi-mapping/overview.md)
- [Auto-connect MIDI controller on startup](auto-connect-midi-controller-on-startup.md)
- [Record a new binding with Learn mode](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Load a previously saved MIDI profile](../../features/midi-mapping/load-a-previously-saved-midi-profile.md)
