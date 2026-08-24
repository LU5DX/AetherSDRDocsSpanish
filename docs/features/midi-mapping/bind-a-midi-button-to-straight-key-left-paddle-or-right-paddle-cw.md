# Mapeo de controlador MIDI

Use esta página para asignar botones, perillas y otros controles de su controlador MIDI a funciones de radio en su FLEX-8600.

## Antes de comenzar

- Su controlador MIDI está conectado a la computadora y es reconocido por el sistema operativo.
- AetherSDR fue compilado con soporte MIDI (`HAVE_MIDI`).
- El diálogo de Mapeo MIDI no está ya en modo Learn de una sesión anterior.

## Configurar un controlador MIDI

1. Abra `Settings > MIDI Mapping...`.
2. En el cuadro combinado **Port:**, seleccione su controlador MIDI de la lista. Si no aparece, haga clic en **Refresh**.
3. Haga clic en **Connect**. El indicador de estado cambia a `Opened`.
4. (Opcional) Marque **Auto-connect on startup** para reabrir el mismo puerto la próxima vez que AetherSDR se inicie.

> El diálogo recuerda su tamaño y posición entre sesiones.

## Crear una asignación con modo Learn

1. En el cuadro combinado **Category**, seleccione una categoría para reducir la lista de parámetros.
2. En el cuadro combinado **Parameter**, seleccione el parámetro de destino.
3. Haga clic en **Learn**. La etiqueta del botón cambia a `Cancel Learn`.
4. Mueva el control (botón, perilla o deslizador) en su controlador MIDI que desea asignar. AetherSDR detecta el mensaje MIDI y completa la asignación automáticamente.
5. Confirme que la nueva fila aparece en la **tabla de asignaciones**, mostrando el nombre del parámetro, la fuente MIDI y el canal.
6. Repita para cada asignación adicional.

## Crear o editar una asignación manualmente

Si prefiere no usar el modo Learn, o necesita corregir una asignación existente:

1. Haga clic en **Manual…** para escribir el canal de una asignación (1–16), tipo de mensaje (Note, Control Change, Program Change, Pitch Bend) y número de mensaje.
   - El mismo editor está disponible por fila: haga clic en el botón **✎ (edit binding)** en la fila que desea corregir.
2. Cambie los valores y confirme para aplicar la asignación.

## Editar, invertir o hacer una asignación relativa

- **Invert** — Marque esta casilla para invertir la dirección del control en esa fila.
- **Relative** — Marque esta casilla para tratar el control como un codificador rotatorio continuo.
- **✎ (edit binding)** — Abre el mismo editor manual descrito anteriormente, precargado con los valores actuales de la fila, para que pueda corregir canal, tipo de mensaje o número.
- **× (delete row)** — Elimina esa asignación.
- **Clear All** — Elimina todas las asignaciones.

## Administrar perfiles

1. Para guardar las asignaciones actuales como un perfil, haga clic en **Save** y asígnele un nombre.
2. Para aplicar un perfil guardado previamente, selecciónelo en el cuadro combinado **Profile:** y haga clic en **Load**.
3. Para importar asignaciones desde un archivo:
   - Haga clic en **Import...** y seleccione un XML de perfil de AetherSDR o un archivo `.map` de SmartSDR.
   - AetherSDR informa cuántas asignaciones fueron importadas. Haga clic en **Load** para aplicarlas.
4. Para escribir las asignaciones actuales en un archivo, haga clic en **Export...** y elija una ubicación. La exportación se guarda como un archivo XML de perfil de AetherSDR.
   - AetherSDR recuerda el último directorio usado para Importar/Exportar y lo reabre la próxima vez.

## Referencia de controles

