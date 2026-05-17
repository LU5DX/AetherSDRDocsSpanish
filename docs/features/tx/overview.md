# Resumen de controles TX

El applet Controles TX le brinda acceso directo a todas las funciones de transmisión: monitoreo de potencia directa y ROE, ajuste de niveles de salida, selección de un perfil TX, activación del transmisor, operación del ATU y habilitación de la Predistorsión Adaptativa. Todos estos controles están agrupados en un solo lugar en el Panel de applets.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. Los controles TX requieren una conexión activa a la radio.
- Asegúrese de que el Panel de applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

Controles TX está siempre presente en el Panel de applets (barra lateral derecha). Alterne su visibilidad con el botón de bandeja **TX** en la barra lateral derecha.

El applet está organizado en filas de arriba a abajo:

1. **Medidores** — lecturas en tiempo real de potencia directa RF y ROE con retención de pico.
2. **Deslizadores de potencia** — ajuste los niveles de potencia de transmisión y de portadora de sintonía antes de activar la transmisión.
3. **Estado del perfil y del ATU** — elija un perfil TX y vea el estado actual del ATU de un vistazo.
4. **Botones de acción** — TUNE, MOX, ATU y MEM para el control del transmisor y del sintonizador.
5. **APD** — alterne la Predistorsión Adaptativa y monitoree su estado de calibración.

