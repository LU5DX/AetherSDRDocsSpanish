# Poner el amplificador en Operar o Espera

Cambie el amplificador lineal ACOM entre el estado de Operar (transmisión activa) y Espera (derivado o inactivo) desde AetherSDR.

## Antes de comenzar

- La radio debe estar conectada a AetherSDR.
- Un amplificador ACOM debe estar conectado y comunicándose (serial o TCP) con AetherSDR.

## Pasos

1. Abra el **Applet panel**.
2. Haga clic en el mosaico **ACOM** para abrir el applet del amplificador ACOM.
3. Haga clic en el botón **Operate / Standby** para alternar entre los dos modos.

   - La etiqueta del botón muestra el modo actual. Cuando el amplificador está en Operar, el botón muestra **Operate**; al hacer clic, cambia a Espera, y viceversa.
   - El indicador **Operate/Standby state** debajo del botón confirma el modo actual: Operar, Espera o Falla.

## Qué hace cada control

| Control | Comportamiento |
|---------|----------------|
| **Operate / Standby** | Botón pulsador. Alterna el amplificador entre los modos Operar y Espera. El estado predeterminado al encender es Espera. |

## Consejos

- El indicador **Operate/Standby state** puede mostrar **Fault** si el amplificador reporta un error. El amplificador debe estar en un estado saludable antes de poder entrar en modo Operar.

## Solución de problemas

- **Hacer clic en Operate / Standby no hace nada** — El amplificador puede estar en estado de Falla. Verifique las lecturas de temperatura, corriente de drenaje y voltaje de red en el applet ACOM. Resuelva la condición de falla en el amplificador mismo antes de intentar volver a entrar en Operar.

## Relacionados

- [Descripción general del amplificador ACOM](overview.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](../amp/monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Observar la temperatura del amplificador, la corriente de drenaje y el voltaje de red](watch-amplifier-temperature-drain-current-and-mains-voltage.md)
