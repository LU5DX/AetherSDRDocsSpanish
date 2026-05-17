# Cambiar Perfiles de TX (p. ej., SSB, Digital)

Utilice el selector de Perfil de TX para cargar un perfil de transmisión con nombre desde la radio. Los perfiles almacenan configuraciones de micrófono, valores de ecualizador y otros parámetros de transmisión, lo que le permite cambiar rápidamente entre modos como SSB y Digital.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Controles de TX requiere una conexión activa a la radio.
- Debe existir al menos un perfil de transmisión en la radio. Cree o administre perfiles a través de `Profiles > Profile Manager...`.

## Pasos

1. Haga clic en el botón de la bandeja **TX** en la barra lateral derecha para abrir el applet Controles de TX.
2. Localice el menú desplegable **TX Profile** cerca del centro del applet.
3. Haga clic en el menú desplegable y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

La radio carga el perfil seleccionado de inmediato. No se requiere ningún paso de confirmación.

## Qué hace cada control

| Control         | Tipo       | Comportamiento                                                                         |
|-----------------|------------|----------------------------------------------------------------------------------------|
| **TX Profile**  | Desplegable | Selecciona y carga un perfil de transmisión desde la radio. La lista es proporcionada por la radio. |

## Consejos

- También puede cargar un perfil desde la barra de menú sin abrir el applet Controles de TX. Vaya a `Profiles` y haga clic en el nombre del perfil en la lista seleccionable debajo del separador.
- Para crear, editar o eliminar perfiles, vaya a `Profiles > Profile Manager...`.

## Solución de problemas

- **El menú desplegable TX Profile está vacío** — No existen perfiles de transmisión en la radio. Abra `Profiles > Profile Manager...` para crear uno.
- **El menú desplegable TX Profile no responde** — AetherSDR no está conectado a la radio. Conéctese primero a través de `Settings > Connect to Radio...`.

## Comportamiento del botón ATU (v0.9.5.1)

A partir de v0.9.5.1, el botón **ATU** funciona como un conmutador por frecuencia que refleja el comportamiento de SmartSDR:

| Situación | Qué hace el botón ATU |
|---|---|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización del ATU. |
| El estado del ATU es **Success** (o **OK**) y la frecuencia de transmisión no ha cambiado desde la última sintonización | Cambia el sintonizador al modo de derivación (bypass). |
| El ATU está en modo de derivación (bypass) | El siguiente clic inicia un nuevo ciclo de sintonización. |

En la práctica, esto significa:

1. Haga clic en **ATU** en una nueva frecuencia — el sintonizador ejecuta un ciclo de sintonización completo.
2. Cuando el indicador **Success** se ilumina en verde, haga clic en **ATU** nuevamente en la misma frecuencia — el sintonizador cambia al modo de derivación (bypass).
3. Cambie la frecuencia y haga clic en **ATU** — el sintonizador siempre inicia un nuevo ciclo, incluso si el estado anterior fue exitoso.

El indicador **Byp** se ilumina en naranja siempre que el sintonizador esté en modo de derivación. El indicador **Success** se ilumina en verde cuando la sintonización fue exitosa y el sintonizador mantiene esa adaptación.

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el amplificador TGXL está en modo OPERATE.

## Menú contextual del botón ATU (v26.5.2.1)

Haga clic derecho en el botón **ATU** para abrir un menú contextual con dos opciones avanzadas.

| Elemento del Menú | Acción |
|---|---|
| **Pre-tune bands…** | Abre el diálogo de Pre-Sintonización para barrer las configuraciones del sintonizador de antena en un rango de frecuencias. Habilitado solo cuando **MEM** está activo. |
| **Clear ATU memories…** | Solicita confirmación y luego borra todas las memorias de sintonización ATU almacenadas en la radio. |

> **Nota:** **Pre-tune bands…** está deshabilitado cuando el botón **MEM** está apagado. Active **MEM** primero para usar esta función.

## Menú contextual del botón TUNE (v26.5.2.1)

Haga clic derecho en el botón **TUNE** para elegir la forma de la portadora para el próximo ciclo de sintonización. Esta es una selección de un solo uso: la elección no se guarda en la configuración de AetherSDR.

| Elemento del Menú | Acción |
|---|---|
| **Mono Tone** | Produce una portadora de tono único. Este es el comportamiento predeterminado. |
| **Two Tone** | Produce una portadora de dos tonos utilizada para probar la distorsión de intermodulación. |

El modo de sintonización de la radio también se restablece a tono único después de un ciclo de encendido.

## Botón MOX y tonos Quindar (v0.9.7)

A partir de v0.9.7, al hacer clic en **MOX**, la solicitud de PTT se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. El efecto práctico es:

- Cuando Quindar está habilitado en la tira de canales de audio y el slice de TX activo está en un modo de fonía (SSB, AM, FM, etc.), el tono K suena cuando se activa **MOX** y el tono BK suena cuando se desactiva **MOX**.
- Cuando Quindar está deshabilitado, o el slice de TX activo no está en un modo de fonía, el comportamiento es idéntico al de versiones anteriores: el transmisor se activa y desactiva inmediatamente.

La apariencia del botón **MOX** no cambia: se vuelve rojo mientras TX está activado y vuelve a su color predeterminado al soltarlo.

> **Nota:** Los tonos Quindar son una función de la tira de canales de audio. Active el control **QUIN** allí antes de esperar que suenen los tonos al usar PTT.

## Retención de pico del medidor de potencia de RF (v26.5.2.1)

El medidor **RF Pwr** incluye una función de retención de pico que captura y mantiene la lectura de potencia de pico envolvente (PEP):

- El valor pico se mantiene estable durante 2 segundos después del pico más reciente.
- Después del período de retención, el valor pico decae gradualmente hacia la lectura actual a una velocidad que toma aproximadamente 2.5 segundos desde el pico hasta cero.
- Cuando deja de transmitir, el valor de retención de pico se restablece a cero inmediatamente: una lectura de PEP retenida no persiste entre sobres.

La tasa de decaimiento se escala automáticamente según el modelo de radio: 48 W/s para una radio sin amplificador (escala de 120 W) y 240 W/s cuando está conectado un excitador Aurora de 500 W (escala de 600 W).

## Indicadores de estado de APD

Los indicadores **Active**, **Cal** y **Avail** muestran el estado actual del sistema de predistorsión adaptativa (APD):

| Estado | Significado |
|---|---|
| **Cal** (verde) | APD se está calibrando. |
| **Avail** (verde) | La calibración está completa y disponible pero aún no se ha aplicado. |
| **Active** (verde) | APD está activado y el ecualizador se aplica activamente. |
| Todos atenuados | APD está desactivado. |

## Relacionado

- [Descripción general de Controles de TX](overview.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar una sintonización de dos tonos](run-a-two-tone-tune.md)
