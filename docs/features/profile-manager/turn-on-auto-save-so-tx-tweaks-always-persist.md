# Activar el guardado automático para que los ajustes de TX siempre persistan

Cuando el guardado automático está habilitado, cualquier cambio que realice en los ajustes de TX y micrófono se escribe de vuelta en el perfil activo de forma automática, por lo que nunca perderá un ajuste por olvidarse de guardar manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Profile Manager requiere una conexión de radio activa.
- Debe existir al menos un perfil de transmisión o micrófono en la radio para que el guardado automático tenga un perfil en el cual escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Auto-Save**.
3. Active la casilla **Auto-save profile changes**.
4. Haga clic en **Close**.

El ajuste surte efecto de inmediato. AetherSDR envía el cambio a la radio; no se requiere reinicio.

Para desactivar el guardado automático, repita los pasos y desactive la casilla **Auto-save profile changes**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| **Auto-save profile changes** | Casilla de verificación | Cuando está activada, los cambios en los ajustes de TX y micrófono se guardan automáticamente en el perfil activo de la radio. Cuando está desactivada, los cambios se descartan a menos que guarde manualmente. | `AutoSaveTransmitProfile` |

## Consejos

- El guardado automático se aplica tanto a los ajustes de TX como a los de micrófono, no solo a una categoría. Si desea experimentar sin sobrescribir su perfil actual, desactive primero la casilla **Auto-save profile changes**, realice sus cambios y evalúe antes de confirmar un guardado manual.
- La casilla refleja el estado actual reportado por la radio cuando se abre el diálogo. Si otro cliente modificó el ajuste en la radio, la casilla se actualiza para reflejar ese cambio.

## Relacionados

- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Descripción general del Profile Manager](overview.md)
