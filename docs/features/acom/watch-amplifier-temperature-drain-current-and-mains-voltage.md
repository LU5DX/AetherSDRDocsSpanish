# Vigile la temperatura del amplificador, la corriente de drenaje y la tensión de red

Supervise la telemetría de salud de su amplificador lineal ACOM — temperatura, corriente de drenaje y tensión de red — para detectar problemas de refrigeración, fallos en la fuente de alimentación o condiciones de funcionamiento anormales antes de que causen daños.

## Antes de comenzar

- Su amplificador ACOM debe estar conectado a AetherSDR mediante serial o TCP.
- AetherSDR debe estar conectado a una radio FLEX-8600.

## Pasos

1. Abra el **Applet panel** en la parte inferior de la ventana de AetherSDR.
2. Haga clic en el mosaico **ACOM**.
3. Lea los indicadores de **Temperature**, **Drain Current** y **Mains Voltage** en el panel del Applet ACOM.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Forward Power** | Lectura de potencia directa en tiempo real desde el amplificador. |
| **SWR** | Lectura de ROE en tiempo real. |
| **Temperature / Drain Current / Mains Voltage** | Lecturas de telemetría de salud del amplificador. |
| **Operate / Standby** | Alterna el amplificador entre los modos Operate y Standby. El valor predeterminado es Standby. |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Operate/Standby state** | Operate, Standby, Fault | Modo de funcionamiento actual del amplificador. |

## Consejos

- Lecturas de temperatura altas pueden indicar refrigeración insuficiente — verifique el funcionamiento del ventilador y el flujo de aire alrededor del amplificador.
- Valores inusuales de corriente de drenaje o tensión de red pueden señalar problemas en la fuente de alimentación o degradación de componentes.

## Relacionado

- [Descripción general del amplificador ACOM](overview.md)
- [Vigile la potencia directa y la ROE en la salida del amplificador](../amp/monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Ponga el amplificador en modo Operate o Standby](put-the-amplifier-in-operate-or-standby.md)
