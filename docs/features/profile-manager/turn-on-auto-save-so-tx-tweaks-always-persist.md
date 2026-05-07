# Activar el guardado automático para que los ajustes de TX siempre persistan

Cuando el guardado automático está habilitado, cualquier cambio que realice en los ajustes de TX y de micrófono se escribe automáticamente en el perfil activo en la radio, de modo que nunca pierda un ajuste por olvidar guardarlo manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de Perfiles requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión o de micrófono en la radio para que el guardado automático tenga un perfil donde escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el cuadro de diálogo del Administrador de Perfiles.
2. Haga clic en la pestaña **Auto-Save**.
3. Marque **Auto-save profile changes**.
4. Haga clic en **Close**.

El ajuste surte efecto de inmediato. AetherSDR envía el cambio a la radio; no es necesario reiniciar.

Para desactivar el guardado automático, repita los pasos y desmarque **Auto-save profile changes**.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| **Auto-save profile changes** | Casilla de verificación | Cuando está marcada, los cambios en los ajustes de TX y micrófono se guardan automáticamente en el perfil activo de la radio. Cuando no está marcada, los cambios se descartan a menos que los guarde manualmente. | `AutoSaveTransmitProfile` |

## Consejos

- El guardado automático se aplica tanto a los ajustes de TX como a los de micrófono, no solo a una categoría. Si desea experimentar sin sobrescribir su perfil actual, desmarque primero **Auto-save profile changes**, realice sus cambios y evalúe antes de confirmar un guardado manual.
- La casilla de verificación refleja el estado actual reportado por la radio cuando se abre el cuadro de diálogo. Si otro cliente cambió el ajuste en la radio, la casilla se actualiza para coincidir.

## Relacionados

- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
- [Profile Manager overview](overview.md)
