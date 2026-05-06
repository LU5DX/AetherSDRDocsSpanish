# Vincular un botón MIDI a la llave recta, paleta izquierda o paleta derecha de CW

Use esta página para asignar un botón físico de su controlador MIDI a las entradas de llave recta, paleta izquierda o paleta derecha de CW en su FLEX-8600. Una vez vinculado, al presionar ese botón se activa la acción de manipulación correspondiente como un evento momentáneo (gate).

## Antes de comenzar

- Su controlador MIDI está conectado a la computadora y reconocido por el sistema operativo.
- AetherSDR fue compilado con soporte MIDI (`HAVE_MIDI`).
- El diálogo MIDI Mapping no está ya en modo Learn de una sesión anterior.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En el combo box **Port:**, seleccione su controlador MIDI de la lista. Si no aparece, haga clic en Refresh.
3. Haga clic en Connect. El indicador de estado cambia para mostrar que el puerto está abierto.
4. En el combo box **Category**, seleccione `Phone/CW`.
5. En el combo box **Parameter**, seleccione una de las siguientes opciones:
   - `Trigger straight key` — envía una pulsación de llave recta
   - `Trigger CW Left Paddle` — envía un evento de paleta izquierda (dit)
   - `Trigger CW Right Paddle` — envía un evento de paleta derecha (dah)
6. Haga clic en Learn. La etiqueta del botón cambia a `Cancel Learn`.
7. Presione y mantenga presionado el botón físico de su controlador MIDI que desea vincular. AetherSDR detecta el mensaje MIDI y completa el vínculo automáticamente.
8. Confirme que la nueva fila aparece en la tabla Bindings, mostrando el nombre del parámetro, la fuente MIDI (MIDI Source) y el canal (Channel).
9. Repita los pasos 5–8 para cada entrada de CW adicional que desee vincular.
10. Haga clic en Close.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Port: | Combo box | Selecciona el dispositivo de entrada MIDI | `MidiPort` |
| Refresh | Botón | Vuelve a escanear los puertos MIDI disponibles | — |
| Connect | Botón | Abre o cierra el puerto MIDI seleccionado | — |
| Auto-connect on startup | Casilla de verificación | Reabre el puerto MIDI automáticamente en el siguiente inicio | `MidiAutoConnect` |
| Category | Combo box | Filtra la lista de Parameter; seleccione `Phone/CW` para las acciones de manipulación CW | — |
| Parameter | Combo box | Elige la acción de destino a vincular; las opciones de CW son `Trigger straight key`, `Trigger CW Left Paddle`, `Trigger CW Right Paddle` | — |
| Learn | Botón | Comienza a escuchar el siguiente mensaje MIDI y lo vincula al parámetro seleccionado; la etiqueta pasa a `Cancel Learn` mientras está activo | — |
| Bindings table | Lista | Muestra todos los vínculos actuales con controles de Invert, Relative y eliminar por fila | — |
| × (eliminar fila) | Botón | Elimina ese vínculo | — |
| Clear All | Botón | Elimina todos los vínculos | — |

## Consejos

- Estas tres acciones de CW son de tipo momentáneo (gate): la llave se mantiene activa mientras el botón o nota MIDI permanezca activo y se libera al soltarlo. Use un pad o botón que envíe mensajes Note On y Note Off para un comportamiento de manipulación correcto.
- Si guardó previamente una asignación que usaba los IDs heredados `cw.key`, `cw.dit` o `cw.dah`, AetherSDR los migra automáticamente a los IDs actuales al cargar. No se requiere ninguna acción manual.
- Active **Auto-connect on startup** para que el puerto esté listo la próxima vez que inicie AetherSDR sin necesidad de abrir este diálogo.

## Solución de problemas

- **La categoría `Phone/CW` no aparece en la lista de Parameter** — Confirme que su versión de AetherSDR es v0.9.7 o posterior. Las tres acciones gate de CW se agregaron en esa versión.
- **Learn se completa pero la llave no se activa al presionar el botón** — Verifique que el estado del puerto muestre que está abierto (se hizo clic en Connect y el indicador de estado confirma la conexión). Además, compruebe que el controlador MIDI está enviando mensajes Note On/Off, visibles en el indicador de actividad (Activity).
- **El vínculo desaparece al reiniciar AetherSDR** — Los vínculos se guardan automáticamente cuando Learn se completa. Si el archivo no se escribió, verifique que AetherSDR tenga permisos de escritura en su directorio de configuración.

## Temas relacionados

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Registrar un nuevo vínculo con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar automáticamente el controlador MIDI al inicio](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Eliminar un vínculo](delete-a-binding.md)
- [Guardar la asignación actual como perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
