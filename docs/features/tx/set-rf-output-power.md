# Configurar la potencia de salida de RF

Use el control deslizante **RF Power** del applet TX Controls para establecer el nivel de potencia de transmisión enviado a su antena. Ajustarlo antes de transmitir evita saturar su amplificador o superar los límites de potencia de la banda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no lo está, vaya a `Settings > Connect to Radio...`.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón **TX** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el control deslizante **RF Power** en el applet TX Controls. Aparece debajo del medidor **SWR**.
2. Arrastre el control deslizante hacia la izquierda o la derecha para establecer el nivel de potencia deseado. La lectura numérica a la derecha del control se actualiza de inmediato.
3. Confirme que el valor mostrado en la lectura es el que desea. El medidor **RF Pwr** reflejará la potencia directa real una vez que transmita.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido |
|---|---|---|---|
| Control deslizante **RF Power** | Establece el nivel de potencia de RF de transmisión enviado a la radio. | 100 | 0–100 |
| Medidor **RF Pwr** | Muestra la potencia directa real en la salida del excitador. | — | 0–120 W (sin amplificador externo); 0–600 W (Aurora 500 W); rojo por encima de 100 W / 500 W |
| Medidor **SWR** | Muestra la relación de onda estacionaria en el excitador. | — | 1.0–3.0; rojo por encima de 2.5 |

## Consejos

- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de su radio. En un FLEX-8600 estándar, la zona roja comienza por encima de 100 W.
- Puede establecer límites de potencia por banda de forma independiente a este control deslizante. Vaya a `Settings > TX Band Settings...` para configurar la potencia, la potencia de ajuste y los ajustes de inhibición para cada banda.
- El control deslizante **RF Power** controla el nivel de salida del excitador, no el de un amplificador externo. Si está usando un amplificador externo, ajuste este control al nivel de excitación que su amplificador requiera.

## Solución de problemas

- **El medidor RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio esté realmente activada. Verifique que MOX esté activo (el botón **MOX** está en rojo) o que su línea PTT esté activada. Verifique también que el control deslizante **RF Power** no esté en 0.
- **El control deslizante se mueve pero la potencia directa no cambia** — Es posible que la conexión con la radio se haya interrumpido. Compruebe el estado de la conexión y vuelva a conectarse mediante `Settings > Connect to Radio...` si es necesario.

## Relacionados

- [Descripción general de TX Controls](overview.md)
- [Configurar la potencia del portador de ajuste](set-tune-carrier-power.md)
- [Iniciar un portador de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Activar o desactivar MOX para accionar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
