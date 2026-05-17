# Invertir un mando o tratarlo como un codificador sin fin

Después de crear una vinculación MIDI, puede invertir su dirección con Invert o indicarle a AetherSDR que trate el control como un codificador sin fin con Relative. Ambas opciones se configuran por vinculación en la tabla Bindings.

## Antes de comenzar

- Debe tener un controlador MIDI conectado y al menos una vinculación existente. Consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md) y [Grabar una nueva vinculación con el modo Learn](record-a-new-binding-with-learn-mode.md).
- Abra `Settings > MIDI Mapping...` para acceder al cuadro de diálogo MIDI Controller Mapping.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Localice la vinculación que desea modificar en la tabla Bindings.
3. Para invertir la dirección del control, marque la casilla Invert en la fila de esa vinculación.
4. Para tratar el control como un codificador sin fin, marque la casilla Relative en la fila de esa vinculación.
5. Cualquiera de las casillas puede marcarse o desmarcarse de forma independiente. Los cambios surten efecto de inmediato.
6. Haga clic en Close cuando termine.

## Qué hace cada control

| Control  | Columna en Bindings | Comportamiento                                                                                                                          |
|----------|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| Invert   | Invert               | Invierte la dirección del control para esa vinculación. Girar en sentido horario disminuye, en sentido antihorario aumenta, o viceversa. |
| Relative | Relative             | Trata el control como un codificador sin fin. Úselo cuando su mando físico envíe valores incrementales (relativos) en lugar de posiciones absolutas (0–127). |

## Filtro de categoría

El cuadro combinado Category sobre la tabla Bindings filtra el cuadro combinado Parameter a una categoría de control específica. En la v26.5.2.1, las categorías disponibles son:

- All
- RX
- TX
- Phone/CW
- EQ
- Global
- Mode
- Band
- Filter
- Slice
- Display
- Frequency

Seleccione una categoría para limitar la lista de parámetros mostrados al crear una nueva vinculación.

## Nuevas acciones momentáneas de disparo CW

En la v26.5.2.1, la categoría Phone/CW incluye tres nuevas acciones momentáneas (Gate) para la manipulación de CW:

- **Trigger straight key** (id: cwkey) — Simula la pulsación de una llave directa.
- **Trigger CW Left Paddle** (id: cwdit) — Simula la pulsación de la paleta izquierda (dit).
- **Trigger CW Right Paddle** (id: cwdah) — Simula la pulsación de la paleta derecha (dah).

Los identificadores heredados con puntos (cw.key, cw.dit, cw.dah) se migran automáticamente al nuevo formato al cargar perfiles antiguos.

## Consejos

- Use Relative cuando su mando envíe valores pequeños de incremento/decremento en lugar de una posición absoluta. Si un mando salta erráticamente al girarlo, activar Relative suele corregirlo.
- Invert y Relative pueden combinarse en la misma vinculación. Por ejemplo, un codificador Relative que incremente en la dirección equivocada puede tener ambas opciones marcadas.
- Los cambios en Invert y Relative se guardan automáticamente al guardar un perfil. Use Save en Profile: para conservarlos.
- Las acciones de disparo CW son momentáneas: se activan mientras se mantiene presionado el control MIDI y se desactivan al soltarlo.

## Solución de problemas

- **Activar Relative hace que un mando deje de responder** — Es posible que el mando esté enviando valores absolutos (0–127). Desmarque Relative y deje la vinculación en modo absoluto.
- **El control sigue moviéndose en la dirección equivocada después de marcar Invert** — Verifique que marcó Invert en la fila correcta. Cada fila de vinculación tiene su propia casilla Invert; desplácese horizontalmente si la columna no está visible.

## Relacionados

- [Grabar una nueva vinculación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Eliminar una vinculación](delete-a-binding.md)
- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
