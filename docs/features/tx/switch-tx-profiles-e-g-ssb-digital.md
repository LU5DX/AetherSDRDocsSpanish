# Controles de TX

El applet Controles de TX proporciona los controles de transmisión: medidores de potencia directa y ROE, controles deslizantes de potencia RF/Tono, selector de perfil TX, botones TUNE/MOX/ATU/MEM y el conmutador APD (Predistorsión Adaptativa) con indicadores de estado.

## Cambiar perfiles TX (p. ej., SSB, Digital)

Use el selector de Perfil TX para cargar un perfil de transmisión con nombre desde la radio. Los perfiles almacenan la configuración del micrófono, los valores del ecualizador y otros parámetros de transmisión, lo que le permite cambiar rápidamente entre modos como SSB y Digital.

### Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Controles de TX requiere una conexión activa con la radio.
- Al menos un perfil de transmisión debe existir en la radio. Cree o administre perfiles mediante `Profiles > Profile Manager...`.

### Pasos

1. Haga clic en el botón **TX** de la bandeja en la barra lateral derecha para abrir el applet Controles de TX.
2. Localice la lista desplegable **TX Profile** cerca del centro del applet.
3. Haga clic en la lista desplegable y seleccione el nombre del perfil que desea cargar (por ejemplo, "SSB" o "Digital").

La radio carga el perfil seleccionado inmediatamente. No se requiere ningún paso de confirmación.

### Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **TX Profile** | Lista desplegable | Selecciona y carga un perfil de transmisión desde la radio. La lista se rellena desde la radio. |

### Consejos

- También puede cargar un perfil desde la barra de menú sin abrir el applet Controles de TX. Vaya a `Profiles` y haga clic en el nombre del perfil en la lista marcable debajo del separador.
- Para crear, editar o eliminar perfiles, vaya a `Profiles > Profile Manager...`.

### Solución de problemas

- **La lista desplegable TX Profile está vacía** — No existen perfiles de transmisión en la radio. Abra `Profiles > Profile Manager...` para crear uno.
- **La lista desplegable TX Profile no responde** — AetherSDR no está conectado a la radio. Conéctese primero mediante `Settings > Connect to Radio...`.

## Controles deslizantes de potencia RF y potencia de tono

Los controles deslizantes **RF Power** y **Tune Pwr** controlan los niveles de potencia de transmisión. Al arrastrar cualquiera de los controles deslizantes, una información sobre herramientas muestra el valor actual como porcentaje (p. ej., "50%").

| Control | Rango | Predeterminado | Comportamiento |
|---|---|---|---|
| **RF Power** | 0–100 | 100 | Establece el nivel de potencia de RF de transmisión como porcentaje del máximo de la radio. Llama a `TransmitModel::setRfPower`. |
| **Tune Pwr** | 0–100 | 10 | Establece el nivel de potencia de la portadora de tono como porcentaje del máximo de la radio. Llama a `TransmitModel::setTunePower`. |

> **Nota:** En la v26.6.1, las informaciones sobre herramientas de los controles deslizantes ahora muestran porcentajes en lugar de valores en vatios. La potencia de salida real depende del modelo de radio y su potencia máxima nominal.

## Medidores de potencia

| Medidor | Rango | Comportamiento |
|---|---|---|
| **RF Pwr** | 0–120 W (sin amplificador), 0–600 W (Aurora 500W); rojo > 100 W / > 500 W | Muestra la potencia directa en la salida del excitador. La escala cambia según el modelo de radio. Pase el cursor sobre el medidor para ver el valor exacto en vatios en una ventana emergente (v26.7.4). |
| **SWR** | 1.0–3.0 (rojo > 2.5) | Muestra la relación de onda estacionaria en el excitador. Pase el cursor sobre el medidor para ver la relación exacta en formato N.N:1 en una ventana emergente (v26.7.4). |

### Retención de pico del medidor de potencia RF (v26.5.2.1)

El medidor **RF Pwr** incluye una función de retención de pico que captura y mantiene la lectura de potencia de envolvente de pico (PEP):

- El valor máximo se mantiene firme durante 2 segundos después del pico más reciente.
- Después del período de retención, el valor máximo decae de nuevo hacia la lectura actual a una velocidad que tarda aproximadamente 2,5 segundos desde el pico hasta cero.
- Cuando deja de transmitir, el valor de retención de pico se restablece a cero inmediatamente — una lectura PEP retenida no persiste entre transmisiones.

