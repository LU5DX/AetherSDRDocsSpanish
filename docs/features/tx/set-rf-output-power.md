# Establecer la potencia de salida RF

Use el regulador RF Power en el applet TX Controls para establecer el nivel de potencia de transmisión que se envía a su antena. Ajustar esto antes de transmitir evita sobrecarga del amplificador o el incumplimiento de los límites de potencia de la banda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet TX Controls debe ser visible. Si no lo es, haga clic en el botón **TX** en la bandeja de la derecha para mostrarlo.

## Pasos

1. Localice el regulador **RF Power** en el applet TX Controls. Aparece debajo del indicador **SWR**.
2. Arrastre el regulador hacia la izquierda o derecha para establecer su nivel de potencia deseado. La lectura numérica a la derecha del regulador se actualiza inmediatamente.
3. Confirme que el valor mostrado en la lectura sea el que desea. El indicador **RF Pwr** reflejará la potencia directa real una vez que transmita.

## Qué hace cada control

| Control             | Descripción                                          | Por defecto |
|---------------------|------------------------------------------------------|---------|
| Regulador **RF Power** | Establece el nivel de potencia RF de transmisión que se envía a la radio.  | 100     |
| Indicador **RF Pwr**    | Muestra la potencia directa real a la salida del excitador. | —       |
| Indicador **SWR**       | Muestra la relación de ondas estacionarias en el excitador.         | —       |

## Consejos

- La escala del indicador **RF Pwr** cambia automáticamente según su modelo de radio. En una FLEX-8600 estándar, la zona roja comienza por encima de 100 W.
- Puede establecer límites de potencia por banda independientemente de este regulador. Vaya a `Settings > TX Band Settings...` para configurar la potencia, potencia de sintonización e inhibición para cada banda.
- El regulador **RF Power** controla el nivel de salida del excitador, no un amplificador separado. Si está usando un amplificador externo, establezca este regulador al nivel de excitación que su amplificador espera.

## Solución de problemas

- **El indicador RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio esté realmente activada. Compruebe que MOX esté activo (el botón **MOX** es rojo) o que su línea PTT esté asertada. También verifique que el regulador **RF Power** no esté ajustado a 0.
- **El regulador se mueve pero la potencia directa no cambia** — La conexión de radio puede haberse perdido. Compruebe el estado de la conexión y reconecte a través de `Settings > Connect to Radio...` si es necesario.

## Temas relacionados

- [Descripción general de TX Controls](overview.md)
- [Establecer la potencia de portadora de sintonización](set-tune-carrier-power.md)
- [Iniciar una portadora de sintonización para verificar SWR](start-a-tune-carrier-to-check-swr.md)
- [Activar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles TX (por ejemplo, SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
