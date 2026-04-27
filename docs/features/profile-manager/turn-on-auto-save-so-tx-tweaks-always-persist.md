# Activar el guardado automático para que los ajustes de TX siempre persistan

Cuando el guardado automático está habilitado, cualquier cambio que realice en los ajustes de TX y micrófono se escribe de vuelta al perfil activo de forma automática, de modo que nunca perderá un ajuste por olvidar guardarlo manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Debe existir al menos un perfil de transmisión o de micrófono en el radio para que el guardado automático tenga un perfil en el cual escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Auto-Save**.
3. Marque **Auto-save profile changes**.
4. Haga clic en **Close**.

El ajuste surte efecto de inmediato. AetherSDR envía el cambio al radio; no se requiere reinicio.

Para desactivar el guardado automático, repita los pasos y desmarque **Auto-save profile changes**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| **Auto-save profile changes** | Casilla de verificación | Cuando está marcada, los cambios en los ajustes de TX y micrófono se guardan automáticamente en el perfil activo del radio. Cuando está desmarcada, los cambios se descartan a menos que los guarde manualmente. | `AutoSaveTransmitProfile` |

## Consejos

- El guardado automático se aplica tanto a los ajustes de TX como a los de micrófono, no solo a una categoría. Si desea experimentar sin sobrescribir su perfil actual, desmarque **Auto-save profile changes** primero, realice sus cambios y evalúe antes de confirmar un guardado manual.
- La casilla refleja el estado actual reportado por el radio cuando se abre el diálogo. Si otro cliente cambió el ajuste en el radio, la casilla se actualiza para coincidir con dicho estado.

## Relacionados

- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Descripción general del Profile Manager](overview.md)
