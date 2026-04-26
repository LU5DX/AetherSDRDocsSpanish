# Ajustar la potencia de salida de RF

Use el applet TX Controls para ajustar la potencia que el radio transmite durante la emisión. Establecer un nivel adecuado protege los transistores finales, cumple con las condiciones de su licencia y mantiene su señal limpia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls requiere una conexión de radio activa.
- Abra el applet TX Controls si no está visible: haga clic en el botón **TX** del panel lateral derecho.

## Pasos

1. Localice el control deslizante **RF Power** en el applet TX Controls.
2. Arrastre el control hacia la izquierda para reducir la potencia o hacia la derecha para aumentarla. El valor numérico a la derecha del control se actualiza de inmediato.
3. Lea la salida actual en el medidor **RF Pwr** sobre los controles deslizantes para confirmar que el radio entrega la potencia esperada durante la transmisión.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| **RF Power** | Control deslizante | 100 | 0–100 | Establece el nivel de potencia de RF de transmisión enviado al radio. La etiqueta numérica a la derecha muestra el valor actual. |
| **RF Pwr** | Medidor | — | 0–120 W (sin amplificador); 0–600 W (Aurora 500 W) | Muestra la potencia directa real en la salida del excitador. La escala cambia automáticamente según el modelo de radio conectado. Indica en rojo por encima de 100 W (sin amplificador) o 500 W (Aurora). |
| **SWR** | Medidor | — | 1.0–3.0 | Muestra la relación de onda estacionaria en el excitador. Indica en rojo por encima de 2.5. |

## Consejos

- El medidor **RF Pwr** solo se mueve mientras el radio está transmitiendo (MOX activado, TUNE activo o PTT presionado). Ajuste el control deslizante antes de transmitir y luego verifique la lectura en el aire.
- Los límites de potencia por banda pueden configurarse por separado. Consulte `Settings > TX Band Settings...` para establecer la potencia máxima de TX, la potencia de ajuste y las opciones de inhibición para cada banda.
- El control deslizante **Tune Pwr** controla la potencia utilizada únicamente durante un ciclo de ajuste y no afecta la potencia de transmisión normal. Consulte [Ajustar la potencia del portador de ajuste](set-tune-carrier-power.md).

## Resolución de problemas

- **El medidor RF Pwr permanece en cero durante la transmisión** — Verifique que la antena esté conectada y que la ROS esté dentro del rango. Una ROS extremadamente alta puede hacer que el radio reduzca la potencia a casi cero.
- **El control deslizante RF Power se mueve pero la salida no cambia** — Confirme que el radio esté conectado (el applet TX Controls requiere una conexión activa). Si el control regresa a su posición anterior, el radio puede estar rechazando el comando; verifique la configuración de banda del radio o el estado de inhibición de TX.
- **La escala de RF Pwr muestra 0–600 W inesperadamente** — Esto es normal si se detecta un módulo Aurora 500 W. El umbral rojo se desplaza a 500 W en esa escala.

## Relacionados

- [Descripción general de TX Controls](overview.md)
- [Ajustar la potencia del portador de ajuste](set-tune-carrier-power.md)
- [Iniciar un portador de ajuste para verificar la ROS](start-a-tune-carrier-to-check-swr.md)
- [Usar el ATU interno](run-the-internal-atu.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
