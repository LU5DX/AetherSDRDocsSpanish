# Invertir un mando o tratarlo como un encoder sin fin

Una vez que existe un enlace MIDI, puede invertir su dirección con Invert o cambiarlo al modo relativo para que un encoder sin fin funcione correctamente en lugar de saltar a posiciones absolutas.

## Antes de comenzar

- Debe haber un controlador MIDI conectado y al menos un enlace ya existente. Consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md) y [Grabar un nuevo enlace con el modo Learn](record-a-new-binding-with-learn-mode.md).
- Abra `Settings > MIDI Mapping...` para acceder al diálogo MIDI Controller Mapping.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Localice el enlace que desea modificar en la tabla Bindings.
3. Para invertir la dirección del control, marque la casilla **Invert** en la fila correspondiente a ese enlace.
4. Para tratar el control como un encoder sin fin, marque la casilla **Relative** en la fila correspondiente a ese enlace.
5. Haga clic en **Close** para cerrar el diálogo. Los cambios surten efecto de inmediato y se guardan automáticamente.

## Qué hace cada control

| Control | Ubicación | Qué hace |
|---|---|---|
| Invert | Tabla Bindings, por fila | Invierte la dirección del control MIDI para ese enlace. |
| Relative | Tabla Bindings, por fila | Trata el control como un encoder sin fin en lugar de una fuente de posición absoluta. |

## Consejos

- Invert y Relative son independientes entre sí. Puede activar ambos en el mismo enlace; por ejemplo, un encoder sin fin invertido.
- Si un mando envía valores CC en el rango 0–127 y nota que siempre salta a una posición fija al girarlo, es probable que el control esté enviando valores absolutos. Active Relative para corregirlo.
- Los cambios en Invert y Relative se persisten de inmediato cuando Learn finaliza o cuando el diálogo guarda los enlaces. No es necesario usar Save en Profile: para conservar estos indicadores por enlace, pero guardar un perfil con nombre los capturará.

## Solución de problemas

- **Las casillas Invert o Relative no son visibles** — La tabla Bindings está vacía. Primero debe grabar al menos un enlace. Consulte [Grabar un nuevo enlace con el modo Learn](record-a-new-binding-with-learn-mode.md).
- **Activar Relative no tiene efecto en el comportamiento físico del mando** — Es posible que el controlador conectado esté enviando valores CC absolutos (0–127) en lugar de valores relativos o con signo. El modo Relative en AetherSDR espera que el propio controlador esté configurado para codificación relativa. Revise la configuración o la documentación de su controlador.

## Relacionados

- [Grabar un nuevo enlace con el modo Learn](record-a-new-binding-with-learn-mode.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)
- [Eliminar un enlace](delete-a-binding.md)
- [Guardar la configuración actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
