# Registrar un nuevo enlace con el modo Learn

Use el modo Learn para asignar un control MIDI físico — un mando, fader o botón — a un parámetro de AetherSDR moviendo el control mientras AetherSDR escucha. Esto es más rápido y confiable que ingresar manualmente los valores de canal y número MIDI.

## Antes de comenzar

- Debe haber un controlador MIDI conectado a su computadora y visible para el sistema operativo.
- El puerto MIDI debe estar abierto en AetherSDR. Si no lo está, consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md).

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Category**, seleccione la categoría que contiene el parámetro que desea enlazar (por ejemplo, `RX`, `TX` o `All`).
3. En el cuadro combinado **Parameter**, seleccione el parámetro de destino.
4. Haga clic en `Learn`. La etiqueta del botón cambia a `Cancel Learn`, lo que indica que AetherSDR está esperando un mensaje MIDI.
5. Mueva el mando, fader o botón de su controlador que desea asignar.
6. AetherSDR captura el mensaje y agrega una nueva fila a la tabla **Bindings**. La etiqueta del botón vuelve a `Learn`.
7. Si desea cancelar sin registrar, haga clic en `Cancel Learn` en lugar de mover un control.
8. Repita los pasos 2–6 para cada enlace adicional.
9. Haga clic en `Close` cuando termine. Los enlaces se guardan automáticamente al completarse el modo Learn.

## Función de cada control

| Control | Descripción |
|---|---|
| Cuadro combinado **Category** | Filtra la lista **Parameter** por categoría de control. Las opciones incluyen `All`, `RX`, `TX`, `Phone/CW`, `EQ` y `Global`. |
| Cuadro combinado **Parameter** | Selecciona el parámetro de AetherSDR al que se enlazará la próxima captura de Learn. |
| `Learn` | Comienza a escuchar el próximo mensaje MIDI entrante y lo enlaza al parámetro seleccionado. Hacer clic nuevamente mientras escucha cancela la operación. |
| Tabla **Bindings** | Muestra todos los enlaces registrados. Columnas: Parameter, MIDI Source, Channel, Invert, Relative y un botón de eliminar. |
| Casilla **Invert** (por fila) | Invierte la dirección del control para ese enlace. |
| Casilla **Relative** (por fila) | Trata el control como un encoder continuo en lugar de una fuente de valor absoluto. |
| Indicador de actividad | Muestra el mensaje MIDI más reciente recibido (canal, tipo, número y valor). Es útil para confirmar que el controlador está enviando datos antes de hacer clic en `Learn`. |

## Sugerencias

- Observe el indicador de actividad mientras mueve un control antes de hacer clic en `Learn`. Si no aparece nada, el puerto no está abierto o el controlador no está enviando datos.
- Si el parámetro incorrecto está seleccionado cuando mueve el control, haga clic en `Cancel Learn`, corrija la selección en **Parameter** y haga clic en `Learn` nuevamente.
- Después de registrar varios enlaces, use `Save` con un nombre en el campo **Profile:** para conservar el mapeo. Consulte [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md).

## Solución de problemas

- **`Learn` se agota el tiempo o el botón permanece con la etiqueta `Cancel Learn` después de mover un control** — Es posible que el puerto MIDI no esté abierto. Verifique el indicador de estado del puerto; si muestra `Closed`, haga clic en `Connect` y vuelva a intentar Learn.
- **El indicador de actividad muestra un mensaje pero no se crea ningún enlace** — Es posible que el campo de parámetro haya estado vacío. Asegúrese de que haya un parámetro seleccionado en el cuadro combinado **Parameter** antes de hacer clic en `Learn`.
- **El controlador envía datos pero el indicador de actividad está en blanco** — Es posible que el puerto seleccionado en el cuadro combinado **Port:** no coincida con el controlador. Haga clic en `Refresh` para reescanear, seleccione el puerto correcto y haga clic en `Connect`.

## Relacionados

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Invertir un mando o tratarlo como un encoder continuo](invert-a-knob-or-treat-it-as-an-endless-encoder.md)
- [Eliminar un enlace](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado anteriormente](load-a-previously-saved-midi-profile.md)
- [Conectar automáticamente el controlador MIDI al inicio](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
