# Ajustar la ganancia TCI RX por canal

El applet TCI Server proporciona cuatro controles deslizantes de ganancia RX independientes — uno por canal — para controlar el nivel de audio con que cada canal receptor se presenta a los clientes TCI conectados, como Log4OM o las herramientas SunSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet TCI requiere una conexión de radio.
- El servidor TCI debe ser visible en el panel de applets. Si no lo está, haga clic en el botón de bandeja **TCI** de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **TCI** de la barra lateral derecha para abrir el applet TCI Server.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** correspondiente al canal que desea ajustar.
3. Arrastre el medidor/control deslizante de esa fila hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El nuevo valor se guarda de inmediato.
4. Repita el procedimiento para cualquier otro canal RX que desee ajustar.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| RX1 gain+meter | Medidor de nivel y control de ganancia combinados para el canal TCI RX 1. | 0.5 | 0.0–1.0 | `TciRxGain1` |
| RX2 gain+meter | Medidor de nivel y control de ganancia combinados para el canal TCI RX 2. | 0.5 | 0.0–1.0 | `TciRxGain2` |
| RX3 gain+meter | Medidor de nivel y control de ganancia combinados para el canal TCI RX 3. | 0.5 | 0.0–1.0 | `TciRxGain3` |
| RX4 gain+meter | Medidor de nivel y control de ganancia combinados para el canal TCI RX 4. | 0.5 | 0.0–1.0 | `TciRxGain4` |
| Etiqueta de asignación de slice | Indicador que muestra qué slice alimenta esta fila RX (p. ej., `Slice A`). Muestra `—` cuando no hay ningún slice asignado. | `—` | `—` o `Slice <letter>` | — |

Cada canal RX comparte su asignación de slice con el mapeo de canales DAX. La etiqueta junto a cada medidor indica qué slice está enrutado actualmente a ese canal.

## Consejos

- La parte del medidor en cada control deslizante refleja el nivel de señal en tiempo real con suavizado de ataque rápido y decaimiento lento, de modo que los picos breves son visibles sin que la pantalla parpadee constantemente.
- Cada valor de ganancia se guarda en el momento en que suelta el control deslizante. Al reiniciar AetherSDR se restaura el último valor guardado.
- Si un canal muestra `—` en la etiqueta de slice, no hay ningún slice asignado actualmente a ese canal DAX. Asigne un slice al canal DAX correspondiente para enrutar el audio a través de él.

## Temas relacionados

- [Descripción general de TCI Server](overview.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
