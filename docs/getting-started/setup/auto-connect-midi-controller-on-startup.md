# Reconexión automática del controlador MIDI al iniciar

Cuando AetherSDR se inicia, puede reabrir automáticamente el último puerto MIDI utilizado para que su controlador esté listo sin intervención manual en cada sesión.

## Antes de comenzar

- AetherSDR debe haber sido compilado con soporte MIDI (`Settings > MIDI Mapping...` debe aparecer en el menú Settings).
- Su controlador MIDI debe estar físicamente conectado y reconocido por el sistema operativo.
- Debe haber conectado al puerto al menos una vez manualmente para que AetherSDR tenga un dispositivo que reabrir. Consulte [Conectar un controlador MIDI](connect-a-midi-controller.md).

## Pasos

1. Vaya a `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Port:**, seleccione su controlador MIDI.
3. Haga clic en **Connect**. El estado del puerto cambia para mostrar el nombre del dispositivo conectado.
4. Marque **Auto-connect on startup**.

AetherSDR guarda tanto `MidiPort` como `MidiAutoConnect` inmediatamente. En el próximo inicio, el puerto se reabre automáticamente sin ninguna acción adicional.

## Qué hace cada control

| Control | Tipo | Comportamiento | Configuración persistida |
|---|---|---|---|
| **Port:** | Cuadro combinado | Selecciona el dispositivo de entrada MIDI a utilizar | `MidiPort` |
| **Refresh** | Botón | Vuelve a escanear los puertos MIDI disponibles | — |
| **Connect** | Botón | Abre o cierra el puerto MIDI seleccionado | — |
| **Auto-connect on startup** | Casilla de verificación | Reabre el puerto MIDI guardado cada vez que AetherSDR se inicia | `MidiAutoConnect` |

## Uso del diálogo MIDI Mapping

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

Seleccione un **Parameter** para asignar y luego haga clic en **Learn** para registrar una vinculación desde su controlador MIDI. En la categoría Phone/CW, hay tres acciones momentáneas (Gate) disponibles: **Trigger straight key**, **Trigger CW Left Paddle** y **Trigger CW Right Paddle**. Los identificadores heredados con puntos (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al leerlos.

También puede crear una vinculación sin usar **Learn**: haga clic en **Manual…** para abrir un diálogo donde escribe el canal, el tipo de mensaje y el número de la vinculación. Esto es útil cuando conoce el mensaje MIDI exacto que envía su controlador pero no puede o no desea generarlo mediante el modo Learn. Cada fila en la **Bindings table** también tiene un botón de edición (✎) que abre el mismo editor manual para corregir el canal, el tipo de mensaje y el número de esa fila.

La **Bindings table** muestra las vinculaciones existentes con controles por fila de **Invert**, **Relative**, edición (✎) y eliminación (**×**). Columnas: Parameter, MIDI Source, Channel, Invert, Relative, (editar), (eliminar).

Use el cuadro combinado **Profile:** y los botones **Save** y **Load** para administrar perfiles de asignación con nombre. También puede transferir perfiles entre sistemas:

- Haga clic en **Import...** para importar un archivo de perfil desde el disco. Se aceptan tanto archivos XML de perfil de AetherSDR como archivos `.map` de SmartSDR. Después de importar, AetherSDR informa cuántas vinculaciones se importaron; haga clic en **Load** para aplicarlas.
- Haga clic en **Export...** para escribir las vinculaciones actuales en un archivo XML de perfil de AetherSDR. El diálogo de archivo se abre en el mismo directorio que usó por última vez para importaciones o exportaciones; el directorio se recuerda en la configuración `MidiImportExportPath`.

## Consejos

- Si desconecta y vuelve a conectar el controlador, haga clic en **Refresh** para repoblar la lista **Port:** antes de hacer clic en **Connect**.
- El estado del puerto y el indicador de actividad se actualizan en tiempo real. Confirme que el indicador de actividad muestra mensajes entrantes antes de cerrar el diálogo.
- El diálogo recuerda su tamaño y posición entre sesiones.
- Use **Manual…** cuando necesite una vinculación para un mensaje MIDI que no puede generar fácilmente con el controlador físico (por ejemplo, un evento de pitch-bend desde un dispositivo virtual).
- Al importar un perfil, las vinculaciones no se aplican hasta que haga clic en **Load**. Esto le permite revisar el resumen de importación antes de realizar cambios en su configuración actual.

## Solución de problemas

- **La lista de puertos está vacía después de conectar el controlador** — Haga clic en **Refresh** para volver a escanear. Si el puerto aún no aparece, verifique que el sistema operativo reconozca el dispositivo.
- **La reconexión automática no funciona en el próximo inicio** — Confirme que hizo clic en **Connect** y vio un estado conectado antes de marcar **Auto-connect on startup**. La configuración guarda el nombre del puerto abierto más recientemente; si el nombre del dispositivo cambió (por ejemplo, en un puerto USB diferente en algunos sistemas), seleccione el puerto correcto manualmente, conéctese nuevamente y vuelva a marcar **Auto-connect on startup**.
- **Un perfil importado no aparece en la tabla** — Haga clic en **Load** después de importar. La importación solo prepara las vinculaciones; no las aplica automáticamente.
- **Manual… abrió el editor pero la vinculación es incorrecta** — Use el botón ✎ por fila en la **Bindings table** para corregir el canal, el tipo de mensaje y el número de esa vinculación específica sin tener que recrearla.

## Relacionado

- [Conectar un controlador MIDI](connect-a-midi-controller.md)
- [Descripción general de MIDI Controller Mapping](../../features/midi-mapping/overview.md)
- [Registrar una nueva vinculación con el modo Learn](../../features/midi-mapping/record-a-new-binding-with-learn-mode.md)
- [Guardar la asignación actual como un perfil con nombre](../../features/midi-mapping/save-the-current-mapping-as-a-named-profile.md)
- Importar y exportar perfiles de asignación
- Disparadores para llave telegráfica y paletas CW
