# Activar el guardado automático para que los ajustes de TX siempre persistan

Active el guardado automático para que cualquier cambio realizado en los ajustes de transmisión y micrófono se escriba automáticamente en el perfil activo, sin necesidad de guardar manualmente después de cada ajuste.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Debe existir al menos un perfil de transmisión en el radio para que el guardado automático tenga un perfil donde escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Auto-Save**.
3. Marque **Auto-save profile changes**.
4. Haga clic en **Close**.

El ajuste surte efecto de inmediato. AetherSDR envía el cambio al radio y guarda su preferencia como `AutoSaveTransmitProfile`.

## Qué hace cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| **Auto-save profile changes** | Cuando está marcado, los cambios en los ajustes de TX y micrófono se guardan automáticamente en el perfil activo. Cuando no está marcado, los cambios no se escriben hasta que los guarde manualmente desde la pestaña **Transmit** o **Microphone**. | `AutoSaveTransmitProfile` |

## Consejos

- Para guardar el estado actual de transmisión con un nombre específico en lugar de depender del guardado automático, use la pestaña **Transmit** y haga clic en **Save** con un nombre introducido en el campo **Profile name**.
- El guardado automático aplica tanto a los ajustes de TX como a los de micrófono, no solo a uno de los dos.

## Relacionado

- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Crear un perfil de micrófono independiente por micrófono](create-a-separate-mic-profile-per-microphone.md)
