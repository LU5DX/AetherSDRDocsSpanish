# Mapeo de controlador MIDI

El diálogo de Mapeo de controlador MIDI le permite configurar un controlador MIDI para usarlo con AetherSDR. Puede seleccionar un dispositivo, registrar asignaciones usando el modo Learn o agregarlas manualmente, ajustar el comportamiento de cada asignación, y guardar, cargar, importar o exportar perfiles de mapeo.

## Abrir el diálogo

1. Vaya a `Settings > MIDI Mapping...`.

El diálogo se abre mostrando el estado actual del puerto MIDI y las asignaciones existentes.

## Seleccionar un dispositivo MIDI

1. En el cuadro combinado `Port:`, seleccione el dispositivo de entrada MIDI que desea usar.
2. Haga clic en `Refresh` para volver a escanear los puertos MIDI disponibles si su dispositivo no aparece en la lista.
3. Haga clic en `Connect` para abrir el puerto seleccionado. El texto del botón cambia a "Disconnect" cuando el puerto está abierto.
4. (Opcional) Marque `Auto-connect on startup` para reabrir automáticamente este puerto la próxima vez que inicie AetherSDR.

El indicador de estado del puerto muestra "Connected: [nombre del dispositivo]" con una etiqueta verde cuando el puerto está abierto, y "Disconnected" con una etiqueta gris cuando está cerrado.

## Registrar una nueva asignación con el modo Learn

1. En el cuadro combinado `Category`, seleccione la categoría de control para el parámetro que desea mapear.
2. En el cuadro combinado `Parameter`, seleccione el parámetro de destino para la nueva asignación.
3. Haga clic en `Learn`. El botón se resalta para indicar que está escuchando.
4. Mueva o presione el control en su dispositivo MIDI que desea mapear.

La asignación aparece en la tabla de asignaciones con el nombre del parámetro, la fuente MIDI y el canal.

### Nota sobre acciones momentáneas (Gate)

En la v0.9.7 se agregaron tres nuevas acciones momentáneas (Gate) en la categoría Phone/CW:

- `Trigger straight key` (id: `cwkey`)
- `Trigger CW Left Paddle` (id: `cwdit`)
- `Trigger CW Right Paddle` (id: `cwdah`)

