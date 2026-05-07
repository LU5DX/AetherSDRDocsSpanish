# Resumen de controles de TX

El applet Controles de TX le proporciona acceso directo a todas las funciones de transmisión: monitoreo de potencia directa y ROE, ajuste de niveles de salida, selección de un perfil de TX, activación del transmisor, ejecución del ATU y habilitación de la Predistorsión Adaptativa. Todos estos controles están agrupados en un solo lugar en el Panel de Applets.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. Los Controles de TX requieren una conexión de radio activa.
- Asegúrese de que el Panel de Applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

Controles de TX está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de bandeja **TX** en la barra lateral derecha.

El applet está organizado en filas de arriba a abajo:

1.  **Medidores** — lecturas en tiempo real de potencia directa de RF y ROE.
2.  **Deslizadores de potencia** — ajuste los niveles de potencia de transmisión y de portadora de sintonía antes de activar la transmisión.
3.  **Estado del perfil y del ATU** — elija un perfil de TX y vea el estado actual del ATU de un vistazo.
4.  **Botones de acción** — TUNE, MOX, ATU y MEM para el control del transmisor y del sintonizador.
5.  **APD** — active o desactive la Predistorsión Adaptativa y supervise su estado de calibración.

Ninguna de las configuraciones de Controles de TX es persistida por AetherSDR; los valores siguen el estado actual de la radio.

## Función de cada control

| Control | Tipo | Valor predeterminado | Rango / Estados | Función |
|---|---|---|---|---|
| **RF Pwr** | Medidor | — | 0–120 W; rojo por encima de 100 W (sin amplificador) / 0–600 W; rojo por encima de 500 W (Aurora 500W) | Muestra la potencia directa en la salida del excitador. La escala cambia automáticamente según el modelo de radio. |
| **SWR** | Medidor | — | 1.0–3.0; rojo por encima de 2.5 | Muestra la relación de onda estacionaria en el excitador. |
| **RF Power** | Deslizador | 100 | 0–100 | Establece el nivel de potencia de RF de transmisión. |
| **Tune Pwr** | Deslizador | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía. |
| **TX Profile** | Menú desplegable | — | Poblado desde la radio | Selecciona y carga un perfil de transmisión de la lista de perfiles de la radio. |
| **Success** | Indicador | Apagado | Apagado / verde | Se ilumina en verde cuando el ATU reporta un resultado de sintonía exitoso u OK. |
| **Byp** | Indicador | Apagado | Apagado / naranja | Se ilumina en naranja cuando el ATU está en modo Bypass o ManualBypass. |
| **Mem** | Indicador | Apagado | Apagado / verde | Se ilumina en verde cuando el ATU está recordando una memoria guardada. |
| **TUNE** | Botón | — | TUNE / TUNING... | Inicia una portadora de sintonía. La etiqueta cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic de nuevo para detener. |
| **MOX** | Botón de alternancia | — | Apagado / encendido (rojo) | Alterna la transmisión manual. El botón se vuelve rojo mientras el transmisor está activado. En v0.9.7, al hacer clic en MOX se enruta a través del coordinador de tonos Quindar, por lo que los tonos K/BK se reproducen al activar y desactivar PTT en modos de fonía cuando Quindar está habilitado en la tira de canales de audio. Consulte [MOX y tonos Quindar](#mox-y-tonos-quindar) a continuación. |
| **ATU** | Botón | — | — | Inicia un ciclo de sintonía del ATU o cambia el sintonizador a bypass, dependiendo del estado actual y la frecuencia. Consulte [Comportamiento del botón ATU](#comportamiento-del-botón-atu) a continuación. Deshabilitado cuando el TGXL está en modo OPERATE. |
| **MEM** | Botón de alternancia | — | Apagado / encendido | Activa o desactiva el recuerdo de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. |
| **APD** | Botón de alternancia | — | Apagado / encendido | Activa o desactiva la Predistorsión Adaptativa en la radio. |
| **Active** | Indicador | Apagado | Apagado / verde | Iluminado cuando APD está activada y el ecualizador se aplica activamente. |
| **Cal** | Indicador | Apagado | Apagado / verde | Iluminado cuando APD está activada y aún se está calibrando. |
| **Avail** | Indicador | Apagado | Apagado / verde | Iluminado cuando APD está activada y hay una calibración disponible pero aún no aplicada. |

### Comportamiento del botón ATU

El botón **ATU** alterna entre iniciar un ciclo de sintonía y poner el sintonizador en bypass, coincidiendo con el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o cualquier clic después de un cambio de frecuencia)** — inicia un nuevo ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia** — si el ATU reporta una coincidencia exitosa u OK y no ha cambiado de frecuencia desde que finalizó esa sintonía, al hacer clic en **ATU** de nuevo se cambia el sintonizador a bypass.
- **Después de un bypass** — el registro de frecuencia sintonizada se borra. El siguiente clic siempre inicia un nuevo ciclo de sintonía.

Si cambia de frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonía, independientemente del estado anterior del ATU.

### MOX y tonos Quindar

A partir de v0.9.7, al hacer clic en **MOX** se enruta la solicitud de PTT a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Cuando Quindar está habilitado en la tira de canales de audio:

- **Activación (MOX encendido)** — el tono K se reproduce antes de que el transmisor se active.
- **Desactivación (MOX apagado)** — el tono BK se reproduce después de que el transmisor se desactive.

Este comportamiento se aplica solo a modos de fonía. En modos que no son de fonía, o cuando Quindar está deshabilitado en la tira de canales de audio, MOX activa el transmisor inmediatamente como antes.

### Progresión del estado de APD

APD pasa por tres estados en secuencia: **Cal** (calibrando) → **Avail** (calibración lista, aún no aplicada) → **Active** (ecualizador aplicado a la señal transmitida).

## Applet ShackSwitch

La v0.9.4 añade soporte para el dispositivo ShackSwitch. Cuando se detecta un ShackSwitch, el Panel de Applets muestra su botón de bandeja (**SS**) y el applet automáticamente. Ambos están ocultos cuando no hay ningún dispositivo ShackSwitch presente. No se requiere configuración manual para mostrar u ocultar este applet.

## Consejos

- Mantenga **Tune Pwr** bajo (el valor predeterminado es 10) para evitar estresar la antena o el amplificador durante la sintonía del ATU.
- Observe el medidor de **SWR** después de un ciclo de sintonía. El indicador **Success** confirma que el ATU encontró una coincidencia, pero el medidor de SWR le muestra el resultado real.
- La escala del medidor de **RF Pwr** cambia automáticamente entre 0–120 W (FLEX-8600 sin amplificador) y 0–600 W (Aurora 500W); el umbral rojo se ajusta en consecuencia.
- Después de una sintonía exitosa, al hacer clic en **ATU** una segunda vez en la misma frecuencia se pone el sintonizador en bypass. Para volver a sintonizar, cambie de frecuencia o haga clic en **ATU** de nuevo después del bypass.
- Si usa **MOX** en un modo de fonía con Quindar habilitado, permita que el tono K termine antes de hablar. El transmisor no se activa hasta que el tono se completa.

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
<!-- docmesh:llm version=V0.9.7 date=2026-05-01 -->
