# Controles de TX

El applet Controles de TX proporciona controles de transmisión: medidores de potencia directa y ROE, deslizadores de potencia RF/Tune, selector de perfil TX, botones TUNE/MOX/ATU/MEM y conmutación APD (Adaptive Pre-Distortion) con indicadores de estado.

## Cambiar perfiles TX (p. ej. SSB, Digital)

Use el selector Perfil TX para cargar un perfil de transmisión con nombre desde la radio. Los perfiles almacenan configuraciones del micrófono, valores del ecualizador y otros parámetros de transmisión, permitiéndole cambiar rápidamente entre modos como SSB y Digital.

### Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Controles de TX requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión en la radio. Cree o administre perfiles mediante `Profiles > Profile Manager...`.

### Pasos

1. Haga clic en el botón de la bandeja **TX** en la barra lateral derecha para abrir el applet Controles de TX.
2. Localice el menú desplegable **TX Profile** cerca del centro del applet.
3. Haga clic en el menú desplegable y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

La radio carga el perfil seleccionado de inmediato. No se requiere ningún paso de confirmación.

### Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Profile** | Menú desplegable | Selecciona y carga un perfil de transmisión desde la radio. La lista es proporcionada por la radio. |

### Consejos

- También puede cargar un perfil desde la barra de menú sin abrir el applet Controles de TX. Vaya a `Profiles` y haga clic en el nombre del perfil en la lista seleccionable debajo del separador.
- Para crear, editar o eliminar perfiles, vaya a `Profiles > Profile Manager...`.

### Solución de problemas

- **El menú desplegable TX Profile está vacío** — No existen perfiles de transmisión en la radio. Abra `Profiles > Profile Manager...` para crear uno.
- **El menú desplegable TX Profile no responde** — AetherSDR no está conectado a la radio. Conéctelo primero mediante `Settings > Connect to Radio...`.

## Deslizadores de Potencia RF y Potencia Tune

Los deslizadores **RF Power** y **Tune Pwr** controlan los niveles de potencia de transmisión. Al arrastrar cualquier deslizador, una información sobre herramientas muestra el valor actual en vatios (p. ej., "50 W").

| Control | Rango | Valor predeterminado | Comportamiento |
|---|---|---|---|
| **RF Power** | 0–100 | 100 | Establece el nivel de potencia de RF de transmisión. Llama a `TransmitModel::setRfPower`. |
| **Tune Pwr** | 0–100 | 10 | Establece el nivel de potencia de la portadora de sintonía. Llama a `TransmitModel::setTunePower`. |

## Medidores de potencia

| Medidor | Rango | Comportamiento |
|---|---|---|
| **RF Pwr** | 0–120 W (sin amplificador), 0–600 W (Aurora 500W); rojo > 100 W / > 500 W | Muestra la potencia directa en la salida del excitador. La escala cambia según el modelo de radio. |
| **SWR** | 1.0–3.0 (rojo > 2.5) | Muestra la relación de onda estacionaria en el excitador. |

### Retención de pico del medidor de potencia RF (v26.5.2.1)

El medidor **RF Pwr** incluye una función de retención de pico que captura y mantiene la lectura de potencia envolvente de pico (PEP):

- El valor pico se mantiene constante durante 2 segundos después del pico más reciente.
- Después del período de retención, el valor pico decae hacia la lectura actual a una velocidad que toma aproximadamente 2.5 segundos desde el pico hasta cero.
- Cuando deja de transmitir, el valor de retención de pico se restablece a cero inmediatamente; una lectura PEP retenida no persiste entre transmisiones.

La velocidad de decaimiento se escala automáticamente según el modelo de radio: 48 W/s para una radio sin amplificador (escala de 120 W) y 240 W/s cuando un excitador Aurora 500 W está conectado (escala de 600 W).

## Comportamiento del botón ATU (v0.9.5.1)

A partir de v0.9.5.1, el botón **ATU** funciona como un conmutador por frecuencia que refleja el comportamiento de SmartSDR:

| Situación | Lo que hace el botón ATU |
|---|---|
| Sin sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización ATU. |
| El estado ATU es **Success** (o **OK**) y la frecuencia de transmisión no ha cambiado desde la última sintonización | Cambia el sintonizador al modo bypass. |
| El ATU está en bypass | El siguiente clic inicia un nuevo ciclo de sintonización. |

En la práctica, esto significa:

