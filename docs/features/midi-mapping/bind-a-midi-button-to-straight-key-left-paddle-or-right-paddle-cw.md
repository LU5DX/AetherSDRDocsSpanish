# Vincular un Botón MIDI a una Llave Telegráfica Directa, una Paleta Izquierda o una Paleta Derecha (CW)

Utilice esta página para asignar un botón físico de su controlador MIDI a las entradas de llave telegráfica directa, paleta izquierda o paleta derecha (CW) de su FLEX-8600. Una vez vinculado, al presionar ese botón se activa la acción de manipulación correspondiente como un evento momentáneo (gate).

## Antes de comenzar

- Su controlador MIDI está conectado a la computadora y reconocido por el sistema operativo.
- AetherSDR fue compilado con soporte MIDI (`HAVE_MIDI`).
- El diálogo de Mapeo MIDI no está ya en modo Aprender de una sesión anterior.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Port:**, seleccione su controlador MIDI de la lista. Si no aparece, haga clic en Refresh.
3. Haga clic en Connect. El indicador de estado cambia para mostrar que el puerto está abierto.
4. En el cuadro combinado **Category**, seleccione `Phone/CW`.
5. En el cuadro combinado **Parameter**, seleccione una de las siguientes opciones:
   - `Trigger straight key` — envía una pulsación de llave directa
   - `Trigger CW Left Paddle` — envía un evento de paleta izquierda (dit)
   - `Trigger CW Right Paddle` — envía un evento de paleta derecha (dah)
6. Haga clic en Learn. La etiqueta del botón cambia a `Cancel Learn`.
7. Presione y mantenga presionado el botón físico de su controlador MIDI que desea vincular. AetherSDR detecta el mensaje MIDI y completa la vinculación automáticamente.
8. Confirme que aparece una nueva fila en la tabla Bindings, mostrando el nombre del parámetro, la fuente MIDI y el canal.
9. Repita los pasos 5 a 8 para cada entrada CW adicional que desee vincular.
10. Haga clic en Close.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Port: | Cuadro combinado | Selecciona el dispositivo de entrada MIDI | `MidiPort` |
| Refresh | Botón | Vuelve a escanear los puertos MIDI disponibles | — |
| Connect | Botón | Abre o cierra el puerto MIDI seleccionado | — |
| Auto-connect on startup | Casilla de verificación | Vuelve a abrir el puerto MIDI automáticamente en el próximo inicio | `MidiAutoConnect` |
| Category | Cuadro combinado | Filtra la lista de Parámetros; seleccione `Phone/CW` para acciones de manipulación CW | — |
| Parameter | Cuadro combinado | Elige la acción de destino a vincular; las opciones CW son `Trigger straight key`, `Trigger CW Left Paddle`, `Trigger CW Right Paddle` | — |
| Learn | Botón | Comienza a escuchar el siguiente mensaje MIDI y lo vincula al parámetro seleccionado; la etiqueta cambia a `Cancel Learn` mientras está activo | — |
| Bindings table | Lista | Muestra todas las vinculaciones actuales con controles por fila para Invertir, Relativo y eliminar | — |
| × (eliminar fila) | Botón | Elimina esa vinculación | — |
| Clear All | Botón | Elimina todas las vinculaciones | — |

## Consejos

- Estas tres acciones CW son de tipo momentáneo (gate): la llave se mantiene activa mientras el botón o nota MIDI permanezca presionado, y se libera al soltarlo. Utilice un pad o botón que envíe mensajes tanto de Note On como de Note Off para un comportamiento de manipulación correcto.
- Si guardó previamente un mapeo que usaba los identificadores heredados `cw.key`, `cw.dit` o `cw.dah`, AetherSDR los migra automáticamente a los identificadores actuales al cargarlos. No se requiere ninguna acción manual.
- Active **Auto-connect on startup** para que el puerto esté listo la próxima vez que AetherSDR se inicie sin necesidad de abrir este diálogo.

## Solución de problemas

- **La categoría `Phone/CW` falta en la lista de Parámetros** — Confirme que su compilación de AetherSDR sea v0.9.7 o posterior. Las tres acciones de puerta CW se agregaron en esa versión.
- **Learn se completa pero la llave no se activa al presionar** — Verifique que el estado del puerto muestre que está abierto (se hizo clic en Connect y el indicador de estado confirma la conexión). También verifique que el controlador MIDI esté enviando mensajes Note On/Off, visibles en el indicador de Actividad.
- **La vinculación desaparece después de reiniciar AetherSDR** — Las vinculaciones se guardan automáticamente cuando Learn se completa. Si el archivo no se escribió, verifique que AetherSDR tenga permiso de escritura en su directorio de configuración.

## Relacionado

- [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md)
- [Record a new binding with Learn mode](record-a-new-binding-with-learn-mode.md)
- [Auto-connect MIDI controller on startup](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Delete a binding](delete-a-binding.md)
- [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md)
