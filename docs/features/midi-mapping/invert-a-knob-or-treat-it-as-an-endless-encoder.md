# Invertir un mando o tratarlo como un codificador sin fin

Después de crear una vinculación MIDI, puede invertir su dirección con Invertir o indicarle a AetherSDR que trate el control como un codificador sin fin con Relativo. Ambas opciones se configuran por vinculación en la tabla de Vinculaciones.

## Antes de empezar

- Debe haber un controlador MIDI conectado y al menos una vinculación existente. Consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md) y [Grabar una nueva vinculación con el modo Aprender](record-a-new-binding-with-learn-mode.md).
- Abra `Settings > MIDI Mapping...` para acceder al cuadro de diálogo de Asignación de controlador MIDI.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Localice la vinculación que desea cambiar en la tabla de Vinculaciones.
3. Para invertir la dirección del control, marque la casilla de verificación Invertir en la fila de esa vinculación.
4. Para tratar el control como un codificador sin fin, marque la casilla de verificación Relativo en la fila de esa vinculación.
5. Cualquiera de las casillas de verificación se puede marcar o desmarcar de forma independiente. Los cambios surten efecto de inmediato.
6. Haga clic en Cerrar cuando haya terminado.

## Qué hace cada control

| Control  | Columna en la tabla de Vinculaciones | Comportamiento                                                                                                                               |
|----------|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Invertir | Invertir                             | Invierte la dirección del control para esa vinculación. Girar en sentido horario disminuye, en sentido antihorario aumenta, o viceversa.        |
| Relativo | Relativo                             | Trata el control como un codificador sin fin. Úselo cuando su mando de hardware envíe valores incrementales (relativos) en lugar de posiciones absolutas (0–127). |

## Filtro de categoría

El cuadro combinado Categoría sobre la tabla de Vinculaciones filtra el cuadro combinado Parámetro a una categoría de control específica. En v26.6.1, las categorías disponibles son:

- Todo
- RX
- TX
- Phone/CW
- EQ
- Global
- Modo
- Banda
- Filtro
- Slice
- Pantalla
- Frecuencia

Seleccione una categoría para reducir la lista de parámetros que se muestran al crear una nueva vinculación.

## Nuevas acciones momentáneas de disparo CW

En v26.6.1, la categoría Phone/CW incluye tres nuevas acciones momentáneas (Gate) para la manipulación telegráfica:

- **Disparar manipulador directo** (id: cwkey) — Simula la pulsación de un manipulador directo.
- **Disparar pala izquierda CW** (id: cwdit) — Simula la pulsación de la pala izquierda (dit).
- **Disparar pala derecha CW** (id: cwdah) — Simula la pulsación de la pala derecha (dah).

Los identificadores heredados con puntos (cw.key, cw.dit, cw.dah) se migran automáticamente al nuevo formato al cargar perfiles antiguos.

## Consejos

- Use Relativo cuando su mando envíe pequeños valores de incremento/decremento en lugar de una posición absoluta. Si un mando salta erráticamente al girarlo, activar Relativo suele corregirlo.
- Invertir y Relativo se pueden combinar en la misma vinculación. Por ejemplo, un codificador Relativo que incrementa en la dirección incorrecta puede tener ambas opciones marcadas.
- Los cambios en Invertir y Relativo se guardan automáticamente al guardar un perfil. Use Guardar en Perfil: para preservarlos.
- Las acciones de disparo CW son momentáneas: se activan mientras se mantiene presionado el control MIDI y se desactivan al soltarlo.

## Solución de problemas

- **Marcar Relativo hace que un mando deje de responder** — Es posible que el mando esté enviando valores absolutos (0–127). Desmarque Relativo y deje la vinculación en modo absoluto.
- **El control aún se mueve en la dirección incorrecta después de marcar Invertir** — Confirme que marcó Invertir en la fila correcta. Cada fila de vinculación tiene su propia casilla de verificación Invertir; desplácese horizontalmente si la columna no es visible.

## Relacionado

- [Grabar una nueva vinculación con el modo Aprender](record-a-new-binding-with-learn-mode.md)
- [Eliminar una vinculación](delete-a-binding.md)
- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
