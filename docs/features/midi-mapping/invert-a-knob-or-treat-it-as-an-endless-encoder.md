# Invertir un mando o tratarlo como un codificador sin fin

Después de crear una vinculación MIDI, puede invertir su dirección con Invert o indicarle a AetherSDR que trate el control como un codificador sin fin con Relative. Ambas opciones se configuran por vinculación en la tabla de vinculaciones.

## Antes de comenzar

- Debe haber un controlador MIDI conectado y al menos una vinculación existente. Consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md) y [Grabar una nueva vinculación con el modo Learn](record-a-new-binding-with-learn-mode.md).
- Abra `Settings > MIDI Mapping...` para acceder al cuadro de diálogo de asignación MIDI.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Localice la vinculación que desea modificar en la tabla de vinculaciones.
3. Para invertir la dirección del control, marque la casilla Invert en la fila de esa vinculación.
4. Para tratar el control como un codificador sin fin, marque la casilla Relative en la fila de esa vinculación.
5. Cualquiera de las casillas se puede marcar o desmarcar de forma independiente. Los cambios surten efecto de inmediato.
6. Haga clic en Close cuando termine.

## Qué hace cada control

| Control  | Columna en la tabla de vinculaciones | Comportamiento                                                                                                                            |
|----------|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| Invert   | Invert                               | Invierte la dirección del control para esa vinculación. Girar en sentido horario disminuye, en sentido antihorario aumenta, o viceversa. |
| Relative | Relative                             | Trata el control como un codificador sin fin. Úselo cuando su mando físico envíe valores incrementales (relativos) en lugar de posiciones absolutas (0–127). |

## Consejos

- Use Relative cuando su mando envíe pequeños valores de incremento/decremento en lugar de una posición absoluta. Si un mando salta erráticamente al girarlo, habilitar Relative normalmente lo corrige.
- Invert y Relative se pueden combinar en la misma vinculación. Por ejemplo, un codificador Relative que incrementa en la dirección incorrecta puede tener ambas opciones marcadas.
- Los cambios en Invert y Relative se guardan automáticamente al guardar un perfil. Use Save en Profile: para conservarlos.

## Solución de problemas

- **Marcar Relative hace que un mando deje de responder** — Es posible que el mando esté enviando valores absolutos (0–127). Desmarque Relative y deje la vinculación en modo absoluto.
- **El control aún se mueve en la dirección incorrecta después de marcar Invert** — Confirme que marcó Invert en la fila correcta. Cada fila de vinculación tiene su propia casilla Invert; desplácese horizontalmente si la columna no está visible.

## Relacionado

- [Grabar una nueva vinculación con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Eliminar una vinculación](delete-a-binding.md)
- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
