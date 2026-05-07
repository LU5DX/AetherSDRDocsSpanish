# Monitorear la Potencia Directa y la ROE a la Salida del Amplificador

El applet del Amplificador muestra lecturas en vivo de potencia directa y ROE desde un amplificador Power Genius XL (PGXL) conectado. Utilice estos medidores para confirmar la potencia de salida y la adaptación de la antena durante la transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El amplificador Power Genius XL debe ser detectado por la radio. El botón de la bandeja AMP no aparece hasta que el PGXL está presente.

## Pasos

1. Localice el botón de la bandeja AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet del Amplificador.
3. Transmita. Observe cómo los medidores Fwd Pwr y SWR se actualizan en tiempo real.

## Qué hace cada control

| Control   | Qué muestra                                     | Rango    |
|-----------|-------------------------------------------------|----------|
| Fwd Pwr   | Potencia directa a la salida del PGXL           | 0–2000 W |
| SWR       | Relación de onda estacionaria a la salida del PGXL | 1.0–3.0  |

Ambos medidores se muestran como indicadores de barra horizontales. La barra rellena se vuelve roja cuando el valor entra en la zona roja. Las etiquetas de división se dibujan en la parte superior de cada indicador en los siguientes puntos de referencia:

- **Fwd Pwr:** 0, 500, 1000, 1.5k, 2k
- **SWR:** 1, 1.5, 2, 2.5, 3

Ninguno de los medidores tiene una clave de configuración persistente. Los valores son telemetría de solo lectura proveniente del PGXL.

## Consejos

- Los indicadores de barra utilizan una animación suavizada. Un breve retraso entre el valor real y la barra mostrada es normal durante condiciones que cambian rápidamente, como el inicio de una transmisión.
- Si la ROE entra en la zona roja (por encima de 2.5), revise su sistema de antena antes de continuar transmitiendo a alta potencia.

## Solución de problemas

- **El botón de la bandeja AMP no es visible** — El PGXL no ha sido detectado por la radio. Verifique que el amplificador esté encendido y conectado a la radio Flex. AetherSDR muestra el botón AMP solo después de que la radio informe que hay un amplificador presente.
- **Los medidores Fwd Pwr y SWR no muestran movimiento durante la transmisión** — Confirme que el amplificador esté en estado OPERATE, no en STANDBY. Consulte [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md).

## Relacionados

- [Descripción general del amplificador](overview.md)
- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Observar la temperatura, la corriente de drenaje y la tensión de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