La velocidad de decaimiento se escala automáticamente según el modelo de radio: 48 W/s para una radio sin amplificador (escala de 120 W) y 240 W/s cuando hay un excitador Aurora de 500 W conectado (escala de 600 W).

### Comportamiento del medidor al desactivar la transmisión (v26.8.4)

A partir de la v26.8.4, ambos medidores se limpian inmediatamente cuando deja de transmitir:

- El medidor **RF Pwr** baja a cero y la retención de pico se restablece inmediatamente.
- El medidor **SWR** vuelve a su posición de reposo en 1.0.

Anteriormente, los medidores podían mantener brevemente los últimos valores notificados después de desactivar la transmisión. Si la radio no notifica un valor de SWR válido durante la transmisión, el medidor de SWR descansa en 1.0 en lugar de mostrar una lectura obsoleta o fuera de escala.

### Ventanas emergentes de valor al pasar el cursor (v26.7.4)

A partir de la v26.7.4, ambos medidores de potencia muestran una ventana emergente con la lectura numérica exacta al pasar el cursor del mouse sobre ellos:

- **RF Pwr** — Muestra el valor exacto en vatios (p. ej., "45 W").
- **SWR** — Muestra la relación exacta en formato convencional (p. ej., "1.42:1").

Esto le ayuda a leer valores precisos sin estimar entre las marcas de la escala.

## Comportamiento del botón ATU (v0.9.5.1)

A partir de la v0.9.5.1, el botón **ATU** funciona como un conmutador por frecuencia que refleja el comportamiento de SmartSDR:

| Situación | Qué hace el botón ATU |
|---|---|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización ATU. |
| El estado de ATU es **Success** (o **OK**) y la frecuencia de transmisión no ha cambiado desde la última sintonización | Cambia el sintonizador a bypass. |
| ATU está en bypass | El siguiente clic inicia un nuevo ciclo de sintonización. |

En la práctica, esto significa:

1. Haga clic en **ATU** en una frecuencia nueva — el sintonizador ejecuta un ciclo completo de sintonización.
2. Cuando el indicador **Success** se ilumina en verde, haga clic en **ATU** nuevamente en la misma frecuencia — el sintonizador cambia a bypass.
3. Cambie la frecuencia y haga clic en **ATU** — el sintonizador siempre inicia un ciclo nuevo, incluso si el estado anterior fue exitoso.

El indicador **Byp** se ilumina en naranja siempre que el sintonizador esté en bypass. El indicador **Success** se ilumina en verde cuando la sintonización fue exitosa y el sintonizador mantiene esa coincidencia.

### Disponibilidad de ATU (v26.8.4)

A partir de la v26.8.4, los botones **ATU** y **MEM** se desactivan cuando la radio conectada no tiene sintonizador de antena. Esto evita que se active accidentalmente el transmisor para ejecutar un ciclo de sintonización que ningún sintonizador atenderá.

La información sobre herramientas explica por qué los botones están desactivados:

| Condición | Información sobre herramientas |
|---|---|
| La radio no tiene sintonizador de antena | "This radio has no antenna tuner" |
| El amplificador TGXL está en modo OPERATE | "Disabled — TGXL is in OPERATE mode" |

Cuando la radio no tiene sintonizador, la información sobre herramientas tiene prioridad sobre el mensaje de TGXL para que se le dirija a la causa raíz.

### Luces indicadoras de ATU

| Indicador | Color | Significado |
|---|---|---|
| **Success** | Verde | El estado de ATU es Successful u OK. |
| **Byp** | Naranja | ATU está en Bypass o ManualBypass. |
| **Mem** | Verde | ATU está usando una memoria. |

Todos los indicadores están atenuados cuando la condición asociada no está activa.

## Menú ATU con clic derecho (v26.5.2.1)

Haga clic derecho en el botón **ATU** para abrir un menú contextual con dos opciones avanzadas.

| Elemento de menú | Acción |
|---|---|
| **Pre-tune bands…** | Abre el diálogo Pre-Tune para barrer la configuración del sintonizador de antena a través de un rango de frecuencias. Habilitado solo cuando **MEM** está activo. |
| **Clear ATU memories…** | Solicita confirmación y luego borra todas las memorias de sintonización ATU almacenadas en la radio. |

