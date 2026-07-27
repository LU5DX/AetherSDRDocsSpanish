# Cambiar a un perfil de transmisión guardado

Cambie la radio a un perfil de transmisión previamente guardado, cargando su configuración de micrófono, procesador, ecualizador y filtro, sin afectar los perfiles globales ni los perfiles solo de micrófono.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Debe existir al menos un perfil de transmisión en la radio. Si no existe ninguno, cree uno usando **Profiles > Profile Manager...** y el botón **Save** o **Create** en la pestaña Transmit.

## Pasos

1. Abra el **Profile Manager** seleccionando **Profiles > Profile Manager...**.
2. Haga clic en la pestaña **Transmit**.
3. En la lista de perfiles, haga clic en el perfil que desea cargar.
4. Haga clic en **Load**.

La radio cambia al perfil de transmisión seleccionado. El nombre del perfil activo aparece resaltado en la lista.

## Consejos

- Para cargar un perfil sin abrir el Profile Manager, use el mosaico **Profile Switcher** en el panel de applets. Consulte [Cycle through transmit profiles quickly](cycle-through-transmit-profiles-quickly.md).
- Active **Auto-Save** en la pestaña Auto-Save para que cualquier cambio que realice en la configuración de TX se guarde automáticamente en el perfil activo.

## Relacionado

- [Profile Manager overview](../profile-manager/overview.md)
- [Profile Switcher overview](overview.md)
- [Cycle through transmit profiles quickly](cycle-through-transmit-profiles-quickly.md)
- [Turn on auto-save so TX tweaks always persist](../profile-manager/turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [See which profile is currently active](see-which-profile-is-currently-active.md)
