# Cambiar perfiles de TX (por ejemplo, SSB, Digital)

Los perfiles de TX almacenan ajustes de transmisión como la ecualización del micrófono, la compresión y el procesamiento de audio específico por modo. Cambiar de perfil permite pasar rápidamente entre configuraciones — por ejemplo, de un perfil de voz SSB a un perfil para modos digitales — sin ajustar cada parámetro manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls requiere una conexión activa con el radio.
- Los perfiles de TX deben existir previamente en el radio. Para crear o editar perfiles, use `Profiles > Profile Manager...`.

## Pasos

1. Haga clic en el botón **TX** del panel lateral derecho para abrir el applet TX Controls.
2. Localice el menú desplegable **TX Profile** cerca de la parte superior del applet, debajo de los controles deslizantes RF Power y Tune Pwr.
3. Haga clic en el menú desplegable **TX Profile** y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

El radio carga el perfil seleccionado de inmediato. No se requiere confirmación adicional.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado |
|---|---|---|---|
| **TX Profile** | Menú desplegable | Carga el perfil de transmisión seleccionado en el radio. La lista se obtiene de los perfiles almacenados en el radio. | Ninguno (se llena al conectar) |

## Consejos

- También puede cambiar de perfil desde la barra de menú. Abra `Profiles` y haga clic en cualquier nombre de perfil de la lista que aparece debajo del separador. El perfil activo se indica con una marca de verificación.
- El contenido de los perfiles (ecualización, compresión, etc.) se almacena en el radio, no en AetherSDR. Use `Profiles > Profile Manager...` para administrarlos.

## Solución de problemas

- **El menú desplegable TX Profile está vacío** — No hay perfiles de transmisión almacenados en el radio. Abra `Profiles > Profile Manager...` para crear uno.
- **El menú desplegable TX Profile no responde** — AetherSDR no está conectado al radio. El applet TX Controls requiere una conexión activa. Verifique su conexión mediante `Settings > Connect to Radio...`.

## Relacionados

- [Descripción general de TX Controls](overview.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Realice su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