Los IDs heredados con puntos (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al leerlos.

## Agregar una asignación manualmente

En lugar de usar el modo Learn, puede escribir los detalles MIDI de una asignación directamente.

1. Seleccione la `Category` y el `Parameter` como se describió anteriormente.
2. Haga clic en `Manual…`. Se abre un diálogo donde puede ingresar el canal, tipo de mensaje y número de la asignación.
3. Ingrese los valores requeridos y confirme.

La asignación aparece en la tabla. También puede reabrir este editor para una asignación existente haciendo clic en el botón `✎` en su fila.

## Ajustar el comportamiento de cada asignación

Cada fila de asignación en la tabla tiene dos controles opcionales:

- **Invert**: Marque esta casilla para invertir la dirección del control en esa fila. Por ejemplo, si girar una perilla en sentido horario normalmente aumenta un valor, marcar Invert hace que disminuya el valor en su lugar.
- **Relative**: Marque esta casilla para tratar el control como un codificador sin fin. Úselo para codificadores rotatorios que no tienen topes físicos y envían cambios de posición relativos.

## Editar una asignación existente

1. En la tabla de asignaciones, localice la fila de la asignación que desea corregir.
2. Haga clic en `✎` en esa fila.
3. Ajuste el canal, tipo de mensaje o número en el editor manual que se abre.
4. Confirme sus cambios.

## Eliminar una asignación

### Eliminar una sola asignación

1. En la tabla de asignaciones, localice la fila de la asignación que desea eliminar.
2. Haga clic en `×` en la columna más a la derecha de esa fila.

La fila se elimina inmediatamente. El cambio se guarda automáticamente.

### Eliminar todas las asignaciones a la vez

1. Haga clic en `Clear All`.

Todas las filas de la tabla de asignaciones se eliminan. El cambio se guarda automáticamente.

## Guardar el mapeo actual como un perfil con nombre

1. En el cuadro combinado `Profile:`, escriba un nombre para su perfil.
2. Haga clic en `Save`.

El perfil se guarda y aparece en la lista de perfiles para uso futuro.

## Cargar un perfil MIDI previamente guardado

1. En el cuadro combinado `Profile:`, seleccione el perfil que desea cargar.
2. Haga clic en `Load`.

Las asignaciones del perfil seleccionado reemplazan las asignaciones actuales en la tabla.

## Importar un perfil desde un archivo

1. Haga clic en `Import...`.
2. Elija un archivo de perfil. Puede importar un archivo XML de perfil de AetherSDR o un archivo `.map` de SmartSDR.

AetherSDR informa cuántas asignaciones se importaron. Haga clic en `Load` para aplicar las asignaciones importadas.

## Exportar las asignaciones actuales a un archivo

1. Haga clic en `Export...`.
2. Elija una ubicación y un nombre de archivo para el perfil exportado.

Las asignaciones actuales se escriben como un archivo XML de perfil de AetherSDR. El directorio que elija se recuerda para la próxima importación o exportación.

## Monitoreo de actividad

El indicador de actividad muestra el mensaje MIDI más reciente recibido, mostrado en una fuente monoespaciada. Úselo para verificar que su controlador MIDI está enviando mensajes y que el puerto funciona correctamente.

## Qué hace cada control

| Control                | Descripción                                     | Notas |
|------------------------|-------------------------------------------------|-------|
| `Port:`                | Selecciona el dispositivo de entrada MIDI.      |       |
| `Refresh`              | Vuelve a escanear los puertos MIDI disponibles. |       |
| `Connect`              | Abre/cierra el puerto MIDI seleccionado.        |       |
| `Auto-connect on startup` | Reabre el puerto MIDI al iniciar.            |       |
| `Category`             | Filtra el cuadro de parámetros por categoría de control. |       |
| `Parameter`            | Elige el parámetro de destino para una nueva asignación. |       |
| `Learn`                | Comienza a escuchar el siguiente mensaje MIDI.  |       |
| `Manual…`              | Abre un diálogo para escribir el canal, tipo de mensaje y número de una asignación. | Nuevo en v26.8.4. |
| Tabla de asignaciones  | Muestra las asignaciones existentes con controles por fila. | Columnas: Parameter, MIDI Source, Channel, Invert, Relative, (edit), (delete). |
| `✎` (editar asignación) | Abre el editor manual para corregir el canal, tipo y número de esta asignación. | Nuevo en v26.8.4. |
| `Invert` (por fila)    | Invierte la dirección del control para la fila. |       |
| `Relative` (por fila)  | Trata el control como un codificador sin fin.   |       |
| `×` (eliminar fila)    | Elimina esa asignación.                         |       |
| `Clear All`            | Elimina todas las asignaciones.                 |       |
| `Profile:`             | Selecciona un perfil de mapeo MIDI guardado.    |       |
| `Save`                 | Guarda las asignaciones actuales como un perfil.|       |
| `Load`                 | Carga el perfil seleccionado.                   |       |
| `Import...`            | Importa un archivo de perfil (XML de AetherSDR o `.map` de SmartSDR). | Nuevo en v26.8.4. |
| `Export...`            | Exporta las asignaciones actuales como un archivo XML de perfil de AetherSDR. | Nuevo en v26.8.4. |
| `Close`                | Cierra el diálogo.                              |       |

## Consejos

- Si elimina una asignación por error, puede restaurarla cargando un perfil guardado previamente.
- Antes de usar `Clear All`, considere guardar sus asignaciones actuales como un perfil primero.
- Use `Import...` para traer asignaciones desde SmartSDR si está migrando desde ese software.
- El indicador de actividad es útil para diagnosticar problemas de conexión: si mueve un control y no ve actividad, verifique que el puerto correcto esté seleccionado y conectado.

## Relacionado

- [Registrar una nueva asignación con el modo Learn](#record-a-new-binding-with-learn-mode)
- [Agregar una asignación manualmente](#add-a-binding-manually)
- [Eliminar una asignación](#delete-a-binding)
- [Guardar el mapeo actual como un perfil con nombre](#save-the-current-mapping-as-a-named-profile)
- [Cargar un perfil MIDI previamente guardado](#load-a-previously-saved-midi-profile)
