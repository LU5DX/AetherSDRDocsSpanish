# Monitoree la potencia directa y la ROE en el amplificador SPE Expert

Monitoree en tiempo real la potencia directa, la ROE de antena y la ROE de entrada del ATU desde su amplificador SPE Expert (1.3K-FA, 1.5K-FA, 2K-FA) mediante el applet SPE en el panel de applets.

## Antes de comenzar

- Su radio FLEX-8600 debe estar conectado a AetherSDR.
- El amplificador SPE Expert debe estar conectado mediante serial o ser2net TCP y encendido.
- El amplificador debe haber sido consultado al menos una vez para que el applet pueda detectar el modelo y ajustar la escala del medidor.

## Pasos

1. Abra el panel de applets haciendo clic en el icono Applet Panel en la barra de herramientas principal.
2. Haga clic en el mosaico **SPE** para abrir el applet del amplificador SPE Expert.
3. Lea el medidor de **Potencia Directa** (etiquetado **PWR**) para ver la potencia de salida en vatios. La escala del medidor se configura automáticamente según el modelo detectado en la primera consulta.
4. Lea el medidor de **ROE de Antena** (etiquetado **SWR**) para ver la ROE del lado de la antena en tiempo real.
5. Lea el medidor de **ROE del ATU** (etiquetado **ATU**) para ver la ROE en tiempo real en la entrada del ATU.
6. Verifique las lecturas de **TEMP**, **V** e **I** para conocer la temperatura del disipador, el voltaje de alimentación y la corriente de alimentación.
7. Si se produce una falla, aparece un banner en la parte superior del applet en texto rojo que describe el problema.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---------|------|----------|
| **Potencia Directa** (PWR) | Medidor | Potencia directa en tiempo real en vatios. Escala configurada según el modelo detectado; 5 marcas espaciadas uniformemente. |
| **ROE de Antena** (SWR) | Medidor | ROE del lado de la antena en tiempo real, escala de 1:1 a 3:1 con marcas en 1, 1.5, 2, 2.5, 3. |
| **ROE del ATU** (ATU) | Medidor | ROE en tiempo real en la entrada del ATU, misma escala que la ROE de antena. |
| **TEMP** | Texto | Temperatura del disipador, mostrada tal cual en la unidad propia del amplificador (C o F). |
| **V** | Texto | Voltaje de alimentación en voltios. |
| **I** | Texto | Corriente de alimentación en amperios. |
| **Pastilla de estado** | Indicador | Muestra **OPR · TX**, **OPR · RX** o **STANDBY** — el modo de operación del amplificador. |
| **Banner de falla** | Indicador | Aparece en texto rojo cuando el amplificador reporta una condición de falla. |

## Consejos

- La lectura de **TEMP** utiliza la unidad (Celsius o Fahrenheit) para la que esté configurada la propia pantalla del amplificador. AetherSDR no la convierte.
- El medidor de potencia tiene suavizado balístico; el valor pico se mantiene durante 2.5 segundos después de cada transmisión.

## Relacionado

- [Descripción general del amplificador SPE Expert](overview.md)
- [Ponga el amplificador SPE Expert en Operate o Standby](put-the-spe-expert-amplifier-in-operate-or-standby.md)
- [Sintonice el amplificador SPE Expert](tune-the-spe-expert-amplifier.md)
