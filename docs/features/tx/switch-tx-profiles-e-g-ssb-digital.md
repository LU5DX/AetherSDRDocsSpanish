# Cambiar perfiles de TX (p. ej., SSB, Digital)

Use el selector de perfiles de TX para cargar un perfil de transmisión con nombre desde el radio. Los perfiles almacenan ajustes del micrófono, valores del ecualizador y otros parámetros de transmisión, lo que permite cambiar rápidamente entre modos como SSB y Digital.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls requiere una conexión activa con el radio.
- Al menos un perfil de transmisión debe existir previamente en el radio. Cree o administre perfiles mediante `Profiles > Profile Manager...`.

## Pasos

1. Haga clic en el botón de bandeja **TX** en la barra lateral derecha para abrir el applet TX Controls.
2. Localice el menú desplegable **TX Profile** cerca del centro del applet.
3. Haga clic en el menú desplegable y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

El radio carga el perfil seleccionado de inmediato. No se requiere ningún paso de confirmación.

## Qué hace cada control

| Control        | Tipo           | Comportamiento                                                                                        |
|----------------|----------------|-------------------------------------------------------------------------------------------------------|
| **TX Profile** | Menú desplegable | Selecciona y carga un perfil de transmisión desde el radio. La lista es proporcionada por el radio. |

## Consejos

- También puede cargar un perfil desde la barra de menú sin abrir el applet TX Controls. Vaya a `Profiles` y haga clic en el nombre del perfil en la lista seleccionable que aparece debajo del separador.
- Para crear, editar o eliminar perfiles, vaya a `Profiles > Profile Manager...`.

## Solución de problemas

- **El menú desplegable TX Profile está vacío** — No existen perfiles de transmisión en el radio. Abra `Profiles > Profile Manager...` para crear uno.
- **El menú desplegable TX Profile no responde** — AetherSDR no está conectado al radio. Conéctese primero mediante `Settings > Connect to Radio...`.

## Comportamiento del botón ATU (v0.9.5.1)

A partir de la v0.9.5.1, el botón **ATU** funciona como un conmutador por frecuencia que refleja el comportamiento de SmartSDR:

| Situación | Qué hace el botón ATU |
|---|---|
| No hay sintonización previa exitosa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización del ATU. |
| El estado del ATU es **Success** (u **OK**) y la frecuencia de transmisión no ha cambiado desde la última sintonización | Cambia el sintonizador a modo bypass. |
| El ATU está en bypass | El siguiente clic inicia un nuevo ciclo de sintonización. |

En la práctica, esto significa:

1. Haga clic en **ATU** en una nueva frecuencia — el sintonizador ejecuta un ciclo de sintonización completo.
2. Cuando el indicador **Success** se ilumina en verde, haga clic en **ATU** nuevamente en la misma frecuencia — el sintonizador pasa a modo bypass.
3. Cambie la frecuencia y haga clic en **ATU** — el sintonizador siempre inicia un nuevo ciclo, incluso si el estado anterior fue exitoso.

El indicador **Byp** se ilumina en naranja cuando el sintonizador está en bypass. El indicador **Success** se ilumina en verde cuando la sintonización fue exitosa y el sintonizador mantiene esa concordancia.

> **Nota:** Los botones **ATU** y **MEM** se deshabilitan cuando el amplificador TGXL está en modo OPERATE.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar una sintonización de dos tonos](run-a-two-tone-tune.md)
