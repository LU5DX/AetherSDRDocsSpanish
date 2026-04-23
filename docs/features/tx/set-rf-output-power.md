# Configurar la potencia de salida de RF

Use el control deslizante RF Power en el applet TX Controls para establecer cuánta potencia emite el radio durante la transmisión. Ajústelo antes de operar para mantenerse dentro de los límites de su licencia y proteger los amplificadores conectados.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. Si no lo está, vaya a `Settings > Connect to Radio...`.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón TX tray en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el control deslizante **RF Power** en el applet TX Controls.
2. Arrastre el control hacia la izquierda para reducir la potencia o hacia la derecha para aumentarla. El valor numérico a la derecha del control se actualiza de inmediato.
3. Confirme que el valor mostrado junto al control es el nivel deseado. El radio aplica la nueva configuración en cuanto mueve el control.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango válido |
|---|---|---|---|
| RF Power (control deslizante) | Establece el nivel de potencia de RF de transmisión enviado al radio. | 100 | 0–100 |
| RF Pwr (medidor) | Muestra la potencia directa en la salida del excitador. Solo lectura. | — | 0–120 W (sin amplificador); 0–600 W (Aurora 500W). El medidor se pone rojo por encima de 100 W / 500 W. |
| SWR (medidor) | Muestra la relación de onda estacionaria en el excitador. Solo lectura. | — | 1.0–3.0. El medidor se pone rojo por encima de 2.5. |

## Consejos

- La escala del medidor RF Pwr cambia automáticamente según el modelo del radio. En un FLEX-8600 estándar, la zona roja comienza en 100 W; en un modelo Aurora 500W comienza en 500 W.
- Para configurar la potencia de una banda específica sin cambiar el control global, use `Settings > TX Band Settings...`. Ese cuadro de diálogo ofrece valores de potencia y potencia de ajuste por banda.
- Preste atención al medidor de SWR durante la transmisión. Una lectura de SWR superior a 2.5 (zona roja) indica un problema en la antena o la línea de alimentación.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Configurar la potencia del portador de ajuste](set-tune-carrier-power.md)
- [Iniciar un portador de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Realice su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
