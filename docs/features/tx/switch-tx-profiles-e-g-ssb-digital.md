# Cambiar perfiles de TX (p. ej., SSB, Digital)

Use el selector de perfil de TX para cargar un perfil de transmisión con nombre desde la radio. Los perfiles guardan configuraciones de micrófono, valores de ecualizador y otros parámetros de transmisión, lo que le permite cambiar rápidamente entre modos como SSB y Digital.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Controles de TX requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión en la radio. Cree o administre perfiles mediante `Profiles > Profile Manager...`.

## Pasos

1. Haga clic en el botón de la bandeja **TX** en la barra lateral derecha para abrir el applet Controles de TX.
2. Localice el menú desplegable **TX Profile** cerca del centro del applet.
3. Haga clic en el menú desplegable y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

La radio carga el perfil seleccionado inmediatamente. No se requiere ningún paso de confirmación.

## Función de cada control

| Control        | Tipo       | Comportamiento                                                                                 |
|----------------|------------|----------------------------------------------------------------------------------------------|
| **TX Profile** | Desplegable | Selecciona y carga un perfil de transmisión desde la radio. La lista la proporciona la radio. |

## Consejos

- También puede cargar un perfil desde la barra de menús sin abrir el applet Controles de TX. Vaya a `Profiles` y haga clic en el nombre del perfil en la lista verificable debajo del separador.
- Para crear, editar o eliminar perfiles, vaya a `Profiles > Profile Manager...`.

## Solución de problemas

- **El menú desplegable TX Profile está vacío** — No existen perfiles de transmisión en la radio. Abra `Profiles > Profile Manager...` para crear uno.
- **El menú desplegable TX Profile no responde** — AetherSDR no está conectado a la radio. Conéctese primero mediante `Settings > Connect to Radio...`.

## Comportamiento del botón ATU (v0.9.5.1)

A partir de v0.9.5.1, el botón **ATU** funciona como un conmutador por frecuencia que refleja el comportamiento de SmartSDR:

| Situación | Qué hace el botón ATU |
|---|---|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización ATU. |
| El estado de ATU es **Success** (o **OK**) y la frecuencia de transmisión no ha cambiado desde la última sintonización | Cambia el sintonizador a bypass. |
| ATU está en bypass | El siguiente clic inicia un nuevo ciclo de sintonización. |

En la práctica, esto significa:

1. Haga clic en **ATU** en una frecuencia nueva: el sintonizador ejecuta un ciclo completo de sintonización.
2. Cuando el indicador **Success** se ilumina en verde, haga clic en **ATU** nuevamente en la misma frecuencia: el sintonizador cambia a bypass.
3. Cambie de frecuencia y haga clic en **ATU**: el sintonizador siempre inicia un nuevo ciclo, incluso si el estado anterior fue exitoso.

El indicador **Byp** se ilumina en naranja siempre que el sintonizador está en bypass. El indicador **Success** se ilumina en verde cuando la sintonización fue exitosa y el sintonizador mantiene esa adaptación.

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el amplificador TGXL está en modo OPERATE.

## Botón MOX y tonos Quindar (v0.9.7)

A partir de v0.9.7, al hacer clic en **MOX**, la solicitud de PTT se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. El efecto práctico es:

- Cuando Quindar está habilitado en la tira de canal de audio y el slice de TX activo está en un modo de telefonía (SSB, AM, FM, etc.), el tono K se reproduce al activar **MOX** y el tono BK se reproduce al desactivar **MOX**.
- Cuando Quindar está deshabilitado, o el slice de TX activo no está en un modo de telefonía, el comportamiento es idéntico al de versiones anteriores: el transmisor se activa y desactiva inmediatamente.

La apariencia del botón **MOX** no cambia: se vuelve rojo mientras TX está activado y vuelve a su color predeterminado al soltarlo.

> **Nota:** Los tonos Quindar son una función de la tira de canal de audio. Active el control **QUIN** allí antes de esperar que se reproduzcan tonos al usar PTT.

## Relacionados

- [Descripción general de Controles de TX](overview.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar un tono de dos tonos](run-a-two-tone-tune.md)
