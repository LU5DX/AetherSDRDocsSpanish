# Activar el guardado automático para que los ajustes de TX siempre persistan

Cuando el guardado automático está habilitado, cualquier cambio que realice en los ajustes de TX y micrófono se escribe de vuelta al perfil activo de forma automática, por lo que no se pierde nada al cambiar de perfil o reiniciar.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Profile Manager requiere una conexión de radio activa.
- Debe existir al menos un perfil de transmisión o micrófono en la radio para que el guardado automático tenga un perfil al que escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña `Auto-Save (tab)`.
3. Marque `Auto-save profile changes`.

AetherSDR envía el cambio a la radio de inmediato. No se requiere ningún paso adicional de guardado. Para deshabilitar el guardado automático, desmarque `Auto-save profile changes`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| `Auto-save profile changes` | Cuando está marcado, los cambios en los ajustes de TX y micrófono se guardan automáticamente en el perfil activo de la radio. Cuando está desmarcado, los cambios se descartan a menos que guarde un perfil manualmente. | `AutoSaveTransmitProfile` |

## Consejos

- El guardado automático se aplica a los perfiles de transmisión y micrófono activos en ese momento. Si no hay ningún perfil activo en la radio, el guardado automático no tiene a dónde escribir. Cargue un perfil primero usando la pestaña `Transmit (tab)` o `Microphone (tab)` antes de habilitar el guardado automático.
- Para guardar manualmente un estado específico sin habilitar el guardado automático, use el botón `Save` en la pestaña `Transmit (tab)` o `Microphone (tab)`.

## Relacionados

- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Crear un perfil de micrófono separado por micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Descripción general del Profile Manager](overview.md)
