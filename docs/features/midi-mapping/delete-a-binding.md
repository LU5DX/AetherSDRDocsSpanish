# Asignación de controlador MIDI

El diálogo Asignación de controlador MIDI le permite configurar un controlador MIDI para usarlo con AetherSDR. Puede seleccionar un dispositivo, grabar asignaciones usando el modo Learn, ajustar el comportamiento por asignación y guardar o cargar perfiles de asignación.

## Abrir el diálogo

1. Vaya a `Settings > MIDI Mapping...`.

Se abre el diálogo, mostrando el estado actual del puerto MIDI y cualquier asignación existente.

## Seleccionar un dispositivo MIDI

1. En el cuadro combinado `Port:`, seleccione el dispositivo de entrada MIDI que desea usar.
2. Haga clic en `Refresh` para volver a escanear los puertos MIDI disponibles si su dispositivo no aparece en la lista.
3. Haga clic en `Connect` para abrir el puerto seleccionado. El texto del botón cambia a "Disconnect" cuando el puerto está abierto.
4. (Opcional) Marque `Auto-connect on startup` para reabrir este puerto automáticamente la próxima vez que inicie AetherSDR.

El indicador de estado del puerto muestra "Connected: [nombre del dispositivo]" con una etiqueta verde cuando el puerto está abierto, y "Disconnected" con una etiqueta gris cuando está cerrado.

## Grabar una nueva asignación con el modo Learn

1. En el cuadro combinado `Category`, seleccione la categoría de control para el parámetro que desea asignar.
2. En el cuadro combinado `Parameter`, seleccione el parámetro de destino para la nueva asignación.
3. Haga clic en `Learn`. El botón se resalta para indicar que está escuchando.
4. Mueva o presione el control en su dispositivo MIDI que desea asignar.

La asignación aparece en la tabla de asignaciones con el nombre del parámetro, la fuente MIDI y el canal.

### Nota sobre acciones momentáneas (Gate)

En v0.9.7, se agregaron tres nuevas acciones momentáneas (Gate) en la categoría Phone/CW:

- `Trigger straight key` (id: `cwkey`)
- `Trigger CW Left Paddle` (id: `cwdit`)
- `Trigger CW Right Paddle` (id: `cwdah`)

Los IDs heredados con puntos (`cw.key`, `cw.dit`, `cw.dah`) se migran automáticamente al leer.

## Ajustar el comportamiento por asignación

Cada fila de asignación en la tabla tiene dos controles opcionales:

- **Invert**: Marque esta casilla para invertir la dirección del control para esa fila. Por ejemplo, si girar una perilla en sentido horario normalmente aumenta un valor, marcar Invert hace que disminuya el valor.
- **Relative**: Marque esta casilla para tratar el control como un codificador sin fin. Úselo para codificadores rotativos que no tienen topes físicos y envían cambios de posición relativos.

## Eliminar una asignación

### Eliminar una sola asignación

1. En la tabla de asignaciones, localice la fila de la asignación que desea eliminar.
2. Haga clic en `×` en la columna más a la derecha de esa fila.

La fila se elimina de inmediato. El cambio se guarda automáticamente.

### Eliminar todas las asignaciones a la vez

1. Haga clic en `Clear All`.

Se eliminan todas las filas de la tabla de asignaciones. El cambio se guarda automáticamente.

## Guardar la asignación actual como un perfil con nombre

1. En el cuadro combinado `Profile:`, escriba un nombre para su perfil.
2. Haga clic en `Save`.

El perfil se guarda y aparece en la lista de perfiles para uso futuro.

## Cargar un perfil MIDI guardado previamente

1. En el cuadro combinado `Profile:`, seleccione el perfil que desea cargar.
2. Haga clic en `Load`.

Las asignaciones del perfil seleccionado reemplazan las asignaciones actuales en la tabla.

## Monitoreo de actividad

El indicador de actividad muestra el mensaje MIDI más reciente recibido, mostrado en una fuente monoespaciada. Úselo para verificar que su controlador MIDI esté enviando mensajes y que el puerto funcione correctamente.

## Qué hace cada control

| Control                | Descripción                                     | Notas |
|------------------------|-------------------------------------------------|-------|
| `Port:`                | Selecciona el dispositivo de entrada MIDI.      |       |
| `Refresh`              | Vuelve a escanear los puertos MIDI disponibles. |       |
| `Connect`              | Abre/cierra el puerto MIDI seleccionado.        |       |
| `Auto-connect on startup` | Reabre el puerto MIDI al iniciar.           |       |
| `Category`             | Filtra el cuadro de parámetros por categoría de control. |       |
| `Parameter`            | Elige el parámetro de destino para una nueva asignación. |       |
| `Learn`                | Comienza a escuchar el próximo mensaje MIDI.    |       |
| Tabla de asignaciones  | Muestra las asignaciones existentes con controles por fila. | Columnas: Parámetro, Fuente MIDI, Canal, Invertir, Relativo, (eliminar). |
| `Invert` (por fila)    | Invierte la dirección del control para la fila. |       |
| `Relative` (por fila)  | Trata el control como un codificador sin fin.   |       |
| `×` (eliminar fila)    | Elimina esa asignación.                         |       |
| `Clear All`            | Elimina todas las asignaciones.                 |       |
| `Profile:`             | Selecciona un perfil de asignación MIDI guardado.|       |
| `Save`                 | Guarda las asignaciones actuales como un perfil.|       |
| `Load`                 | Carga el perfil seleccionado.                    |       |
| `Close`                | Cierra el diálogo.                              |       |

## Consejos

- Si elimina una asignación por error, puede restaurarla cargando un perfil guardado previamente.
- Antes de usar `Clear All`, considere guardar sus asignaciones actuales como un perfil primero.
- El indicador de actividad es útil para diagnosticar problemas de conexión: si mueve un control y no ve actividad, verifique que el puerto correcto esté seleccionado y conectado.

## Relacionado

- [Eliminar una asignación](#eliminar-una-asignación)
- [Grabar una nueva asignación con el modo Learn](#grabar-una-nueva-asignación-con-el-modo-learn)
- [Guardar la asignación actual como un perfil con nombre](#guardar-la-asignación-actual-como-un-perfil-con-nombre)
- [Cargar un perfil MIDI guardado previamente](#cargar-un-perfil-midi-guardado-previamente)
