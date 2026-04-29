# Cambiar perfiles de TX (p. ej., SSB, Digital)

Use el selector de perfil de TX para cargar un perfil de transmisión con nombre desde el radio. Los perfiles almacenan ajustes de micrófono, valores de ecualizador y otros parámetros de transmisión, lo que permite cambiar rápidamente entre modos como SSB y Digital.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls requiere una conexión activa con el radio.
- Debe existir al menos un perfil de transmisión en el radio. Cree o administre perfiles desde `Profiles > Profile Manager...`.

## Pasos

1. Haga clic en el botón de bandeja **TX** en la barra lateral derecha para abrir el applet TX Controls.
2. Localice el menú desplegable **TX Profile** cerca de la parte central del applet.
3. Haga clic en el menú desplegable y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

El radio carga el perfil seleccionado de inmediato. No se requiere ningún paso de confirmación.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Valores válidos |
|---|---|---|---|---|
| **TX Profile** | Menú desplegable | Selecciona y carga un perfil de transmisión desde el radio. La lista es proporcionada por el radio. | — | Proviene de la lista de perfiles del radio |

## Consejos

- También puede cargar un perfil desde la barra de menú sin abrir el applet TX Controls. Vaya a `Profiles` y haga clic en el nombre del perfil en la lista con casillas de verificación debajo del separador.
- Para crear, editar o eliminar perfiles, vaya a `Profiles > Profile Manager...`.

## Solución de problemas

- **El menú desplegable TX Profile está vacío** — No existen perfiles de transmisión en el radio. Abra `Profiles > Profile Manager...` para crear uno.
- **El menú desplegable TX Profile no responde** — AetherSDR no está conectado al radio. Conéctese primero desde `Settings > Connect to Radio...`.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar una prueba de dos tonos](run-a-two-tone-tune.md)
