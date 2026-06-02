# Vincular un botón MIDI a la llave directa, la paleta izquierda o la paleta derecha de CW

Use esta página para asignar un botón físico de su controlador MIDI a las entradas de llave directa, paleta izquierda (dit) o paleta derecha (dah) de CW de su FLEX-8600. Una vez vinculado, al presionar ese botón se activa la acción de manipulación correspondiente como un evento momentáneo (gate).

## Antes de comenzar

- Su controlador MIDI está conectado a la computadora y es reconocido por el sistema operativo.
- AetherSDR fue compilado con soporte MIDI (`HAVE_MIDI`).
- El diálogo de Mapeo MIDI no está ya en modo Aprendizaje de una sesión anterior.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Port:**, seleccione su controlador MIDI de la lista. Si no aparece, haga clic en **Refresh**.
3. Haga clic en **Connect**. El indicador de estado cambia para mostrar que el puerto está abierto.
4. En el cuadro combinado **Category**, seleccione `Phone/CW`.
5. En el cuadro combinado **Parameter**, seleccione una de las siguientes opciones:
   - `Trigger straight key` — envía una pulsación de llave directa
   - `Trigger CW Left Paddle` — envía un evento de paleta izquierda (dit)
   - `Trigger CW Right Paddle` — envía un evento de paleta derecha (dah)
6. Haga clic en **Learn**. La etiqueta del botón cambia a `Cancel Learn`.
7. Presione y mantenga presionado el botón físico de su controlador MIDI que desea vincular. AetherSDR detecta el mensaje MIDI y completa la vinculación automáticamente.
8. Confirme que la nueva fila aparece en la **tabla de Vinculaciones**, mostrando el nombre del parámetro, la fuente MIDI y el canal.
9. Repita los pasos 5 a 8 para cada entrada de CW adicional que desee vincular.
10. Haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Port: | Cuadro combinado | Selecciona el dispositivo de entrada MIDI | `MidiPort` |
| Refresh | Botón | Vuelve a escanear los puertos MIDI disponibles | — |
| Connect | Botón | Abre o cierra el puerto MIDI seleccionado | — |
| Estado del puerto | Indicador | Muestra si el puerto MIDI está actualmente abierto (Opened o Closed) | — |
| Indicador de actividad | Indicador | Muestra el mensaje MIDI más reciente recibido | — |
| Auto-connect on startup | Casilla de verificación | Vuelve a abrir el puerto MIDI automáticamente en el próximo inicio | `MidiAutoConnect` |
| Category | Cuadro combinado | Filtra la lista de Parámetros; las categorías incluyen All, RX, TX, Phone/CW, EQ, Global, Mode, Band, Filter, Slice, Display y Frequency | — |
| Parameter | Cuadro combinado | Elige la acción de destino a vincular; las opciones de CW son `Trigger straight key`, `Trigger CW Left Paddle`, `Trigger CW Right Paddle` | — |
| Learn | Botón | Comienza a escuchar el siguiente mensaje MIDI y lo vincula al parámetro seleccionado; la etiqueta cambia a `Cancel Learn` mientras está activo | — |
| Tabla de vinculaciones | Lista | Muestra todas las vinculaciones actuales con controles por fila de Invert, Relative y eliminar; columnas: Parameter, MIDI Source, Channel, Invert, Relative, (eliminar) | — |
| Invert | Casilla de verificación | Invierte la dirección de control para la fila | — |
| Relative | Casilla de verificación | Trata el control como un codificador sin fin | — |
| × (eliminar fila) | Botón | Elimina esa vinculación | — |
| Clear All | Botón | Elimina todas las vinculaciones | — |
| Profile: | Cuadro combinado | Elige un perfil de mapeo MIDI guardado | — |
| Save | Botón | Guarda las vinculaciones actuales como un perfil | — |
| Load | Botón | Carga el perfil seleccionado | — |
| Close | Botón | Cierra el diálogo | — |

## Consejos

- Estas tres acciones de CW son de tipo momentáneo (gate): la llave se mantiene activa mientras el mensaje de nota MIDI o el botón permanezcan activos, y luego se suelta. Use un pad o botón que envíe mensajes tanto de Note On como de Note Off para un correcto comportamiento de manipulación.
- Si previamente guardó un mapeo que usaba los identificadores heredados `cw.key`, `cw.dit` o `cw.dah`, AetherSDR los migra automáticamente a los identificadores actuales (`cwkey`, `cwdit`, `cwdah`) al cargarlo. No se necesita ninguna acción manual.
- Active **Auto-connect on startup** para que el puerto esté listo la próxima vez que AetherSDR se inicie sin necesidad de abrir este diálogo.
- Use el cuadro combinado **Profile:** para guardar y cargar perfiles de mapeo con nombre. Haga clic en **Save** para almacenar las vinculaciones actuales, o en **Load** para aplicar un perfil guardado previamente.
- El diálogo recuerda su tamaño y posición entre sesiones.

## Solución de problemas

- **La categoría `Phone/CW` falta en la lista de Parámetros** — Confirme que su compilación de AetherSDR sea v0.9.7 o posterior. Las tres acciones de gate de CW se agregaron en esa versión.
- **Learn se completa pero la llave no se activa al presionarla** — Verifique que el estado del puerto muestre que el puerto está abierto (se hizo clic en Connect y el indicador de estado confirma la conexión). También verifique que el controlador MIDI esté enviando mensajes Note On/Off, visibles en el indicador de actividad.
- **La vinculación desaparece después de reiniciar AetherSDR** — Las vinculaciones se guardan automáticamente cuando Learn se completa. Si el archivo no se escribió, verifique que AetherSDR tenga permiso de escritura en su directorio de configuración.

## Relacionado

- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Grabar una nueva vinculación con el modo Aprendizaje](record-a-new-binding-with-learn-mode.md)
- [Conectar automáticamente el controlador MIDI al inicio](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Eliminar una vinculación](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
