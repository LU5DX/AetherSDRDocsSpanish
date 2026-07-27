# Controles de TX

El applet Controles de TX proporciona controles de transmisión: medidores de potencia directa y ROE, deslizadores de potencia RF/Sintonía, selector de perfil TX, botones TUNE/MOX/ATU/MEM y conmutación de APD (Predistorsión Adaptativa) con indicadores de estado.

## Cambiar perfiles TX (p. ej., SSB, Digital)

Use el selector de Perfil TX para cargar un perfil de transmisión con nombre desde la radio. Los perfiles almacenan configuraciones de micrófono, valores de ecualizador y otros parámetros de transmisión, lo que le permite cambiar rápidamente entre modos como SSB y Digital.

### Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Controles de TX requiere una conexión activa a la radio.
- Debe existir al menos un perfil de transmisión en la radio. Cree o administre perfiles a través de `Profiles > Profile Manager...`.

### Pasos

1. Haga clic en el botón de la bandeja **TX** en la barra lateral derecha para abrir el applet Controles de TX.
2. Localice el menú desplegable **TX Profile** cerca del centro del applet.
3. Haga clic en el menú desplegable y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

La radio carga el perfil seleccionado de inmediato. No se requiere ningún paso de confirmación.

### Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Profile** | Menú desplegable | Selecciona y carga un perfil de transmisión desde la radio. La lista la completa la radio. |

### Consejos

- También puede cargar un perfil desde la barra de menús sin abrir el applet Controles de TX. Vaya a `Profiles` y haga clic en el nombre del perfil en la lista seleccionable debajo del separador.
- Para crear, editar o eliminar perfiles, vaya a `Profiles > Profile Manager...`.

### Solución de problemas

- **El menú desplegable TX Profile está vacío** — No existen perfiles de transmisión en la radio. Abra `Profiles > Profile Manager...` para crear uno.
- **El menú desplegable TX Profile no responde** — AetherSDR no está conectado a la radio. Conéctelo primero a través de `Settings > Connect to Radio...`.

## Deslizadores de Potencia RF y Potencia de Sintonía

Los deslizadores **RF Power** y **Tune Pwr** controlan los niveles de potencia de transmisión. Al arrastrar cualquier deslizador, una información sobre herramientas muestra el valor actual como un porcentaje (por ejemplo, "50%").

| Control | Rango | Predeterminado | Comportamiento |
|---|---|---|---|
| **RF Power** | 0–100 | 100 | Establece el nivel de potencia de RF de transmisión como un porcentaje del máximo de la radio. Llama a `TransmitModel::setRfPower`. |
| **Tune Pwr** | 0–100 | 10 | Establece el nivel de potencia de la portadora de sintonía como un porcentaje del máximo de la radio. Llama a `TransmitModel::setTunePower`. |

> **Nota:** En v26.6.1, las informaciones sobre herramientas de los deslizadores ahora muestran porcentajes en lugar de valores en vatios. La potencia de salida real depende del modelo de radio y su potencia máxima nominal.

## Medidores de Potencia

| Medidor | Rango | Comportamiento |
|---|---|---|
| **RF Pwr** | 0–120 W (directo), 0–600 W (Aurora 500W); rojo > 100 W / > 500 W | Muestra la potencia directa en la salida del excitador. La escala cambia según el modelo de radio. Pase el cursor sobre el indicador para ver un valor exacto en vatios en una ventana emergente (v26.7.4). |
| **SWR** | 1.0–3.0 (rojo > 2.5) | Muestra la relación de onda estacionaria en el excitador. Pase el cursor sobre el indicador para ver la relación exacta en formato N.N:1 en una ventana emergente (v26.7.4). |

### Retención de pico del medidor de Potencia RF (v26.5.2.1)

El medidor **RF Pwr** incluye una función de retención de pico que captura y mantiene la lectura de potencia de pico envolvente (PEP):

- El valor pico se mantiene estable durante 2 segundos después del pico más reciente.
- Después del período de retención, el valor pico disminuye hacia la lectura actual a una velocidad que toma aproximadamente 2.5 segundos desde el pico hasta cero.
- Cuando deja de transmitir, el valor de retención de pico se restablece a cero inmediatamente; una lectura PEP retenida no persiste entre transmisiones.

La tasa de disminución se escala automáticamente según el modelo de radio: 48 W/s para una radio directa (escala de 120 W) y 240 W/s cuando está conectado un excitador Aurora 500 W (escala de 600 W).

### Ventanas emergentes de valor al pasar el cursor (v26.7.4)

A partir de v26.7.4, ambos medidores de potencia muestran una ventana emergente con la lectura numérica exacta al pasar el cursor del ratón sobre ellos:

- **RF Pwr** — Muestra el valor exacto en vatios (p. ej., "45 W").
- **SWR** — Muestra la relación exacta en formato convencional (p. ej., "1.42:1").

Esto le ayuda a leer valores precisos sin tener que estimar entre las marcas de graduación.