Ninguna de las configuraciones de Controles TX es persistida por AetherSDR; los valores siguen el estado actual de la radio.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango / Estados | Qué hace |
|---|---|---|---|---|
| **RF Pwr** | Medidor | — | 0–120 W; rojo por encima de 100 W (sin amplificador) / 0–600 W; rojo por encima de 500 W (Aurora 500W) | Muestra la potencia directa en la salida del excitador. La escala cambia automáticamente según el modelo de radio. Incluye una barra de retención de pico que mantiene la lectura PEP más alta durante 2 segundos y luego decae al valor suavizado actual. El pico se restablece a cero inmediatamente cuando el transmisor se desactiva. |
| **SWR** | Medidor | — | 1.0–3.0; rojo por encima de 2.5 | Muestra la relación de onda estacionaria en el excitador. |
| **RF Power** | Deslizador | 100 | 0–100 | Establece el nivel de potencia de transmisión RF. |
| **Tune Pwr** | Deslizador | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía. |
| **TX Profile** | Menú desplegable | — | Poblado desde la radio | Selecciona y carga un perfil de transmisión de la lista de perfiles de la radio. |
| **Success** | Indicador | Apagado | Apagado / verde | Se enciende en verde cuando el ATU reporta un resultado de sintonía exitoso u OK. |
| **Byp** | Indicador | Apagado | Apagado / naranja | Se enciende en naranja cuando el ATU está en Bypass o ManualBypass. |
| **Mem** | Indicador | Apagado | Apagado / verde | Se enciende en verde cuando el ATU está recuperando una memoria guardada. |
| **TUNE** | Botón | — | TUNE / TUNING... | Inicia una portadora de sintonía. La etiqueta cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic nuevamente para detener. Haga clic derecho para abrir el Menú contextual de sintonía y seleccionar la forma de la portadora. |
| **MOX** | Botón de alternancia | — | Apagado / encendido (rojo) | Alterna la transmisión manual. El botón se vuelve rojo mientras el transmisor está activado. En v0.9.7, al hacer clic en MOX, la solicitud se enruta a través del coordinador de tonos Quindar, por lo que los tonos K/BK se reproducen al presionar y soltar PTT en modos de voz cuando Quindar está habilitado en la tira de canales de audio. Consulte [MOX y tonos Quindar](#mox-y-tonos-quindar) a continuación. |
| **ATU** | Botón | — | — | Inicia un ciclo de sintonía del ATU o cambia el sintonizador a bypass, dependiendo del estado actual y la frecuencia. Consulte [Comportamiento del botón ATU](#comportamiento-del-botón-atu) a continuación. Deshabilitado cuando TGXL está en modo OPERATE. Haga clic derecho para abrir el Menú contextual del ATU. |
| **MEM** | Botón de alternancia | — | Apagado / encendido | Activa o desactiva la recuperación de memoria del ATU. Deshabilitado cuando TGXL está en modo OPERATE. |
| **APD** | Botón de alternancia | — | Apagado / encendido | Activa o desactiva la Predistorsión Adaptativa en la radio. |
| **Active** | Indicador | Apagado | Apagado / verde | Se enciende cuando APD está activado y el ecualizador se aplica activamente. |
| **Cal** | Indicador | Apagado | Apagado / verde | Se enciende cuando APD está activado y aún está calibrando. |
| **Avail** | Indicador | Apagado | Apagado / verde | Se enciende cuando APD está activado y hay una calibración disponible pero aún no aplicada. |

### Comportamiento del botón ATU

El botón **ATU** alterna entre iniciar un ciclo de sintonía y poner el sintonizador en bypass, siguiendo el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o cualquier clic después de un cambio de frecuencia)** — inicia un nuevo ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia** — si el ATU reporta una coincidencia exitosa u OK y usted no ha cambiado de frecuencia desde que finalizó esa sintonía, hacer clic en **ATU** nuevamente cambia el sintonizador a bypass.
- **Después de un bypass** — el registro de frecuencia sintonizada se borra. El siguiente clic siempre inicia un nuevo ciclo de sintonía.

Si cambia de frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonía independientemente del estado anterior del ATU.

### Menú contextual del ATU

Haga clic derecho en el botón **ATU** para abrir el menú contextual del ATU con las siguientes opciones:

- **Pre-tune bands…** — Abre el diálogo de Barrido de presintonía. Esta opción solo está disponible cuando las memorias del ATU (MEM) están habilitadas. Si están deshabilitadas, un tooltip explica que MEM debe estar habilitado primero.
- **Clear ATU memories…** — Abre un diálogo de confirmación. Haga clic en **Yes** para borrar todas las memorias almacenadas del ATU en la radio.

### Menú contextual de sintonía

Haga clic derecho en el botón **TUNE** para abrir el menú contextual de sintonía. Esto le permite elegir la forma de la portadora para el próximo ciclo de sintonía. El menú ofrece dos opciones:

- **Mono Tone** — Un tono de portadora único.
- **Two Tone** — Dos tonos simultáneos (típicamente usados para pruebas de IMD).

Seleccionar cualquiera de las opciones la aplica inmediatamente para el próximo ciclo de sintonía. Esta es una configuración de un solo uso: no se guarda en AppSettings, y la radio vuelve a su modo de sintonía predeterminado al reiniciarse. El modo actualmente activo se muestra con una marca de verificación.

### MOX y tonos Quindar

A partir de v0.9.7, al hacer clic en **MOX**, la solicitud PTT se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Cuando Quindar está habilitado en la tira de canales de audio:

- **Activación (MOX encendido)** — el tono K se reproduce antes de que el transmisor se active.
- **Desactivación (MOX apagado)** — el tono BK se reproduce después de que el transmisor se desactive.

Este comportamiento se aplica solo a modos de voz. En modos que no son de voz, o cuando Quindar está deshabilitado en la tira de canales de audio, MOX activa el transmisor inmediatamente como antes.

### Progresión del estado de APD

APD pasa por tres estados en secuencia: **Cal** (calibrando) → **Avail** (calibración lista, aún no aplicada) → **Active** (ecualizador aplicado a la señal transmitida).

## Applet ShackSwitch

V0.9.4 añade soporte para el dispositivo ShackSwitch. Cuando se detecta un ShackSwitch, el Panel de applets muestra su botón de bandeja (**SS**) y el applet automáticamente. Ambos están ocultos cuando no hay ningún dispositivo ShackSwitch presente. No se requiere configuración manual para mostrar u ocultar este applet.

## Consejos

- Mantenga **Tune Pwr** bajo (el valor predeterminado es 10) para evitar estresar la antena o el amplificador durante la sintonía del ATU.
- Observe el medidor **SWR** después de un ciclo de sintonía. El indicador **Success** confirma que el ATU encontró una coincidencia, pero el medidor SWR le muestra el resultado real.
- La escala del medidor **RF Pwr** cambia automáticamente entre 0–120 W (FLEX-8600 sin amplificador) y 0–600 W (Aurora 500W); el umbral rojo se ajusta en consecuencia.
- El medidor **RF Pwr** incluye una barra de retención de pico que mantiene la lectura PEP más alta durante 2 segundos y luego decae gradualmente. Esto se restablece inmediatamente cuando desactiva el transmisor.
- Use el menú contextual de clic derecho en **TUNE** para cambiar entre portadoras de sintonía Mono Tone y Two Tone para fines de prueba.
- Después de una sintonía exitosa, hacer clic en **ATU** una segunda vez en la misma frecuencia pone el sintonizador en bypass. Para resintonizar, cambie de frecuencia o haga clic en **ATU** nuevamente después del bypass.
- Haga clic derecho en **ATU** para acceder a las funciones de Barrido de presintonía y Borrar memorias del ATU.
- Si usa **MOX** en un modo de voz con Quindar habilitado, permita que el tono K termine antes de hablar. El transmisor no se activa hasta que el tono se completa.

## Relacionados

- [Set RF output power](set-rf-output-power.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- [Switch TX profiles (e.g. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Run the internal ATU](run-the-internal-atu.md)
- [Recall an ATU memory](recall-an-atu-memory.md)
- [Enable APD to linearise the transmitter](enable-apd-to-linearise-the-transmitter.md)
- [Run a Two-Tone Tune](run-a-two-tone-tune.md)
- [Make your first QSO with AetherSDR](../../getting-started/tutorials/first-qso.md)
- [Pre-tune ATU memories](pre-tune-atu-memories.md)
- [Clear ATU memories](clear-atu-memories.md)
<!-- docmesh:llm version=v26.5.2.1 date=2026-05-01 -->
