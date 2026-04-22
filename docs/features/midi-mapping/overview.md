# Descripción general del mapeo de controladores MIDI

La función de mapeo de controladores MIDI le permite asignar controles físicos de un controlador MIDI — perillas, faders, botones — a parámetros de radio en AetherSDR. Abra el diálogo una vez para configurar su dispositivo y registrar las asignaciones; luego use perfiles con nombre para cambiar entre distribuciones de controlador.

## Antes de comenzar

- Su controlador MIDI debe estar conectado a su computadora y reconocido por el sistema operativo antes de que AetherSDR pueda listarlo.
- El soporte MIDI debe estar compilado en su versión de AetherSDR (`HAVE_MIDI`). Si `Settings > MIDI Mapping...` no aparece en el menú, su versión no incluye soporte MIDI.

## Cómo funciona

Abra el diálogo desde `Settings > MIDI Mapping...`. El diálogo está dividido en dos secciones: **MIDI Device** y **Parameter Bindings**.

**MIDI Device** se encarga de seleccionar y abrir el puerto de su controlador. Seleccione un puerto en el cuadro combinado `Port:` y haga clic en `Connect` para abrirlo. El indicador de estado del puerto, ubicado debajo del cuadro combinado, muestra `Connected: <port name>` o `Disconnected`. El indicador de actividad a su lado muestra el mensaje MIDI más reciente recibido (por ejemplo, `Ch 1 CC #7 = 64`), lo cual es útil para verificar que AetherSDR está recibiendo la señal de su controlador.

**Parameter Bindings** es donde se crean y administran las asignaciones entre los controles MIDI y los parámetros de radio. Use el cuadro combinado `Category` para reducir la lista de parámetros; luego seleccione un parámetro específico en el cuadro combinado `Parameter`. Haga clic en `Learn`, mueva el control físico en su controlador MIDI, y AetherSDR registrará la asignación automáticamente. Todas las asignaciones actuales aparecen en la tabla de asignaciones. Cada fila muestra el parámetro, la fuente MIDI, el canal y las opciones por asignación. Use perfiles con nombre para guardar y restaurar conjuntos completos de asignaciones.

## Qué hace cada control

### Sección MIDI Device

| Control | Tipo | Comportamiento | Configuración persistida |
|---|---|---|---|
| `Port:` | Cuadro combinado | Selecciona el dispositivo de entrada MIDI a utilizar. | `MidiPort` |
| `Refresh` | Botón | Vuelve a escanear los puertos MIDI disponibles y actualiza `Port:`. | — |
| `Connect` | Botón | Abre el puerto MIDI seleccionado. La etiqueta cambia a `Disconnect` cuando el puerto está abierto. | — |
| `Auto-connect on startup` | Casilla de verificación | Cuando está marcada, AetherSDR reabre el último puerto MIDI utilizado al iniciar. | `MidiAutoConnect` |
| Estado del puerto | Indicador | Muestra `Connected: <port name>` o `Disconnected`. | — |
| Indicador de actividad | Indicador | Muestra el mensaje MIDI más reciente recibido (canal, tipo, número, valor). | — |

### Sección Parameter Bindings

| Control | Tipo | Comportamiento | Configuración persistida |
|---|---|---|---|
| `Category` | Cuadro combinado | Filtra la lista `Parameter` por categoría de control (All, RX, TX, Phone/CW, EQ, Global). | — |
| `Parameter` | Cuadro combinado | Elige el parámetro de radio de destino para una nueva asignación. | — |
| `Learn` | Botón | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado. La etiqueta cambia a `Cancel Learn` mientras escucha. | — |
| Tabla de asignaciones | Lista | Muestra todas las asignaciones existentes. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminación por fila. | — |
| `Invert` | Casilla de verificación (por fila) | Invierte la dirección del control para esa asignación. | — |
| `Relative` | Casilla de verificación (por fila) | Trata el control como un encoder continuo en lugar de una fuente de valor absoluto. | — |
| `×` | Botón (por fila) | Elimina esa asignación. | — |
| `Clear All` | Botón | Elimina todas las asignaciones. | — |
| `Profile:` | Cuadro combinado | Selecciona o nombra un perfil de mapeo MIDI guardado. El campo es editable. | — |
| `Save` | Botón | Guarda las asignaciones actuales con el nombre que aparece en `Profile:`. | — |
| `Load` | Botón | Carga las asignaciones del perfil indicado en `Profile:`. | — |
| `Close` | Botón | Cierra el diálogo. | — |

## Consejos

- Use el indicador de actividad para confirmar que AetherSDR está recibiendo MIDI antes de intentar usar `Learn`. Si el indicador no se actualiza al mover un control, el puerto no está abierto o se ha seleccionado el puerto incorrecto.
- `Relative` debe habilitarse para encoders continuos (perillas sin topes físicos). Déjelo sin marcar para potenciómetros estándar y faders.
- Los nombres de perfil se ingresan directamente en el cuadro combinado `Profile:`. Escriba un nuevo nombre y haga clic en `Save` para crear un perfil; seleccione un nombre existente y haga clic en `Load` para restaurarlo.

## Temas relacionados

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Conectar automáticamente el controlador MIDI al iniciar](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Registrar una nueva asignación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Invertir una perilla o tratarla como encoder continuo](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Guardar el mapeo actual como perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado previamente](load-a-previously-saved-midi-profile.md)
