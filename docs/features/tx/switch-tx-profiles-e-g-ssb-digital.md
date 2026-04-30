# Cambiar perfiles TX (p. ej. SSB, Digital)

Use el selector de perfil TX para cargar un perfil de transmisión nombrado desde la radio. Los perfiles almacenan configuraciones de micrófono, valores del ecualizador y otros parámetros de transmisión, permitiéndole cambiar rápidamente entre modos como SSB y Digital.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX Controls requiere una conexión de radio activa.
- Al menos un perfil de transmisión debe existir ya en la radio. Cree o administre perfiles a través de `Profiles > Profile Manager...`.

## Pasos

1. Haga clic en el botón **TX** en la bandeja de la barra lateral derecha para abrir el applet TX Controls.
2. Localice el desplegable **TX Profile** cerca del medio del applet.
3. Haga clic en el desplegable y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

La radio carga el perfil seleccionado inmediatamente. No se requiere un paso de confirmación.

## Qué hace cada control

| Control        | Tipo      | Comportamiento                                                                                 |
|----------------|-----------|------------------------------------------------------------------------------------------------|
| **TX Profile** | Desplegable | Selecciona y carga un perfil de transmisión desde la radio. La lista es poblada por la radio. |

## Consejos

- También puede cargar un perfil desde la barra de menú sin abrir el applet TX Controls. Vaya a `Profiles` y haga clic en el nombre del perfil en la lista verificable debajo del separador.
- Para crear, editar o eliminar perfiles, vaya a `Profiles > Profile Manager...`.

## Solución de problemas

- **El desplegable TX Profile está vacío** — No existen perfiles de transmisión en la radio. Abra `Profiles > Profile Manager...` para crear uno.
- **El desplegable TX Profile no responde** — AetherSDR no está conectado a la radio. Conéctese primero a través de `Settings > Connect to Radio...`.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Establecer potencia de salida RF](set-rf-output-power.md)
- [Ejecutar una sintonización de dos tonos](run-a-two-tone-tune.md)
