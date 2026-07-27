# Monitorear la temperatura, corriente de drenaje y tensión de red del amplificador

Supervise la telemetría de estado de su amplificador lineal ACOM — temperatura, corriente de drenaje y tensión de red — para detectar problemas de refrigeración, fallos en la fuente de alimentación o condiciones de funcionamiento anómalas antes de que causen daños.

## Antes de comenzar

- Su amplificador ACOM debe estar conectado a AetherSDR mediante puerto serie o TCP.
- AetherSDR debe estar conectado a una radio FLEX-8600.

## Pasos

1. Abra el **Applet panel** en la parte inferior de la ventana de AetherSDR.
2. Haga clic en el mosaico **ACOM**.
3. Lea los indicadores de **Temperature**, **Drain Current** y **Mains Voltage** en el panel del Applet ACOM.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Temperature** | Lectura de temperatura en tiempo real desde los sensores internos del amplificador. |
| **Drain Current** | Corriente de drenaje en tiempo real que consume la etapa final del amplificador. |
| **Mains Voltage** | Tensión de red CA en tiempo real suministrada al amplificador. |

Estos tres valores se actualizan continuamente cuando el amplificador se comunica con AetherSDR.

## Consejos

- Lecturas altas de temperatura pueden indicar refrigeración insuficiente — verifique el funcionamiento del ventilador y el flujo de aire alrededor del amplificador.
- Valores inusuales de corriente de drenaje o tensión de red pueden señalar problemas en la fuente de alimentación o degradación de componentes.

## Relacionado

- [Descripción general del amplificador ACOM](overview.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](../amp/monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Poner el amplificador en Operate o Standby](put-the-amplifier-in-operate-or-standby.md)
