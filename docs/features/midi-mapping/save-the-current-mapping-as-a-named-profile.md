# Guardar la Asignación Actual como un Perfil con Nombre

Guarde sus asignaciones MIDI actuales con un nombre para poder recuperarlas más tarde o cambiar entre diseños de controlador sin tener que volver a aprender cada asignación.

## Antes de comenzar

- Debe existir al menos una asignación en la tabla de Asignaciones. Se puede guardar una asignación vacía, pero no es útil.
- Abra `Settings > MIDI Mapping...` para acceder al diálogo de Asignación de Controlador MIDI.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Confirme que la tabla de Asignaciones muestra las asignaciones que desea guardar.
3. En el campo **Profile:**, escriba un nombre para el perfil. El campo acepta texto libre; también muestra los nombres de perfiles existentes en su lista desplegable si se ha guardado alguno anteriormente.
4. Haga clic en **Save**.

El perfil se guarda inmediatamente. La lista desplegable **Profile:** se actualiza para incluir el nuevo nombre.

## Qué hace cada control

| Control | Qué hace | Clave de configuración |
|---|---|---|
| **Port:** | Selecciona el dispositivo de entrada MIDI. | `MidiPort` |
| **Refresh** | Vuelve a escanear los puertos MIDI disponibles. | — |
| **Connect** | Abre/cierra el puerto MIDI seleccionado. | — |
| **Auto-connect on startup** | Vuelve a abrir el puerto MIDI al iniciar. | `MidiAutoConnect` |
| **Category** | Filtra el combo de parámetros a una categoría de control. Categorías disponibles: All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency. | — |
| **Parameter** | Elige el parámetro objetivo para una nueva asignación. En v26.5.1, hay tres nuevas acciones momentáneas (Gate) disponibles en la categoría Phone/CW: "Trigger straight key" (id: cwkey), "Trigger CW Left Paddle" (id: cwdit), "Trigger CW Right Paddle" (id: cwdah). Los ID punteados heredados cw.key/cw.dit/cw.dah se migran automáticamente al leerlos. | — |
| **Learn** | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado. | — |
| **Bindings table** | Muestra las asignaciones existentes con controles por fila de Invert, Relative y eliminar. Columnas: Parameter, MIDI Source, Channel, Invert, Relative, (delete). | — |
| **Invert** | Invierte la dirección del control para la fila. | — |
| **Relative** | Trata el control como un codificador sin fin. | — |
| **× (delete row)** | Elimina esa asignación. | — |
| **Clear All** | Elimina todas las asignaciones. | — |
| **Profile:** | Cuadro combinado editable. Escriba un nuevo nombre para crear un perfil, o seleccione un nombre existente de la lista desplegable para sobrescribirlo. | — |
| **Save** | Guarda las asignaciones actuales con el nombre mostrado en **Profile:**. No hace nada si el campo está vacío. | — |
| **Load** | Reemplaza las asignaciones actuales con las almacenadas bajo el nombre de perfil seleccionado. | — |
| **Close** | Cierra el diálogo. | — |

## Indicadores

| Indicador | Significado |
|---|---|
| **Port status** | Muestra "Opened" o "Closed" para indicar si el puerto MIDI está actualmente abierto. |
| **Activity indicator** | Muestra el mensaje MIDI más reciente recibido. |

## Consejos

- Escribir un nombre que ya existe en **Profile:** y hacer clic en **Save** sobrescribe ese perfil sin una solicitud de confirmación.
- Para mantener las asignaciones de diferentes controladores separadas, use un nombre descriptivo como el modelo del controlador o el caso de uso.

## Solución de problemas

- **Hacer clic en Save no hace nada** — El campo **Profile:** está vacío o contiene solo espacios. Escriba un nombre primero.
- **Un nombre de perfil no aparece en la lista desplegable después de guardar** — Haga clic en cualquier lugar para cerrar la lista desplegable y vuelva a abrirla; la lista se actualiza después de cada guardado.

## Relacionado

- [Load a previously saved MIDI profile](load-a-previously-saved-midi-profile.md)
- [Record a new binding with Learn mode](record-a-new-binding-with-learn-mode.md)
- [Delete a binding](delete-a-binding.md)
- [MIDI Controller Mapping overview](overview.md)
