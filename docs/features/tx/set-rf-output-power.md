# Configurar la potencia de salida de RF

Use el control deslizante RF Power en el applet TX Controls para establecer cuánta potencia transmite el FLEX-8600. Ajustarlo antes de transmitir evita la sobreexcitación y protege su amplificador o sistema de antena.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón TX tray en la barra lateral derecha.

## Pasos

1. Localice el control deslizante **RF Power** en el applet TX Controls. Es el primer control deslizante debajo de los medidores **RF Pwr** y **SWR**.
2. Arrastre el control hacia la izquierda para reducir la potencia o hacia la derecha para aumentarla. El valor numérico a la derecha del control se actualiza de inmediato.
3. Confirme que el valor mostrado junto al control coincide con el nivel de potencia deseado (0–100).

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido |
|---|---|---|---|
| Medidor **RF Pwr** | Muestra la potencia directa en la salida del excitador. | — | 0–120 W; rojo por encima de 100 W (sin amplificador). La escala cambia a 0–600 W en los modelos Aurora 500W, rojo por encima de 500 W. |
| Medidor **SWR** | Muestra la relación de onda estacionaria en el excitador. | — | 1.0–3.0; rojo por encima de 2.5. |
| Control deslizante **RF Power** | Establece el nivel de potencia de RF de transmisión enviado a la radio. | 100 | 0–100 |

## Consejos

- El medidor **RF Pwr** muestra la potencia directa real únicamente durante la transmisión. Ajuste el control antes de transmitir y luego verifique la lectura del medidor durante una transmisión.
- Si utiliza un amplificador lineal, ajuste **RF Power** al nivel de excitación que requiere su amplificador en lugar del máximo.
- Para establecer la potencia del portador de ajuste de forma independiente del nivel de potencia de operación, use el control deslizante **Tune Pwr**. Consulte [Configurar la potencia del portador de ajuste](set-tune-carrier-power.md).

## Solución de problemas

- **El control se mueve pero la potencia directa no cambia** — Es posible que la radio no esté transmitiendo. El medidor **RF Pwr** solo registra mientras la radio está activa. Active la radio con MOX o transmitiendo normalmente y vuelva a verificar.
- **El medidor RF Pwr entra en zona roja** — Reduzca el control deslizante **RF Power**. En la operación sin amplificador del FLEX-8600, la zona roja comienza por encima de 100 W; superarla arriesga una sobreexcitación.

## Relacionados

- [Descripción general de TX Controls](overview.md)
- [Configurar la potencia del portador de ajuste](set-tune-carrier-power.md)
- [Iniciar un portador de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Activar o desactivar MOX para teclear el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (p. ej. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
