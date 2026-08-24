# Descripción general de los controles de TX

El applet TX Controls le brinda acceso directo a todas las funciones de transmisión: monitoreo de potencia directa y ROE, ajuste de niveles de salida, selección de un perfil de TX, activación del transmisor, ejecución del ATU y habilitación de la Pre-Distorsión Adaptativa. Todos estos controles están agrupados en un solo lugar en el Panel de Applets.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. TX Controls requiere una conexión activa a la radio.
- Asegúrese de que el Panel de Applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

TX Controls está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de bandeja **TX** en la barra lateral derecha.

El applet está organizado en filas de arriba hacia abajo:

1. **Meters** — lecturas en tiempo real de potencia directa de RF y ROE con retención de pico.
2. **Power sliders** — establezca los niveles de potencia de transmisión y de portadora de sintonía antes de activar la transmisión.
3. **Profile and ATU status** — elija un perfil de TX y vea el estado actual del ATU de un vistazo.
4. **Action buttons** — TUNE, MOX, ATU y MEM para el control de transmisión y del sintonizador.
5. **APD** — alterne la Pre-Distorsión Adaptativa y monitoree su estado de calibración.

Ninguno de los ajustes de TX Controls es persistido por AetherSDR; los valores siguen el estado actual de la radio.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango / Estados | Qué hace |
|---|---|---|---|---|
| **RF Pwr** | Medidor | — | 0–120 W; rojo por encima de 100 W (sin amplificador) / 0–600 W; rojo por encima de 500 W (Aurora 500W) | Muestra la potencia directa en la salida del excitador. La escala cambia automáticamente según el modelo de radio. Incluye una barra de retención de pico que mantiene la lectura PEP más alta durante 2 segundos y luego decae al valor suavizado actual. El pico se restablece a cero inmediatamente cuando el transmisor desactiva la transmisión. Cuando no se transmite, el medidor lee cero. Pase el cursor sobre el medidor para ver la lectura exacta en vatios (p. ej., "45 W"). |
| **SWR** | Medidor | — | 1.0–3.0; rojo por encima de 2.5 | Muestra la relación de onda estacionaria en el excitador. Cuando no se transmite, o cuando no se reporta un valor de ROE válido, el medidor se ubica en 1.0. Pase el cursor sobre el medidor para ver la lectura exacta de la relación (p. ej., "1.42:1"). |
| **RF Power** | Deslizador | 100 | 0–100 | Establece el nivel de potencia de transmisión de RF como porcentaje del máximo. Durante el arrastre del deslizador, una información sobre herramientas muestra el porcentaje actual (p. ej., "75%"). Los valores se sincronizan con la radio al soltar el deslizador. |
| **Tune Pwr** | Deslizador | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía como porcentaje del máximo. Durante el arrastre del deslizador, una información sobre herramientas muestra el porcentaje actual (p. ej., "50%"). Los valores se sincronizan con la radio al soltar el deslizador. |
| **TX Profile** | Lista desplegable | — | Se completa desde la radio | Selecciona y carga un perfil de transmisión de la lista de perfiles de la radio. |
| **Success** | Indicador | Atenuado | Atenuado / verde | Se enciende en verde cuando el ATU reporta un resultado de sintonía exitoso u OK. |
| **Byp** | Indicador | Atenuado | Atenuado / naranja | Se enciende en naranja cuando el ATU está en Bypass o ManualBypass. |
| **Mem** | Indicador | Atenuado | Atenuado / verde | Se enciende en verde cuando el ATU recupera una memoria guardada. |
| **TUNE** | Botón | — | TUNE / TUNING... | Inicia una portadora de sintonía. La etiqueta cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic nuevamente para detener. Haga clic derecho para abrir el Menú Contextual de Tune y seleccionar la forma de la portadora. |
| **MOX** | Botón de alternancia | — | Apagado / encendido (rojo) | Alterna la transmisión manual. El botón se vuelve rojo mientras el transmisor está activado. En reposo, el botón tiene un borde ámbar de acento y texto para distinguirlo de los botones TUNE, ATU y MEM (personalizable en el Editor de Temas). En v0.9.7, al hacer clic en MOX se enruta a través del coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar y desactivar PTT en modos de telefónía cuando Quindar está habilitado en la Tira de Canales de Audio. Consulte [Tonos MOX y Quindar](#tonos-mox-y-quindar) a continuación. |
| **ATU** | Botón | — | — | Inicia un ciclo de sintonía del ATU o cambia el sintonizador a bypass, según el estado actual y la frecuencia. Consulte [Comportamiento del botón ATU](#comportamiento-del-botón-atu) a continuación. Deshabilitado cuando TGXL está en modo OPERATE, o cuando la radio no tiene sintonizador de antena. Haga clic derecho para abrir el Menú Contextual del ATU. |
| **MEM** | Botón de alternancia | — | Apagado / encendido | Alterna la recuperación de memoria del ATU. Deshabilitado cuando TGXL está en modo OPERATE, o cuando la radio no tiene sintonizador de antena. |
| **APD** | Botón de alternancia | — | Apagado / encendido | Alterna la Pre-Distorsión Adaptativa en la radio. |
| **Active** | Indicador | Atenuado | Atenuado / verde | Encendido cuando APD está activado y el ecualizador se aplica activamente. |
| **Cal** | Indicador | Atenuado | Atenuado / verde | Encendido cuando APD está activado y aún está calibrando. |
| **Avail** | Indicador | Atenuado | Atenuado / verde | Encendido cuando APD está activado y hay una calibración disponible pero aún no aplicada. |

### Comportamiento del botón ATU

El botón **ATU** alterna entre iniciar un ciclo de sintonía y poner el sintonizador en bypass, coincidiendo con el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o cualquier clic después de un cambio de frecuencia)** — inicia un ciclo de sintonía ATU nuevo.
- **Segundo clic en la misma frecuencia** — si el ATU reporta una coincidencia exitosa u OK y no ha cambiado de frecuencia desde que se completó esa sintonía, al hacer clic en **ATU** nuevamente se cambia el sintonizador a bypass.
- **Después de un bypass** — se borra el registro de la frecuencia sintonizada. El siguiente clic siempre inicia un ciclo de sintonía nuevo.

Si cambia de frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonía independientemente del estado anterior del ATU.

### Disponibilidad de los botones ATU y MEM

Los botones **ATU** y **MEM** están deshabilitados, con una información sobre herramientas explicativa, en dos situaciones:

- **La radio no tiene sintonizador de antena** — la radio reportó que no hay sintonizador presente (p. ej., una Hermes-Lite 2). La información sobre herramientas dice "This radio has no antenna tuner". Esta verificación tiene prioridad sobre el estado de TGXL.
- **TGXL está en modo OPERATE** — el sintonizador se omite a través del TGXL. La información sobre herramientas dice "Disabled — TGXL is in OPERATE mode". **TUNE** permanece habilitado; envía una portadora a través del TGXL para verificaciones de potencia/ROE, coincidiendo con el comportamiento de SmartSDR (#443).

### Menú contextual del ATU

Haga clic derecho en el botón **ATU** para abrir el menú contextual del ATU con las siguientes opciones:

- **Pre-tune bands…** — abre el diálogo de Barrido de Pre-Sintonía. Esta opción solo está disponible cuando las memorias del ATU (MEM) están habilitadas. Si está deshabilitada, una información sobre herramientas explica que MEM debe habilitarse primero.
- **Clear ATU memories…** — abre un diálogo de confirmación. Haga clic en **Yes** para borrar todas las memorias del ATU almacenadas en la radio.

### Menú contextual de Tune

Haga clic derecho en el botón **TUNE** para abrir el menú contextual de Tune. Esto le permite elegir la forma de la portadora para el siguiente ciclo de sintonía. El menú ofrece dos opciones:

- **Mono Tone** — una única portadora de tono.
- **Two Tone** — dos tonos simultáneos (normalmente utilizados para pruebas de IMD).

Seleccionar cualquiera de las opciones la aplica inmediatamente para el siguiente ciclo de sintonía. Esta es una configuración de un solo uso: no se guarda en AppSettings, y la radio vuelve a su modo de sintonía predeterminado al reiniciarse. El modo actualmente activo se muestra con una marca de verificación.

### Tonos MOX y Quindar

A partir de v0.9.7, al hacer clic en **MOX** se enruta la solicitud de PTT a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Cuando Quindar está habilitado en la Tira de Canales de Audio:

- **Activación (MOX encendido)** — el tono K se reproduce antes de que el transmisor se active.
- **Desactivación (MOX apagado)** — el tono BK se reproduce después de que el transmisor se desactive.

Este comportamiento se aplica solo a modos de telefónía. En modos que no son de telefónía, o cuando Quindar está deshabilitado en la Tira de Canales de Audio, MOX activa el transmisor inmediatamente como antes.

### Progresión del estado de APD

APD avanza por tres estados en secuencia: **Cal** (calibrando) → **Avail** (calibración lista, aún no aplicada) → **Active** (ecualizador aplicado a la señal transmitida).

## Applet ShackSwitch

La versión v0.9.4 añade soporte para el dispositivo ShackSwitch. Cuando se detecta un ShackSwitch, el Panel de Applets muestra su botón de bandeja (**SS**) y su applet automáticamente. Ambos están ocultos cuando no hay ningún dispositivo ShackSwitch presente. No se requiere configuración manual para mostrar u ocultar este applet.

## Consejos

- Mantenga **Tune Pwr** bajo (el predeterminado es 10) para evitar estresar la antena o el amplificador durante la sintonía del ATU.
- Observe el medidor de **SWR** después de un ciclo de sintonía. El indicador **Success** confirma que el ATU encontró una coincidencia, pero el medidor de SWR le muestra el resultado real.
- La escala del medidor de **RF Pwr** cambia automáticamente entre 0–120 W (FLEX-8600 sin amplificador) y 0–600 W (Aurora 500W); el umbral rojo se ajusta en consecuencia.
- El medidor de **RF Pwr** incluye una barra de retención de pico que mantiene la lectura PEP más alta durante 2 segundos y luego decae gradualmente. Esto se restablece inmediatamente cuando desactiva la transmisión. Tanto la lectura en vivo como la retención de pico se ponen a cero al desactivar.
- Cuando el transmisor no está activado, el medidor de **SWR** se ubica en 1.0 en lugar de mostrar una lectura obsoleta. Un valor de ROE válido solo se muestra mientras se transmite.
- Pase el cursor sobre los medidores de **RF Pwr** o **SWR** para ver la lectura numérica exacta — útil cuando necesita valores precisos en lugar de estimar a partir de las marcas de escala.
- Use el menú contextual de clic derecho en **TUNE** para alternar entre portadoras de sintonía Mono Tone y Two Tone para fines de prueba.
- Después de una sintonía exitosa, hacer clic en **ATU** una segunda vez en la misma frecuencia pone el sintonizador en bypass. Para volver a sintonizar, cambie de frecuencia o haga clic en **ATU** nuevamente después del bypass.
- Haga clic derecho en **ATU** para acceder a las funciones de Barrido de Pre-Sintonía y borrar las memorias del ATU.
- Si los botones **ATU** y **MEM** están deshabilitados, pase el cursor sobre ellos para ver el motivo. La información sobre herramientas distingue entre una radio sin sintonizador y un TGXL en modo OPERATE.
- Si usa **MOX** en un modo de telefónía con Quindar habilitado, permita que el tono K termine antes de hablar. El transmisor no se activa hasta que el tono se completa.
- Al arrastrar los deslizadores de **RF Power** o **Tune Pwr**, una información sobre herramientas muestra el valor de potencia exacto como porcentaje (p. ej., "75%"), lo que facilita establecer niveles precisos. Los valores se envían a la radio cuando suelta el deslizador.

## Relacionados

- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Habilitar APD para linealizar el transmisor](enable-apd-to-linearise-the-transmitter.md)
- [Ejecutar una sintonía de Two-Tone](run-a-two-tone-tune.md)
- [Realice su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
- Pre-sintonizar memorias del ATU
- Borrar memorias del ATU
<!-- docmesh:llm version=v26.8.4 date=2026-06-16 -->
