# Supervise la salud del amplificador y encadene amplificadores

Supervise la telemetría en tiempo real del amplificador lineal ACOM y controle su modo de operación desde AetherSDR.

## Antes de comenzar

- La radio debe estar conectada a AetherSDR.
- Un amplificador ACOM debe estar conectado y comunicándose (serial o TCP) con AetherSDR.

## Pasos

1. Abra el **Applet panel**.
2. Haga clic en el mosaico **ACOM** para abrir el applet ACOM Amplifier.

El applet muestra las siguientes lecturas en tiempo real:

- **Forward Power** — potencia directa en tiempo real a la salida del amplificador.
- **SWR** — relación de onda estacionaria en tiempo real a la salida del amplificador.
- **Temperature / Drain Current / Mains Voltage** — telemetría de salud del amplificador.

## Seleccione el modo de operación del amplificador

1. En el applet ACOM Amplifier, haga clic en **Operate** para colocar el amplificador en modo Operate (transmisión activa).
2. Haga clic en **Standby** para colocar el amplificador en modo Standby (derivado o en espera).

El indicador **Operate/Standby state** debajo de los botones muestra el modo actual: Operate, Standby o Fault. El botón del modo actual aparece resaltado.

## Qué hace cada control

| Control | Comportamiento |
|---------|----------|
| **Forward Power** | Indicador. Lectura de potencia directa en tiempo real del amplificador. |
| **SWR** | Indicador. Lectura de ROE en tiempo real. |
| **Temperature / Drain Current / Mains Voltage** | Indicadores. Lecturas de telemetría de salud del amplificador. |
| **Operate / Standby** | Botón pulsador. Alterna el amplificador entre los modos Operate y Standby. El estado predeterminado al encender es Standby. |

## Consejos

- El indicador **Operate/Standby state** puede mostrar **Fault** si el amplificador reporta un error. El amplificador debe estar en un estado saludable antes de poder entrar en modo Operate.
- Los amplificadores ACOM rastrean automáticamente la banda de la radio, por lo que no se requiere selección manual de banda.

## Solución de problemas

- **Al hacer clic en Operate no ocurre nada** — El amplificador puede estar en estado Fault. Verifique las lecturas de temperatura, corriente de drenaje y voltaje de red en el applet ACOM. Resuelva la condición de falla en el propio amplificador antes de intentar volver a entrar en Operate.

## Relacionado

- [Supervisar la potencia directa y la ROE en la salida del amplificador](../amp/monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Observar la temperatura del amplificador, la corriente de drenaje y el voltaje de red](watch-amplifier-temperature-drain-current-and-mains-voltage.md)
