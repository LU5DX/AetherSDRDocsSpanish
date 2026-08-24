# Ponga el amplificador SPE Expert en Operate o Standby

Esta página le muestra cómo cambiar su amplificador lineal SPE Expert entre Operate y Standby desde el applet SPE Amplifier.

## Antes de comenzar

- El amplificador debe estar conectado mediante serie o ser2net TCP y encendido.
- Debe estar conectado a una radio FLEX-8600.

## Pasos

1. Abra el panel del applet y haga clic en el mosaico **SPE**.
2. Haga clic en **OPER** para cambiar el amplificador de Standby a Operate.
3. Haga clic en **OPER** nuevamente para volver a Standby.

La píldora de estado en la parte superior del applet muestra el modo actual: `OPR · RX` cuando está operando y recibiendo, `OPR · TX` cuando está operando y transmitiendo, o `STANDBY` cuando está en espera.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|
| **OPER** | STBY | Alterna entre Operate y Standby (refleja la tecla OPERATE del panel frontal). | Ninguna |
| Píldora **Status** | — | Muestra el modo actual como `OPR · RX`, `OPR · TX` o `STANDBY`. | Ninguna |

## Consejos

- Use Standby cuando desee operar sin el amplificador (barefoot) sin apagar el equipo.
- El botón **OPER** está deshabilitado mientras el amplificador está en silencio; encienda el amplificador con **ON** primero si es necesario.

## Relacionados

- [Descripción general del amplificador SPE Expert](overview.md)
- [Monitoree la potencia directa y la ROE en el amplificador SPE Expert](monitor-forward-power-and-swr-on-the-spe-expert-amplifier.md)
- [Cambie el nivel de potencia del SPE Expert (Low, Mid, High)](cycle-the-spe-expert-power-level-low-mid-high.md)
- [Sintonice el amplificador SPE Expert](tune-the-spe-expert-amplifier.md)
