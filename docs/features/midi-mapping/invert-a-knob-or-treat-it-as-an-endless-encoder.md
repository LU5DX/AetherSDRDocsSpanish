# Invertir un mando o tratarlo como un codificador sin fin

Después de crear un enlace MIDI, puede invertir su dirección con Invert o indicar a AetherSDR que trate el control como un codificador sin fin con Relative. Ambas opciones se configuran por enlace en la tabla de Bindings.

## Antes de comenzar

- Debe haber un controlador MIDI conectado y al menos un enlace existente. Consulte [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md) y [Record a new binding with Learn mode](record-a-new-binding-with-learn-mode.md).
- Abra `Settings > MIDI Mapping...` para acceder al diálogo MIDI Controller Mapping.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Localice el enlace que desea cambiar en la tabla de Bindings.
3. Para invertir la dirección del control, marque la casilla Invert en la fila de ese enlace.
4. Para tratar el control como un codificador sin fin, marque la casilla Relative en la fila de ese enlace.
5. Cualquiera de las casillas puede marcarse o desmarcarse de forma independiente. Los cambios se aplican de inmediato.
6. Haga clic en Close cuando haya terminado.

## Qué hace cada control

| Control          | Columna en la tabla de Bindings                                                                    | Comportamiento                                                                                                                                                           |
|------------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Invert           | Invert                                                                                             | Invierte la dirección del control para ese enlace. Girar en el sentido de las agujas del reloj para disminuir, en sentido contrario para aumentar, o viceversa.          |
| Relative         | Relative                                                                                           | Trata el control como un codificador sin fin. Úselo cuando su mando de hardware envíe valores incrementales (relativos) en lugar de posiciones absolutas (0–127).         |
| Manual…          | Abre un diálogo para escribir el canal, tipo de mensaje y número de un enlace en lugar de usar Learn mode. | Nuevo en v26.8.4 (#4760). Abre el mismo editor manual que usa el botón de edición de cada fila.                                                                          |
| ✎ (editar enlace) | Abre el editor manual para corregir el canal, tipo y número de este enlace.                        | Nuevo en v26.8.4 (#4760).                                                                                                                                                |
| Import...        | Importa un archivo de perfil al almacén: perfil XML de AetherSDR o archivo ".map" de SmartSDR.     | Nuevo en v26.8.4. Informa cuántos enlaces se importaron y permite al usuario hacer clic en Load para aplicarlos.                                                          |
| Export...        | Exporta los enlaces actuales como archivo XML de perfil de AetherSDR.                              | Nuevo en v26.8.4. El directorio recordado se conserva en MidiImportExportPath.                                                                                           |
| Port:            | Cuadro combinado                                                                                   | Selecciona el dispositivo de entrada MIDI.                                                                                                                               |
| Refresh          | Botón                                                                                              | Reescanea los puertos MIDI disponibles.                                                                                                                                  |
| Connect          | Botón                                                                                              | Abre/cierra el puerto MIDI seleccionado.                                                                                                                                 |
| Auto-connect on startup | Casilla de verificación                                                                      | Reabre el puerto MIDI al iniciar.                                                                                                                                        |
| Category         | Cuadro combinado                                                                                   | Filtra el cuadro de parámetros por categoría de control.                                                                                                                 |
| Parameter        | Cuadro combinado                                                                                   | Elige el parámetro de destino para un nuevo enlace. En v0.9.7, se agregaron tres nuevas acciones momentáneas (Gate) en la categoría Phone/CW: 'Trigger straight key' (id: cwkey), 'Trigger CW Left Paddle' (id: cwdit), 'Trigger CW Right Paddle' (id: cwdah). Los IDs heredados con puntos cw.key/cw.dit/cw.dah se migran automáticamente al leerlos. |
| Learn            | Botón                                                                                              | Comienza a escuchar el siguiente mensaje MIDI y lo enlaza al parámetro seleccionado.                                                                                     |
| Bindings table   | Lista                                                                                              | Muestra los enlaces existentes con controles por fila de Invert, Relative, edición (✎) y eliminación. Columnas: Parameter, MIDI Source, Channel, Invert, Relative, (edit), (delete). |
| × (eliminar fila) | Botón                                                                                             | Elimina ese enlace.                                                                                                                                                      |
| Clear All        | Botón                                                                                              | Elimina todos los enlaces.                                                                                                                                               |
| Profile:         | Cuadro combinado                                                                                   | Selecciona un perfil de mapeo MIDI guardado.                                                                                                                             |
| Save             | Botón                                                                                              | Guarda los enlaces actuales como perfil.                                                                                                                                 |
| Load             | Botón                                                                                              | Carga el perfil seleccionado.                                                                                                                                            |
| Close            | Botón                                                                                              | Cierra el diálogo.                                                                                                                                                       |
| Port status      | Indicador                                                                                          | Muestra si el puerto MIDI está actualmente abierto (Opened/Closed).                                                                                                      |
| Activity indicator | Indicador                                                                                        | Muestra el mensaje MIDI más reciente recibido.                                                                                                                           |

## Filtro de categoría

El cuadro combinado Category encima de la tabla de Bindings filtra el cuadro combinado Parameter a una categoría de control específica. En v26.6.1, las categorías disponibles son:

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

Seleccione una categoría para reducir la lista de parámetros que se muestran al crear un nuevo enlace.

## Nuevas acciones momentáneas de activación de CW

En v26.6.1, la categoría Phone/CW incluye tres nuevas acciones momentáneas (Gate) para el tecleo de CW:

- **Trigger straight key** (id: cwkey) — Simula la pulsación de una llave recta.
- **Trigger CW Left Paddle** (id: cwdit) — Simula la pulsación de la paleta izquierda (dit).
- **Trigger CW Right Paddle** (id: cwdah) — Simula la pulsación de la paleta derecha (dah).

Los IDs heredados con puntos (cw.key, cw.dit, cw.dah) se migran automáticamente al nuevo formato al cargar perfiles antiguos.

## Consejos

- Use Relative cuando su mando envíe pequeños valores de incremento/decremento en lugar de una posición absoluta. Si un mando salta de forma errática al girarlo, activar Relative suele corregirlo.
- Invert y Relative pueden combinarse en el mismo enlace. Por ejemplo, un codificador Relative que incrementa en la dirección equivocada puede tener ambas opciones marcadas.
- Los cambios en Invert y Relative se guardan automáticamente al guardar un perfil. Use Save en Profile: para conservarlos.
- Las acciones de activación de CW son momentáneas: se activan mientras el control MIDI está pulsado y se desactivan al soltarlo.

## Solución de problemas

- **Al marcar Relative, un mando deja de responder** — El mando puede estar enviando valores absolutos (0–127). Desmarque Relative y deje el enlace en modo absoluto.
- **El control sigue moviéndose en la dirección equivocada después de marcar Invert** — Verifique que haya marcado Invert en la fila correcta. Cada fila de enlace tiene su propia casilla Invert; desplácese horizontalmente si la columna no está visible.

## Relacionados

- [Record a new binding with Learn mode](record-a-new-binding-with-learn-mode.md)
- [Delete a binding](delete-a-binding.md)
- [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md)
- [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md)