## Comportamiento del botón ATU (v0.9.5.1)

A partir de v0.9.5.1, el botón **ATU** funciona como un conmutador por frecuencia que refleja el comportamiento de SmartSDR:

| Situación | Qué hace el botón ATU |
|---|---|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización de la ATU. |
| El estado de la ATU es **Success** (o **OK**) y la frecuencia de transmisión no ha cambiado desde la última sintonización | Cambia el sintonizador a bypass. |
| La ATU está en bypass | El siguiente clic inicia un nuevo ciclo de sintonización. |

En la práctica, esto significa:

1. Haga clic en **ATU** en una nueva frecuencia: el sintonizador ejecuta un ciclo de sintonización completo.
2. Cuando el indicador **Success** se enciende en verde, haga clic en **ATU** nuevamente en la misma frecuencia: el sintonizador cambia a bypass.
3. Cambie la frecuencia y haga clic en **ATU**: el sintonizador siempre inicia un ciclo nuevo, incluso si el estado anterior fue exitoso.

El indicador **Byp** se enciende en naranja siempre que el sintonizador está en bypass. El indicador **Success** se enciende en verde cuando la sintonización fue exitosa y el sintonizador mantiene esa adaptación.

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el amplificador TGXL está en modo OPERATE.

### Luces indicadoras de ATU

| Indicador | Color | Significado |
|---|---|---|
| **Success** | Verde | El estado de la ATU es Successful u OK. |
| **Byp** | Naranja | La ATU está en Bypass o ManualBypass. |
| **Mem** | Verde | La ATU está usando una memoria. |

Todos los indicadores están atenuados cuando la condición asociada no está activa.

## Menú contextual del botón ATU (v26.5.2.1)

Haga clic derecho en el botón **ATU** para abrir un menú contextual con dos opciones avanzadas.

| Elemento del menú | Acción |
|---|---|
| **Pre-tune bands…** | Abre el diálogo Pre-Tune para barrer la configuración del sintonizador de antena en un rango de frecuencias. Solo está habilitado cuando **MEM** está activo. |
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

Haga clic en **MOX** para activar o desactivar la transmisión manual. El botón se vuelve rojo mientras la TX está activada.

### Apariencia del botón MOX (v26.7.4)

A partir de v26.7.4, el botón MOX tiene un distintivo acento ámbar cuando está inactivo para distinguirlo visualmente de los botones vecinos TUNE, ATU y MEM. Este acento utiliza colores de tema tokenizados (`color.tx.mox.border`, `color.tx.mox.text` y variantes al pasar el cursor) que puede editar en el Editor de Temas, el mismo enfoque utilizado para el chip LIVE del waterfall. El estado activo (transmitiendo) permanece rojo sólido con un borde rojo.

### Botón MOX y tonos Quindar (v0.9.7)

A partir de v0.9.7, al hacer clic en **MOX** se enruta la solicitud de PTT a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. El efecto práctico es:

- Cuando Quindar está habilitado en la tira de canal de audio y el slice TX activo está en un modo de telefonía (SSB, AM, FM, etc.), el tono K suena cuando se hace clic en **MOX** para activarlo y el tono BK suena cuando se hace clic en **MOX** para desactivarlo.
- Cuando Quindar está deshabilitado, o el slice TX activo no está en un modo de telefonía, el comportamiento es idéntico al de versiones anteriores: el transmisor se activa y desactiva inmediatamente.

La apariencia del botón **MOX** no cambia: se vuelve rojo mientras TX está activada y vuelve a su color predeterminado al soltarlo.

> **Nota:** Los tonos Quindar son una función de la tira de canal de audio. Active el control **QUIN** allí antes de esperar que suenen tonos al PTT.

## Botón MEM

Haga clic en **MEM** para activar o desactivar la recuperación de la memoria de la ATU. Deshabilitado cuando TGXL está en modo OPERATE.

## Botón APD e indicadores de estado

Haga clic en **APD** para activar o desactivar la predistorsión adaptativa en la radio. Los indicadores de estado muestran el estado actual de APD:

| Indicador | Significado |
|---|---|
| **Active** (verde) | APD está activado y el ecualizador se aplica activamente. |
| **Cal** (verde) | APD está activado y todavía está calibrando. |
| **Avail** (verde) | APD está activado y hay una calibración disponible pero aún no se ha aplicado. |
| Todos atenuados | APD está desactivado. |

La progresión de APD es: **Cal** (calibrando) → **Avail** (listo) → **Active** (aplicado).

## Marcadores de Activación de TX (v26.7.4)

A partir de v26.7.4, los botones TUNE, MOX y ATU están marcados internamente como controles de activación de TX. Este es un cambio estructural que afecta cómo las herramientas de accesibilidad y la lógica interna identifican los controles relacionados con la transmisión; no se asocia ningún cambio visual con esta marcación.

## Relacionado

- [Descripción general de Controles de TX](overview.md)
- [Establecer potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar una sintonía de dos tonos](run-a-two-tone-tune.md)
