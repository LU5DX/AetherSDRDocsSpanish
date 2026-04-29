# Monitorear la Potencia Directa y el ROS en la Salida del Amplificador

El applet Amplifier muestra lecturas en vivo de potencia directa y ROS desde un amplificador Power Genius XL (PGXL) conectado. Use estos medidores para confirmar la potencia de salida y la adaptación de antena durante la transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El radio debe haber detectado un amplificador Power Genius XL. El botón AMP del panel de bandeja no aparece hasta que el PGXL esté presente.

## Pasos

1. Localice el botón AMP del panel de bandeja en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet Amplifier.
3. Transmita. Observe cómo los medidores Fwd Pwr y SWR se actualizan en tiempo real.

## Qué hace cada control

| Control | Qué muestra | Rango | Zona roja |
|---------|-------------|-------|-----------|
| Fwd Pwr | Potencia directa en la salida del PGXL | 0–2000 W | Por encima de 1500 W |
| SWR | Relación de onda estacionaria en la salida del PGXL | 1.0–3.0 | Por encima de 2.5 |

Ambos medidores se muestran como barras horizontales. La barra rellena se vuelve roja cuando el valor entra en la zona roja. Las etiquetas de escala se dibujan a lo largo de la parte superior de cada barra en los siguientes puntos de referencia:

- **Fwd Pwr:** 0, 500, 1000, 1.5k, 2k
- **SWR:** 1, 1.5, 2, 2.5, 3

Ninguno de los medidores tiene una clave de configuración persistente. Los valores son telemetría de solo lectura proveniente del PGXL.

## Consejos

- Las barras de medición usan animación suavizada. Un breve retraso entre el valor real y la barra mostrada es normal durante condiciones de cambio rápido, como el inicio de una transmisión.
- Si el SWR entra en la zona roja (por encima de 2.5), revise su sistema de antena antes de continuar transmitiendo a alta potencia.

## Solución de problemas

- **El botón AMP del panel de bandeja no es visible** — El radio no ha detectado el PGXL. Verifique que el amplificador esté encendido y conectado a la radio Flex. AetherSDR muestra el botón AMP solo después de que la radio reporta que hay un amplificador presente.
- **Los medidores Fwd Pwr y SWR no muestran movimiento durante la transmisión** — Confirme que el amplificador esté en estado OPERATE y no en STANDBY. Consulte [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md).

## Temas relacionados

- [Descripción general del amplificador](overview.md)
- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Ver la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
