# Descripción general de TX Controls

El applet TX Controls le brinda acceso directo a todas las funciones de transmisión: supervisión de potencia directa y ROS, ajuste de niveles de salida, selección de perfil de TX, activación del transmisor, operación del ATU y habilitación de la Predistorsión Adaptativa (APD). Todos estos controles están agrupados en un solo lugar en el Panel de Applets.

## Antes de comenzar

- Conecte un radio FLEX-8600. TX Controls requiere una conexión de radio activa.
- Asegúrese de que el Panel de Applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

TX Controls está siempre presente en el Panel de Applets (barra lateral derecha). Active o desactive su visibilidad con el botón de bandeja **TX** en la barra lateral derecha.

El applet está organizado en filas de arriba a abajo:

1. **Meters** — lecturas en tiempo real de potencia directa de RF y ROS.
2. **Power sliders** — ajuste los niveles de potencia de transmisión y portadora de sintonía antes de activar el transmisor.
3. **Profile and ATU status** — elija un perfil de TX y vea el estado actual del ATU de un vistazo.
4. **Action buttons** — TUNE, MOX, ATU y MEM para el control de transmisión y del sintonizador.
5. **APD** — active o desactive la Predistorsión Adaptativa y supervise su estado de calibración.

Ninguno de los ajustes de TX Controls es guardado por AetherSDR; los valores siguen el estado actual del radio.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango / Estados | Función |
|---|---|---|---|---|
| **RF Pwr** | Medidor | — | 0–120 W; rojo por encima de 100 W (sin amplificador) / 0–600 W; rojo por encima de 500 W (Aurora 500W) | Muestra la potencia directa en la salida del excitador. La escala cambia automáticamente según el modelo de radio. |
| **SWR** | Medidor | — | 1.0–3.0; rojo por encima de 2.5 | Muestra la relación de onda estacionaria (ROS) en el excitador. |
| **RF Power** | Control deslizante | 100 | 0–100 | Ajusta el nivel de potencia de RF en transmisión. |
| **Tune Pwr** | Control deslizante | 10 | 0–100 | Ajusta el nivel de potencia de la portadora de sintonía. |
| **TX Profile** | Lista desplegable | — | Obtenida del radio | Selecciona y carga un perfil de transmisión de la lista de perfiles del radio. |
| **Success** | Indicador | Apagado | Apagado / verde | Se enciende en verde cuando el ATU informa un resultado de sintonía exitoso o aceptable. |
| **Byp** | Indicador | Apagado | Apagado / naranja | Se enciende en naranja cuando el ATU está en modo Bypass o ManualBypass. |
| **Mem** | Indicador | Apagado | Apagado / verde | Se enciende en verde cuando el ATU está recuperando una memoria guardada. |
| **TUNE** | Botón | — | TUNE / TUNING... | Inicia una portadora de sintonía. La etiqueta cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic nuevamente para detener. |
| **MOX** | Botón de alternancia | — | Apagado / encendido (rojo) | Activa o desactiva la transmisión manual. El botón se pone rojo mientras el transmisor está activado. |
| **ATU** | Botón | — | — | Inicia un ciclo de sintonía del ATU o cambia el sintonizador a bypass, según el estado actual y la frecuencia. Consulte [comportamiento del botón ATU](#atu-button-behaviour) más abajo. Se desactiva cuando el TGXL está en modo OPERATE. |
| **MEM** | Botón de alternancia | — | Apagado / encendido | Activa o desactiva la recuperación de memoria del ATU. Se desactiva cuando el TGXL está en modo OPERATE. |
| **APD** | Botón de alternancia | — | Apagado / encendido | Activa o desactiva la Predistorsión Adaptativa en el radio. |
| **Active** | Indicador | Apagado | Apagado / verde | Encendido cuando APD está activo y el ecualizador se aplica activamente. |
| **Cal** | Indicador | Apagado | Apagado / verde | Encendido cuando APD está activo y aún se está calibrando. |
| **Avail** | Indicador | Apagado | Apagado / verde | Encendido cuando APD está activo y hay una calibración disponible pero aún no aplicada. |

### Comportamiento del botón ATU

El botón **ATU** alterna entre iniciar un ciclo de sintonía y poner el sintonizador en bypass, siguiendo el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o cualquier clic tras un cambio de frecuencia)** — inicia un nuevo ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia** — si el ATU informa una coincidencia exitosa o aceptable y no ha cambiado de frecuencia desde que finalizó esa sintonía, al hacer clic en **ATU** nuevamente se pone el sintonizador en bypass.
- **Después de un bypass** — el registro de la frecuencia sintonizada se borra. El siguiente clic siempre inicia un nuevo ciclo de sintonía.

Si cambia de frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonía independientemente del estado anterior del ATU.

### Progresión de estados de APD

APD avanza a través de tres estados en secuencia: **Cal** (calibrando) → **Avail** (calibración lista, aún no aplicada) → **Active** (ecualizador aplicado a la señal transmitida).

## Applet ShackSwitch

La versión V0.9.4 añade compatibilidad con el dispositivo ShackSwitch. Cuando se detecta un ShackSwitch, el Panel de Applets muestra automáticamente su botón de bandeja (**SS**) y el applet correspondiente. Ambos se ocultan cuando no hay ningún dispositivo ShackSwitch presente. No se requiere configuración manual para mostrar u ocultar este applet.

## Consejos

- Mantenga **Tune Pwr** bajo (el valor predeterminado es 10) para evitar estresar la antena o el amplificador durante la sintonía del ATU.
- Observe el medidor **SWR** después de un ciclo de sintonía. El indicador **Success** confirma que el ATU encontró una coincidencia, pero el medidor de ROS muestra el resultado real.
- La escala del medidor **RF Pwr** cambia automáticamente entre 0–120 W (FLEX-8600 sin amplificador) y 0–600 W (Aurora 500W); el umbral de color rojo se ajusta en consecuencia.
- Tras una sintonía exitosa, hacer clic en **ATU** por segunda vez en la misma frecuencia pone el sintonizador en bypass. Para resintonizar, cambie de frecuencia o haga clic en **ATU** nuevamente después del bypass.

## Relacionado

- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Ajustar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Iniciar una portadora de sintonía para verificar la ROS](start-a-tune-carrier-to-check-swr.md)
- [Activar MOX para accionar el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Operar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Habilitar APD para linealizar el transmisor](enable-apd-to-linearise-the-transmitter.md)
- [Realizar una sintonía de dos tonos](run-a-two-tone-tune.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
<!-- docmesh:llm version=V0.9.5.1 date=2026-05-01 -->
