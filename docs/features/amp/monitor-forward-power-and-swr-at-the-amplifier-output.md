# Monitorizar la potencia directa y la ROE en la salida del amplificador

El applet del amplificador muestra lecturas en vivo de la potencia directa y la ROE de un amplificador Power Genius XL (PGXL) conectado. Utilice estos medidores para confirmar la potencia de salida y la adaptación de la antena durante la transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- Un amplificador Power Genius XL debe ser detectado por la radio. El botón de la bandeja AMP no aparece hasta que el PGXL esté presente.

## Pasos

1. Localice el botón de la bandeja AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet del amplificador.
3. Transmita. Observe cómo los medidores Fwd Pwr y SWR se actualizan en tiempo real.

## Qué hace cada control

| Control | Qué muestra                              | Rango    |
|---------|------------------------------------------|----------|
| PWR     | Potencia directa en la salida del PGXL   | 0–2000 W |
| SWR     | Relación de onda estacionaria en la salida del PGXL | 1.0–3.0  |
| Id      | Corriente de drenaje                     | 0–70 A   |

Los tres medidores se muestran como barras de medición horizontales con una etiqueta a la izquierda que indica el nombre del campo y el valor en vivo (por ejemplo, "PWR 1148"). La barra se vuelve roja cuando el valor entra en la zona roja. Las marcas de graduación se dibujan a lo largo de la parte superior de cada medidor en los siguientes puntos de referencia:

- **PWR:** 0, 500, 1000, 1.5K, 2K
- **SWR:** 1, 1.5, 2, 2.5, 3
- **Id:** 0, 10, 20, 30, 40, 50, 60, 70

El medidor PWR tiene balística de liberación lenta: la barra sube rápidamente en las ráfagas de RF pero disminuye en aproximadamente 800 ms, por lo que las transmisiones breves permanecen visibles. Esto coincide con la sensación de retención de pico del medidor S.

Ningún medidor tiene una clave de configuración persistente. Los valores son telemetría de solo lectura del PGXL.

## Consejos

- Las barras de medición utilizan animación suavizada. Un breve retraso entre el valor real y la barra mostrada es normal durante condiciones de cambio rápido, como el inicio de una transmisión.
- Si la ROE entra en la zona roja (por encima de 2.5), verifique su sistema de antena antes de continuar transmitiendo a alta potencia.
- El medidor de corriente de drenaje (Id) ayuda a monitorear la salud del amplificador. Si Id supera los 60 A, considere reducir la potencia de excitación.

## Solución de problemas

- **El botón de la bandeja AMP no es visible** — El PGXL no ha sido detectado por la radio. Verifique que el amplificador esté encendido y conectado a la radio Flex. AetherSDR muestra el botón AMP solo después de que la radio informe que hay un amplificador presente.
- **Los medidores PWR y SWR no muestran movimiento durante la transmisión** — Confirme que el amplificador esté en estado OPERATE, no en STANDBY. Consulte [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md).

## Relacionado

- [Visión general del amplificador](overview.md)
- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Ver la temperatura del PGXL, el voltaje de drenaje y el voltaje de red](watch-pgxl-temperature-drain-voltage-and-mains-voltage.md)
