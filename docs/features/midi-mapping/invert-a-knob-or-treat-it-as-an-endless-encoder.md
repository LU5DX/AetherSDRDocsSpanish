# Invertir un mando o tratarlo como un codificador sin fin

Después de crear un enlace MIDI, puede invertir su dirección con Invert o indicarle a AetherSDR que trate el control como un codificador sin fin con Relative. Ambas opciones se configuran por enlace en la tabla Bindings.

## Antes de comenzar

- Debe haber un controlador MIDI conectado y al menos un enlace ya existente. Consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md) y [Registrar un nuevo enlace con el modo Learn](record-a-new-binding-with-learn-mode.md).
- Abra `Settings > MIDI Mapping...` para acceder al diálogo MIDI Controller Mapping.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Localice el enlace que desea modificar en la tabla Bindings.
3. Para invertir la dirección del control, marque la casilla Invert en la fila de ese enlace.
4. Para tratar el control como un codificador sin fin, marque la casilla Relative en la fila de ese enlace.
5. Cada casilla puede marcarse o desmarcarse de forma independiente. Los cambios surten efecto de inmediato.
6. Haga clic en Close cuando termine.

## Qué hace cada control

| Control | Columna en la tabla Bindings | Comportamiento | Valor predeterminado |
|---|---|---|---|
| Invert | Invert | Invierte la dirección del control para ese enlace. Gire a la derecha para disminuir y a la izquierda para aumentar, o viceversa. | Desmarcado |
| Relative | Relative | Trata el control como un codificador sin fin. Úselo cuando el mando de hardware envíe valores incrementales (relativos) en lugar de posiciones absolutas (0–127). | Desmarcado |

## Consejos

- Use Relative cuando el mando envíe pequeños valores de incremento/decremento en lugar de una posición absoluta. Si un mando salta de forma errática al girarlo, habilitar Relative generalmente lo corrige.
- Invert y Relative pueden combinarse en el mismo enlace. Por ejemplo, un codificador Relative que incrementa en la dirección incorrecta puede tener ambas opciones marcadas.
- Los cambios en Invert y Relative se guardan automáticamente al guardar un perfil. Use Save en Profile: para conservarlos.

## Solución de problemas

- **Marcar Relative hace que un mando deje de responder** — Es posible que el mando esté enviando valores absolutos (0–127). Desmarque Relative y deje el enlace en modo absoluto.
- **El control sigue moviéndose en la dirección incorrecta después de marcar Invert** — Confirme que marcó Invert en la fila correcta. Cada fila de enlace tiene su propia casilla Invert; desplace la vista horizontalmente si la columna no está visible.

## Relacionados

- [Registrar un nuevo enlace con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Eliminar un enlace](delete-a-binding.md)
- [Guardar la configuración actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
