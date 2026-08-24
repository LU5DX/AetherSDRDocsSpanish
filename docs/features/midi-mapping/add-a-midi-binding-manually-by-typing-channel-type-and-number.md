# Agregar un enlace MIDI manualmente escribiendo canal, tipo y número

Esta página le muestra cómo crear un enlace MIDI en AetherSDR escribiendo directamente el canal, tipo de mensaje y número, en lugar de usar el modo Learn. Esto es útil cuando conoce los detalles exactos del mensaje MIDI de su controlador y desea agregar un enlace sin tener que mover físicamente una perilla o botón.

## Antes de comenzar

- Su controlador MIDI debe estar conectado a su computadora.
- Abra el diálogo MIDI Controller Mapping: `Settings > MIDI Mapping...`
- Debe haber un puerto seleccionado y conectado (consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)).

## Pasos

1. En el cuadro combinado **Parameter**, seleccione el parámetro objetivo para el nuevo enlace. Opcionalmente, use el cuadro combinado **Category** para filtrar la lista (p. ej., `RX`, `TX`, `Phone/CW`).
2. Haga clic en **Manual…** . Se abre el mismo editor que usa el botón de edición por fila (✎).
3. Escriba el canal MIDI, tipo de mensaje y número para el enlace.
4. Confirme el diálogo para agregar el enlace a la tabla.

El nuevo enlace aparece en la **Bindings table** con su parámetro, fuente MIDI y canal.

## Qué hace cada control

| Control | Descripción | Configuración persistida |
|---|---|---|
| **Port:** | Selecciona el dispositivo de entrada MIDI. | `MidiPort` |
| **Refresh** | Vuelve a escanear los puertos MIDI disponibles. | — |
| **Connect** | Abre o cierra el puerto MIDI seleccionado. | — |
| **Auto-connect on startup** | Reabre el puerto MIDI cuando AetherSDR se inicia. | `MidiAutoConnect` |
| **Category** | Filtra la lista de parámetros por categoría de control. | — |
| **Parameter** | Elige el parámetro objetivo para un nuevo enlace. | — |
| **Learn** | Comienza a escuchar el siguiente mensaje MIDI y lo enlaza al parámetro seleccionado. | — |
| **Manual…** | Abre un diálogo para escribir el canal, tipo de mensaje y número de un enlace en lugar de usar el modo Learn. Nuevo en v26.8.4. | — |
| **Bindings table** | Muestra los enlaces existentes con controles por fila: Invert, Relative, editar (✎) y eliminar (×). Columnas: Parameter, MIDI Source, Channel, Invert, Relative. | — |
| **Invert** | Invierte la dirección del control para la fila. | — |
| **Relative** | Trata el control como un codificador sin fin. | — |
| **Clear All** | Elimina todos los enlaces. | — |

## Consejos

- El botón **Manual…** es el mismo editor que usa el botón de edición por fila (✎), por lo que puede corregir un enlace de la misma manera en que lo creó.
- La entrada manual es útil cuando conoce el mensaje MIDI exacto que envía su controlador y no desea arriesgarse a una captura incorrecta con Learn.

## Relacionados

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Grabar un nuevo enlace con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Editar el canal, tipo y número de un enlace existente](edit-an-existing-binding-s-channel-type-and-number.md)
- [Eliminar un enlace](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado previamente](load-a-previously-saved-midi-profile.md)
