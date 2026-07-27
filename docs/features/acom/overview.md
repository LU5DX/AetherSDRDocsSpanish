# Resumen del amplificador ACOM

El applet del amplificador ACOM le permite supervisar y controlar un amplificador lineal ACOM conectado mediante puerto serie o TCP. Proporciona telemetría en tiempo real y control básico del modo de operación, con seguimiento automático de banda cuando se sintoniza la radio.

## Cómo funciona

El applet se comunica con un amplificador ACOM a través de una conexión serie o TCP. Una vez conectado, recibe continuamente datos de telemetría del amplificador y los muestra en tiempo real. El applet también envía comandos de cambio de banda al amplificador cuando usted cambia de frecuencia en la radio, manteniendo sincronizada la selección de banda del amplificador.

## Abrir el applet del amplificador ACOM

1. Localice la bandeja del panel de applets en la ventana principal.
2. Haga clic en el mosaico ACOM para abrir el applet del amplificador ACOM.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---------|------|----------------------|---------------|
| Forward Power | indicador | — | Lectura de potencia directa en tiempo real desde el amplificador. |
| SWR | indicador | — | Lectura de ROE en tiempo real. |
| Temperature / Drain Current / Mains Voltage | indicador | — | Lecturas de telemetría del estado del amplificador. |
| Operate / Standby | botón pulsador | Standby | Alterna el amplificador entre los modos Operate y Standby. El indicador muestra el estado actual: Operate, Standby o Fault. |

## Relacionados

- [Supervisar la potencia directa y la ROE en la salida del amplificador](../amp/monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Poner el amplificador en modo Operate o Standby](put-the-amplifier-in-operate-or-standby.md)
- [Observar la temperatura, la corriente de drenaje y la tensión de red del amplificador](watch-amplifier-temperature-drain-current-and-mains-voltage.md)