| Control                    | Tipo       | Comportamiento                                                                               |
|----------------------------|------------|----------------------------------------------------------------------------------------------|
| Port:                      | Cuadro combinado | Selecciona el dispositivo de entrada MIDI                                              |
| Refresh                    | Botón      | Reescanea los puertos MIDI disponibles                                                       |
| Connect                    | Botón      | Abre o cierra el puerto MIDI seleccionado                                                    |
| Port status                | Indicador  | Muestra si el puerto MIDI está actualmente abierto (`Opened` o `Closed`)                     |
| Activity indicator         | Indicador  | Muestra el mensaje MIDI más reciente recibido                                                |
| Auto-connect on startup    | Casilla    | Reabre el puerto MIDI al iniciar                                                             |
| Category                   | Cuadro combinado | Filtra la lista de parámetros por categoría de control                                 |
| Parameter                  | Cuadro combinado | Elige el parámetro de destino para una nueva asignación                                 |
| Learn                      | Botón      | Comienza a escuchar el siguiente mensaje MIDI y lo asigna al parámetro seleccionado          |
| Manual…                    | Botón      | Abre un diálogo para escribir el canal, tipo de mensaje y número de una asignación en lugar de usar Learn |
| Bindings table             | Lista      | Muestra las asignaciones existentes; columnas: Parámetro, Fuente MIDI, Canal, Invertir, Relativo, editar, eliminar |
| ✎ (edit binding)           | Botón      | Abre el editor manual para esa fila                                                          |
| Invert                     | Casilla    | Invierte la dirección del control para la fila                                               |
| Relative                   | Casilla    | Trata el control como un codificador rotatorio continuo                                      |
| × (delete row)             | Botón      | Elimina esa asignación                                                                       |
| Clear All                  | Botón      | Elimina todas las asignaciones                                                               |
| Profile:                   | Cuadro combinado | Selecciona un perfil de mapeo MIDI guardado                                              |
| Save                       | Botón      | Guarda las asignaciones actuales como un perfil                                              |
| Load                       | Botón      | Carga el perfil seleccionado                                                                 |
| Import...                  | Botón      | Importa un archivo de perfil al almacén — XML de perfil de AetherSDR o un archivo `.map` de SmartSDR |
| Export...                  | Botón      | Exporta las asignaciones actuales como un archivo XML de perfil de AetherSDR                 |
| Close                      | Botón      | Cierra el diálogo                                                                             |

## Asignar un botón MIDI a la tecla CW

Estos pasos asignan un botón físico en su controlador MIDI a las entradas de tecla recta, paleta izquierda o paleta derecha CW.

1. En el cuadro combinado **Category**, seleccione `Phone/CW`.
2. En el cuadro combinado **Parameter**, seleccione una de las siguientes opciones:
   - `Trigger straight key` — envía una pulsación de tecla recta
   - `Trigger CW Left Paddle` — envía un evento de paleta izquierda (dit)
   - `Trigger CW Right Paddle` — envía un evento de paleta derecha (dah)
3. Haga clic en **Learn**, luego presione y mantenga presionado el botón físico en su controlador MIDI.
4. Confirme que la nueva fila aparece en la **tabla de asignaciones**.

Estas tres acciones CW son de tipo momentáneo (compuerta): la tecla se mantiene presionada mientras el Note MIDI o botón permanezca activo, y luego se libera. Use un pad o botón que envíe mensajes tanto Note On como Note Off para un comportamiento de tecleo correcto.

Si previamente guardó un mapeo que usaba los IDs heredados `cw.key`, `cw.dit` o `cw.dah`, AetherSDR los migra automáticamente a los IDs actuales (`cwkey`, `cwdit`, `cwdah`) al cargar. No se requiere acción manual.

## Solución de problemas

- **Learn se completa pero la tecla no se activa al presionarla** — Verifique que el estado del puerto muestre `Opened`. Confirme que el controlador MIDI está enviando mensajes Note On/Off, visibles en el indicador de actividad.
- **La asignación desaparece después de reiniciar AetherSDR** — Las asignaciones se guardan automáticamente cuando Learn se completa. Si el archivo no se escribió, verifique que AetherSDR tenga permiso de escritura en su directorio de configuración.
- **La categoría `Phone/CW` falta en la lista de parámetros** — Confirme que su compilación de AetherSDR sea v0.9.7 o posterior. Las tres acciones de compuerta CW se agregaron en esa versión.

## Relacionado

- [Grabar una nueva asignación con modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Auto-conectar controlador MIDI al iniciar](../../getting-started/setup/auto-connect-midi-controller-on-startup.md)
- [Eliminar una asignación](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
