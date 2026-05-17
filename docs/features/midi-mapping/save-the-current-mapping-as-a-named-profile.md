# Guardar la Asignación Actual como un Perfil Nombrado

Guarde sus asignaciones MIDI actuales con un nombre para poder recuperarlas más tarde o cambiar entre diseños de controlador sin tener que re-aprender cada asignación.

## Antes de comenzar

- Debe existir al menos una asignación en la tabla de Asignaciones. Se puede guardar una asignación vacía, pero no es útil.
- Abra `Settings > MIDI Mapping...` para acceder al diálogo de Asignación de Controlador MIDI.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Confirme que la tabla de Asignaciones muestra las asignaciones que desea guardar.
3. En el campo **Profile:**, escriba un nombre para el perfil. El campo acepta texto libre; también muestra los nombres de perfiles existentes en su lista desplegable si se han guardado previamente.
4. Haga clic en **Save**.

El perfil se guarda inmediatamente. La lista desplegable **Profile:** se actualiza para incluir el nuevo nombre.

## Qué hace cada control

| Control | Qué hace | Clave de configuración |
|---|---|---|
| **Port:** | Selecciona el dispositivo de entrada MIDI. | `MidiPort` |
| **Refresh** | Vuelve a escanear los puertos MIDI disponibles. | — |
| **Connect** | Abre/cierra el puerto MIDI seleccionado. | — |
| **Auto-connect on startup** | Reabre el puerto MIDI al iniciar. | `MidiAutoConnect` |
| **Category** | Filtra el combo de parámetros a una categoría de control. Categorías disponibles: All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display, Frequency. | — |
| **Parameter** | Elige el parámetro destino para una nueva asignación. En v26.5.2.1, hay tres acciones momentáneas (Gate) disponibles en la categoría Phone/CW: "Trigger straight key" (id: cwkey), "Trigger CW Left Paddle" (id: cwdit), "Trigger CW Right Paddle" (id: cwdah). Las IDs con puntos heredadas cw.key/cw.dit/cw.dah se migran automáticamente al leer. | — |
| **Learn** | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado. | — |
| **Bindings table** | Muestra las asignaciones existentes con controles por fila para Invert, Relative y eliminar. Columnas: Parameter, MIDI Source, Channel, Invert, Relative, (eliminar). | — |
| **Invert** | Invierte la dirección de control para la fila. | — |
| **Relative** | Trata el control como un codificador sin fin. | — |
| **× (delete row)** | Elimina esa asignación. | — |
| **Clear All** | Elimina todas las asignaciones. | — |
| **Profile:** | Cuadro combinado editable. Escriba un nombre nuevo para crear un perfil, o seleccione un nombre existente de la lista desplegable para sobrescribirlo. | — |
| **Save** | Guarda las asignaciones actuales con el nombre mostrado en **Profile:**. No hace nada si el campo está vacío. | — |
| **Load** | Reemplaza las asignaciones actuales con las almacenadas bajo el nombre del perfil seleccionado. | — |
| **Close** | Cierra el diálogo. | — |

## Indicadores

| Indicador | Significado |
|---|---|
| **Port status** | Muestra "Opened" o "Closed" para indicar si el puerto MIDI está actualmente abierto. |
| **Activity indicator** | Muestra el mensaje MIDI más reciente recibido. |

## Consejos

- Escribir un nombre que ya existe en **Profile:** y hacer clic en **Save** sobrescribe ese perfil sin un aviso de confirmación.
- Para mantener asignaciones separadas para diferentes controladores, use un nombre descriptivo como el modelo del controlador o el caso de uso.
- El diálogo recuerda su posición y tamaño de ventana entre sesiones.

## Solución de problemas

- **Al hacer clic en Save no sucede nada** — El campo **Profile:** está vacío o contiene solo espacios. Escriba un nombre primero.
- **Un nombre de perfil no aparece en la lista desplegable después de guardar** — Haga clic en cualquier lugar para cerrar la lista desplegable y vuélvala a abrir; la lista se actualiza después de cada guardado.

## Relacionado

- [Cargar un perfil MIDI previamente guardado](load-a-previously-saved-midi-profile.md)
- [Grabar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Visión general de la Asignación de Controlador MIDI](overview.md)