> **Nota:** **Pre-tune bands…** está deshabilitado cuando el botón **MEM** está apagado. Habilite **MEM** primero para usar esta función.

## Botón TUNE

Haga clic en **TUNE** para iniciar o detener una portadora de tono. Mientras está activo, el texto del botón cambia a "TUNING..." con fondo rojo.

### Menú TUNE con clic derecho (v26.5.2.1)

Haga clic derecho en el botón **TUNE** para elegir la forma de la portadora para el próximo ciclo de tono. Esta es una selección única — la elección no se guarda en la configuración de AetherSDR.

| Elemento de menú | Acción |
|---|---|
| **Mono Tone** | Produce una portadora de tono único. Este es el comportamiento predeterminado. |
| **Two Tone** | Produce una portadora de dos tonos utilizada para probar la distorsión de intermodulación. |

El modo de tono de la radio también se restablece a tono único después de un ciclo de encendido.

## Botón MOX

Haga clic en **MOX** para alternar la transmisión manual. El botón se pone rojo mientras TX está activado.

### Apariencia del botón MOX (v26.7.4)

A partir de la v26.7.4, el botón MOX tiene un acento ámbar distintivo en reposo para distinguirlo visualmente de los botones vecinos TUNE, ATU y MEM. Este acento utiliza colores de tema tokenizados (`color.tx.mox.border`, `color.tx.mox.text` y variantes de hover) que puede editar en el Editor de temas — el mismo enfoque utilizado para el chip LIVE del waterfall. El estado activo (transmisión) permanece en rojo sólido con borde rojo.

### Botón MOX y tonos Quindar (v0.9.7)

A partir de la v0.9.7, al hacer clic en **MOX** se enruta la solicitud de PTT a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. El efecto práctico es:

- Cuando Quindar está habilitado en la tira de canales de audio y el slice TX activo está en un modo de telefonía (SSB, AM, FM, etc.), el tono K suena al hacer clic en **MOX** para activar y el tono BK suena al hacer clic en **MOX** para desactivar.
- Cuando Quindar está deshabilitado, o el slice TX activo no está en un modo de telefonía, el comportamiento es idéntico al de versiones anteriores — el transmisor se activa y desactiva inmediatamente.

La apariencia del botón **MOX** no cambia: se pone rojo mientras TX está activado y vuelve a su color predeterminado al soltarlo.

> **Nota:** Los tonos Quindar son una función de la tira de canales de audio. Habilite el control **QUIN** allí antes de esperar que suenen los tonos en PTT.

## Botón MEM

Haga clic en **MEM** para alternar la recuperación de memoria ATU activada o desactivada. Se desactiva cuando la radio no tiene sintonizador de antena o cuando TGXL está en modo OPERATE.

## Botón APD e indicadores de estado

Haga clic en **APD** para alternar la predistorsión adaptativa en la radio. Los indicadores de estado muestran el estado actual de APD:

| Indicador | Significado |
|---|---|
| **Active** (verde) | APD está activado y el ecualizador se aplica activamente. |
| **Cal** (verde) | APD está activado y aún se está calibrando. |
| **Avail** (verde) | APD está activado y hay una calibración disponible pero aún no aplicada. |
| Todos atenuados | APD está desactivado. |

La progresión de APD sigue: **Cal** (calibrando) → **Avail** (listo) → **Active** (aplicado).

### Visibilidad de la fila APD (v26.8.4)

A partir de la v26.8.4, el botón APD y sus indicadores Active/Cal/Avail están ocultos desde el inicio en radios que no admiten APD configurable. Anteriormente, un inicio en frío podía mostrar un control APD de apariencia activa sin nada detrás hasta que la radio notificara sus capacidades de APD. La fila ahora aparece solo una vez que la radio confirma que APD es configurable.

## Marcadores de activación TX (v26.7.4)

A partir de la v26.7.4, los botones TUNE, MOX y ATU están marcados internamente como controles de activación TX. Este es un cambio estructural que afecta cómo las herramientas de accesibilidad y la lógica interna identifican los controles relacionados con la transmisión — no hay ningún cambio visual asociado con esta marcación.

## Relacionados

- [Descripción general de Controles de TX](overview.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar un tono de dos tonos](run-a-two-tone-tune.md)