1. Haga clic en **ATU** en una nueva frecuencia: el sintonizador ejecuta un ciclo de sintonización completo.
2. Cuando el indicador **Success** se enciende en verde, haga clic en **ATU** nuevamente en la misma frecuencia: el sintonizador cambia a bypass.
3. Cambie de frecuencia y haga clic en **ATU**: el sintonizador siempre inicia un nuevo ciclo, incluso si el estado anterior fue exitoso.

El indicador **Byp** se enciende en naranja cuando el sintonizador está en bypass. El indicador **Success** se enciende en verde cuando la sintonización fue exitosa y el sintonizador mantiene esa adaptación.

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el amplificador TGXL está en modo OPERATE.

### Luces indicadoras ATU

| Indicador | Color | Significado |
|---|---|---|
| **Success** | Verde | El estado ATU es Successful u OK. |
| **Byp** | Naranja | El ATU está en Bypass o ManualBypass. |
| **Mem** | Verde | El ATU está usando una memoria. |

Todos los indicadores están atenuados cuando la condición asociada no está activa.

## Menú contextual del botón ATU (v26.5.2.1)

Haga clic derecho en el botón **ATU** para abrir un menú contextual con dos opciones avanzadas.

| Elemento del menú | Acción |
|---|---|
| **Pre-tune bands…** | Abre el diálogo Pre-Tune para barrer los ajustes del sintonizador de antena en un rango de frecuencias. Habilitado solo cuando **MEM** está activo. |
| **Clear ATU memories…** | Solicita confirmación y luego borra todas las memorias de sintonización ATU almacenadas en la radio. |

> **Nota:** **Pre-tune bands…** está deshabilitado cuando el botón **MEM** está apagado. Active **MEM** primero para usar esta función.

## Botón TUNE

Haga clic en **TUNE** para iniciar o detener una portadora de sintonía. Mientras está activo, el texto del botón cambia a "TUNING..." con un fondo rojo.

### Menú contextual del botón TUNE (v26.5.2.1)

Haga clic derecho en el botón **TUNE** para elegir la forma de la portadora para el próximo ciclo de sintonía. Esta es una selección única: la elección no se guarda en la configuración de AetherSDR.

| Elemento del menú | Acción |
|---|---|
| **Mono Tone** | Produce una portadora de un solo tono. Este es el comportamiento predeterminado. |
| **Two Tone** | Produce una portadora de dos tonos utilizada para probar la distorsión de intermodulación. |

El modo de sintonía de la radio también se restablece a un solo tono después de un ciclo de encendido.

## Botón MOX

Haga clic en **MOX** para activar o desactivar la transmisión manual. El botón se vuelve rojo mientras la transmisión está activada.

### Botón MOX y tonos Quindar (v0.9.7)

A partir de v0.9.7, al hacer clic en **MOX**, la solicitud de PTT se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. El efecto práctico es:

- Cuando Quindar está habilitado en la tira de canal de Audio y la rebanada TX activa está en un modo de telefonía (SSB, AM, FM, etc.), el tono K suena cuando se hace clic en **MOX** para activar y el tono BK suena cuando se hace clic en **MOX** para desactivar.
- Cuando Quindar está deshabilitado, o la rebanada TX activa no está en un modo de telefonía, el comportamiento es idéntico a versiones anteriores: el transmisor se activa y desactiva inmediatamente.

La apariencia del botón **MOX** no cambia: se vuelve rojo mientras la transmisión está activada y vuelve a su color predeterminado al soltarlo.

> **Nota:** Los tonos Quindar son una característica de la tira de canal de Audio. Active el control **QUIN** allí antes de esperar que los tonos suenen al usar PTT.

## Botón MEM

Haga clic en **MEM** para activar o desactivar la recuperación de memoria ATU. Deshabilitado cuando el TGXL está en modo OPERATE.

## Botón APD e indicadores de estado

Haga clic en **APD** para activar o desactivar la predistorsión adaptativa en la radio. Los indicadores de estado muestran el estado actual de APD:

| Indicador | Significado |
|---|---|
| **Active** (verde) | APD está activado y el ecualizador se aplica activamente. |
| **Cal** (verde) | APD está activado y aún está calibrando. |
| **Avail** (verde) | APD está activado y hay una calibración disponible pero aún no se ha aplicado. |
| Todos atenuados | APD está desactivado. |

La progresión de APD sigue: **Cal** (calibrando) → **Avail** (listo) → **Active** (aplicado).

## Relacionados

- [Descripción general de Controles de TX](overview.md)
- [Establecer potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar una sintonía de dos tonos](run-a-two-tone-tune.md)
