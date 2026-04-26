# Cambiar perfiles de TX (p. ej., SSB, Digital)

Use el selector de perfiles de TX para cargar un perfil de transmisión con nombre almacenado en el radio — por ejemplo, cambiar de un perfil de voz SSB a un perfil de modos digitales sin volver a introducir manualmente los ajustes de micrófono, ecualizador o compresor.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls no funciona sin una conexión activa con el radio.
- Los perfiles de transmisión deben existir previamente en el FLEX-8600. Créelos o adminístrelos mediante `Profiles > Profile Manager...`.

## Pasos

1. Haga clic en el botón de bandeja **TX** en la barra lateral derecha para abrir el applet TX Controls, si aún no está visible.
2. Localice el menú desplegable **TX Profile** en el applet TX Controls. Aparece debajo de los controles deslizantes **RF Power** y **Tune Pwr**.
3. Haga clic en el menú desplegable **TX Profile** y seleccione el perfil que desea cargar (por ejemplo, "SSB" o "Digital").

El radio carga el perfil seleccionado de inmediato. No se requiere ningún paso de confirmación.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Valores válidos |
|---|---|---|---|---|
| **TX Profile** | Menú desplegable | Carga el perfil de transmisión seleccionado en el radio. La lista se rellena con los perfiles almacenados en el radio. | — | Perfiles devueltos por el radio |

## Consejos

- También puede cargar un perfil desde la barra de menús. Vaya a `Profiles` y haga clic en cualquier nombre de perfil que aparezca debajo del separador. La marca de verificación se desplaza al perfil recién cargado.
- Para crear, renombrar o eliminar perfiles, use `Profiles > Profile Manager...`.

## Solución de problemas

- **El menú desplegable TX Profile está vacío** — El radio no tiene perfiles de transmisión globales definidos. Abra `Profiles > Profile Manager...` para crear uno.
- **Seleccionar un perfil no tiene efecto** — Confirme que la conexión con el radio está activa. El selector de perfiles no envía ningún comando cuando AetherSDR está desconectado del radio.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Configurar la potencia del portador de sintonía](set-tune-carrier-power.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
