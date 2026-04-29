# Descripción general de TX Controls

El applet TX Controls le da acceso directo a todas las funciones de transmisión: monitoreo de potencia directa y ROS, ajuste de niveles de salida, selección de un perfil de TX, activación del transmisor, ejecución del ATU y habilitación de la Predistorsión Adaptativa. Todos estos controles están agrupados en un solo lugar en el Panel de Applets.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. TX Controls requiere una conexión de radio activa.
- Asegúrese de que el Panel de Applets sea visible. Si no lo es, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

TX Controls está siempre presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de bandeja **TX** en la barra lateral derecha.

El applet está organizado en filas de arriba a abajo:

1. **Meters** — lecturas en tiempo real de potencia directa de RF y ROS.
2. **Power sliders** — ajuste los niveles de potencia de transmisión y de portadora de ajuste antes de activar el transmisor.
3. **Profile and ATU status** — elija un perfil de TX y vea el estado actual del ATU de un vistazo.
4. **Action buttons** — TUNE, MOX, ATU y MEM para el control de transmisión y del sintonizador.
5. **APD** — alterne la Predistorsión Adaptativa y monitoree su estado de calibración.

Ninguno de los ajustes de TX Controls es guardado de forma permanente por AetherSDR; los valores siguen el estado actual de la radio.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango / Estados | Qué hace |
|---|---|---|---|---|
| **RF Pwr** | Medidor | — | 0–120 W; rojo por encima de 100 W (sin amplificador) / 0–600 W; rojo por encima de 500 W (Aurora 500W) | Muestra la potencia directa en la salida del excitador. La escala cambia automáticamente según el modelo de radio. |
| **SWR** | Medidor | — | 1.0–3.0; rojo por encima de 2.5 | Muestra la relación de onda estacionaria en el excitador. |
| **RF Power** | Control deslizante | 100 | 0–100 | Establece el nivel de potencia de RF de transmisión. |
| **Tune Pwr** | Control deslizante | 10 | 0–100 | Establece el nivel de potencia de la portadora de ajuste. |
| **TX Profile** | Lista desplegable | — | Poblada desde la radio | Selecciona y carga un perfil de transmisión de la lista de perfiles de la radio. |
| **Success** | Indicador | Apagado | Apagado / verde | Se ilumina en verde cuando el ATU reporta un resultado de ajuste exitoso u OK. |
| **Byp** | Indicador | Apagado | Apagado / naranja | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. |
| **Mem** | Indicador | Apagado | Apagado / verde | Se ilumina en verde cuando el ATU está recuperando una memoria guardada. |
| **TUNE** | Botón | — | TUNE / TUNING... | Inicia una portadora de ajuste. La etiqueta cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic de nuevo para detenerlo. |
| **MOX** | Botón de alternancia | — | Apagado / encendido (rojo) | Alterna la transmisión manual. El botón se vuelve rojo mientras el transmisor está activado. |
| **ATU** | Botón | — | — | Inicia el ciclo de sintonización del ATU interno. Deshabilitado cuando TGXL está en modo OPERATE. |
| **MEM** | Botón de alternancia | — | Apagado / encendido | Activa o desactiva la recuperación de memoria del ATU. Deshabilitado cuando TGXL está en modo OPERATE. |
| **APD** | Botón de alternancia | — | Apagado / encendido | Activa o desactiva la Predistorsión Adaptativa en la radio. |
| **Active** | Indicador | Apagado | Apagado / verde | Se ilumina cuando APD está encendido y el ecualizador está aplicado activamente. |
| **Cal** | Indicador | Apagado | Apagado / verde | Se ilumina cuando APD está encendido y aún está calibrando. |
| **Avail** | Indicador | Apagado | Apagado / verde | Se ilumina cuando APD está encendido y hay una calibración disponible pero aún no aplicada. |

### Progresión de estados de APD

APD avanza a través de tres estados en secuencia: **Cal** (calibrando) → **Avail** (calibración lista, aún no aplicada) → **Active** (ecualizador aplicado a la señal transmitida).

## Consejos

- Mantenga **Tune Pwr** bajo (el valor predeterminado es 10) para evitar esforzar la antena o el amplificador durante la sintonización del ATU.
- Observe el medidor **SWR** después de un ciclo de ajuste. El indicador **Success** confirma que el ATU encontró una coincidencia, pero el medidor de ROS le muestra el resultado real.
- La escala del medidor **RF Pwr** cambia automáticamente entre 0–120 W (FLEX-8600 sin amplificador) y 0–600 W (Aurora 500W); el umbral rojo se ajusta en consecuencia.

## Temas relacionados

- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Ajustar la potencia de la portadora de ajuste](set-tune-carrier-power.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Iniciar una portadora de ajuste para verificar el ROS](start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Habilitar APD para linealizar el transmisor](enable-apd-to-linearise-the-transmitter.md)
- [Realizar un ajuste de dos tonos](run-a-two-tone-tune.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
