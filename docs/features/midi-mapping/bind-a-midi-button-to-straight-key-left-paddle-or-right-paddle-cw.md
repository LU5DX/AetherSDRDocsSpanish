# Vincular un botón MIDI a una Llave Directa, Paleta Izquierda o Paleta Derecha para CW

Use esta página para asignar un botón físico de su controlador MIDI a las entradas de llave directa, paleta izquierda o paleta derecha para CW en su FLEX-8600. Una vez vinculado, al presionar ese botón se activa la acción de manipulación correspondiente como un evento momentáneo (pulso).

## Antes de comenzar

- Su controlador MIDI está conectado a la computadora y reconocido por el sistema operativo.
- AetherSDR fue compilado con soporte MIDI (`HAVE_MIDI`).
- El diálogo de Mapeo MIDI no está ya en modo Aprendizaje de una sesión anterior.

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
7. Presione y mantenga presionado el botón físico de su controlador MIDI que desea vincular. AetherSDR detecta el mensaje MIDI y completa el enlace automáticamente.
8. Confirme que aparece una nueva fila en la tabla de Enlaces, mostrando el nombre del parámetro, el Origen MIDI y el Canal.
9. Repita los pasos 5 a 8 para cada entrada CW adicional que desee vincular.
10. Haga clic en Close.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Port: | Cuadro combinado | Selecciona el dispositivo de entrada MIDI | `MidiPort` |
| Refresh | Botón | Vuelve a escanear los puertos MIDI disponibles | — |
| Connect | Botón | Abre o cierra el puerto MIDI seleccionado | — |
| Auto-connect on startup | Casilla de verificación | Vuelve a abrir el puerto MIDI automáticamente en el próximo inicio | `MidiAutoConnect` |
| Category | Cuadro combinado | Filtra la lista de Parámetros; las categorías incluyen All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display y Frequency | — |
| Parameter | Cuadro combinado | Elige la acción de destino a vincular; las opciones CW son `Trigger straight key`, `Trigger CW Left Paddle`, `Trigger CW Right Paddle` | — |
| Learn | Botón | Comienza a escuchar el siguiente mensaje MIDI y lo vincula al parámetro seleccionado; la etiqueta cambia a `Cancel Learn` mientras está activo | — |
| Bindings table | Lista | Muestra todos los enlaces actuales con controles por fila de Invertir, Relativo y eliminar | — |
| × (eliminar fila) | Botón | Elimina ese enlace | — |
| Clear All | Botón | Elimina todos los enlaces | — |

## Consejos

- Estas tres acciones CW son de tipo momentáneo (pulso): la llave se mantiene presionada mientras la nota o el botón MIDI permanezca activo, y luego se suelta. Use un pad o botón que envíe mensajes de Note On y Note Off para un comportamiento de manipulación correcto.
- Si previamente guardó un mapeo que usaba los identificadores heredados `cw.key`, `cw.dit` o `cw.dah`, AetherSDR los migra automáticamente a los identificadores actuales al cargarlo. No se requiere ninguna acción manual.
- Active **Auto-connect on startup** para que el puerto esté listo la próxima vez que AetherSDR se inicie sin necesidad de abrir este diálogo.

## Solución de problemas

- **Falta la categoría `Phone/CW` en la lista de Parámetros** — Confirme que su compilación de AetherSDR sea v0.9.7 o posterior. Las tres acciones de pulso CW se agregaron en esa versión.
- **Learn se completa pero la llave no se activa al presionarla** — Verifique que el estado del puerto muestre que el puerto está abierto (se hizo clic en Connect y el indicador de estado confirma la conexión). También verifique que el controlador MIDI esté enviando mensajes Note On/Off, visibles en el indicador de Actividad.
- **El enlace desaparece después de reiniciar AetherSDR** — Los enlaces se guardan automáticamente cuando Learn se completa. Si el archivo no se escribió, compruebe que AetherSDR tenga permiso de escritura en su directorio de configuración.

## Relacionado

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Grabar un nuevo enlace con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar automáticamente el controlador MIDI al inicio](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Eliminar un enlace](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil nombrado](save-the-current-mapping-as-a-named-profile.md)
