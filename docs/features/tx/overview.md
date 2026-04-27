# Descripción general de los controles de TX

El applet TX Controls le da acceso directo a todas las funciones de transmisión: monitoreo de potencia directa y ROS, ajuste de niveles de salida, selección de perfil de TX, activación del transmisor, ejecución del ATU y habilitación de la pré-distorsión adaptativa. Todos estos controles están agrupados en un mismo lugar dentro del Panel de Applets.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. TX Controls requiere una conexión de radio activa.
- Asegúrese de que el Panel de Applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

TX Controls siempre está presente en el Panel de Applets (barra lateral derecha). Alterne su visibilidad con el botón de bandeja **TX** en la barra lateral derecha.

El applet está organizado en filas de arriba hacia abajo:

1. **Meters** — lecturas en tiempo real de potencia directa de RF y ROS.
2. **Power sliders** — ajuste los niveles de potencia de transmisión y de portadora de sintonía antes de activar la transmisión.
3. **Profile and ATU status** — elija un perfil de TX y consulte el estado actual del ATU de un vistazo.
4. **Action buttons** — TUNE, MOX, ATU y MEM para el control del transmisor y el sintonizador.
5. **APD** — active o desactive la Pré-distorsión Adaptativa y monitoree su estado de calibración.

Ninguno de los ajustes de TX Controls es guardado por AetherSDR; los valores siguen el estado actual de la radio.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango / Estados | Función |
|---|---|---|---|---|
| **RF Pwr** | Medidor | — | 0–120 W; rojo por encima de 100 W (sin amplificador) / 0–600 W; rojo por encima de 500 W (Aurora 500W) | Muestra la potencia directa en la salida del excitador. La escala cambia automáticamente según el modelo de radio. |
| **SWR** | Medidor | — | 1.0–3.0; rojo por encima de 2.5 | Muestra la relación de onda estacionaria en el excitador. |
| **RF Power** | Control deslizante | 100 | 0–100 | Establece el nivel de potencia de RF para la transmisión. |
| **Tune Pwr** | Control deslizante | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía. |
| **TX Profile** | Lista desplegable | — | Poblada desde la radio | Selecciona y carga un perfil de transmisión desde la lista de perfiles de la radio. |
| **Success** | Indicador | Apagado | Apagado / verde | Se ilumina en verde cuando el ATU reporta un resultado de sintonía exitoso o correcto. |
| **Byp** | Indicador | Apagado | Apagado / naranja | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. |
| **Mem** | Indicador | Apagado | Apagado / verde | Se ilumina en verde cuando el ATU está recuperando una memoria guardada. |
| **TUNE** | Botón | — | TUNE / TUNING... | Inicia una portadora de sintonía. La etiqueta cambia a "TUNING..." con fondo rojo mientras está activa. Haga clic de nuevo para detenerla. |
| **MOX** | Botón de alternancia | — | Desactivado / activado (rojo) | Alterna la transmisión manual. El botón se vuelve rojo mientras el transmisor está activo. |
| **ATU** | Botón | — | — | Inicia el ciclo de sintonía del ATU interno. Deshabilitado cuando TGXL está en modo OPERATE. |
| **MEM** | Botón de alternancia | — | Desactivado / activado | Activa o desactiva la recuperación de memoria del ATU. Deshabilitado cuando TGXL está en modo OPERATE. |
| **APD** | Botón de alternancia | — | Desactivado / activado | Activa o desactiva la Pré-distorsión Adaptativa en la radio. |
| **Active** | Indicador | Apagado | Apagado / verde | Se ilumina cuando APD está activado y el ecualizador está aplicado activamente. |
| **Cal** | Indicador | Apagado | Apagado / verde | Se ilumina cuando APD está activado y aún está calibrando. |
| **Avail** | Indicador | Apagado | Apagado / verde | Se ilumina cuando APD está activado y hay una calibración disponible pero aún no aplicada. |

### Progresión de estados de APD

APD avanza por tres estados en secuencia: **Cal** (calibrando) → **Avail** (calibración lista, aún no aplicada) → **Active** (ecualizador aplicado a la señal transmitida).

## Consejos

- Mantenga **Tune Pwr** bajo (el valor predeterminado es 10) para evitar sobrecargar la antena o el amplificador durante la sintonía del ATU.
- Observe el medidor **SWR** después de un ciclo de sintonía. El indicador **Success** confirma que el ATU encontró una coincidencia, pero el medidor SWR le muestra el resultado real.
- La escala del medidor **RF Pwr** cambia automáticamente entre 0–120 W (FLEX-8600 sin amplificador) y 0–600 W (Aurora 500W); el umbral de color rojo se ajusta en consecuencia.

## Temas relacionados

- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Ajustar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Iniciar una portadora de sintonía para verificar el ROS](start-a-tune-carrier-to-check-swr.md)
- [Activar MOX para transmitir manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Habilitar APD para linealizar el transmisor](enable-apd-to-linearise-the-transmitter.md)
- [Ejecutar una sintonía de dos tonos](run-a-two-tone-tune.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
