# Descripción general del amplificador ACOM

El applet ACOM Amplifier le permite monitorear y controlar un amplificador lineal ACOM conectado por puerto serial o TCP. Proporciona telemetría en tiempo real y control básico del modo de operación, con seguimiento automático de banda cuando se sintoniza la radio.

## Cómo funciona

El applet se comunica con un amplificador ACOM a través de una conexión serial o TCP. Una vez conectado, recibe continuamente datos de telemetría del amplificador y los muestra en tiempo real. El applet también envía comandos de cambio de banda al amplificador cuando usted cambia la frecuencia en la radio, manteniendo la selección de banda del amplificador sincronizada.

## Cómo abrir el applet ACOM Amplifier

1. Localice la bandeja del Applet Panel en la ventana principal.
2. Haga clic en el mosaico ACOM para abrir el applet ACOM Amplifier.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento |
|---------|------|----------------|----------------|
| Forward Power | indicador | — | Lectura de potencia directa en tiempo real desde el amplificador. |
| SWR | indicador | — | Lectura de ROE en tiempo real. |
| Temperature / Drain Current / Mains Voltage | indicador | — | Lecturas de telemetría del estado del amplificador. |
| Operate / Standby | botón pulsador | Standby | Alterna el amplificador entre los modos Operate y Standby. |

## Cómo entender el indicador Operate/Standby

El botón pulsador Operate/Standby también funciona como indicador. Su estado codificado por colores muestra el modo de operación actual del amplificador:

| Estado | Significado |
|--------|-------------|
| Operate | El amplificador está en modo Operate. |
| Standby | El amplificador está en modo Standby. |
| Fault | El amplificador ha informado una condición de falla. |

## Relacionado

- [Monitor forward power and SWR at the amplifier output](../amp/monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Put the amplifier in Operate or Standby](put-the-amplifier-in-operate-or-standby.md)
- [Watch amplifier temperature, drain current and mains voltage](watch-amplifier-temperature-drain-current-and-mains-voltage.md)
