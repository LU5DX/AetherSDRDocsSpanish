# Monitorear temperatura, corriente de drenaje y tensión de red del PGXL

El applet Amplifier muestra en tiempo real la temperatura del disipador, la corriente de drenaje y la tensión de red de un Power Genius XL conectado. Use estas lecturas para supervisar el estado del amplificador durante una sesión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El radio debe haber detectado un amplificador Power Genius XL. El botón de bandeja AMP no aparece hasta que el radio reporta un PGXL.

## Pasos

1. Localice el botón de bandeja AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet Amplifier.
3. Lea el indicador **Temp** para conocer la temperatura del disipador. La barra se vuelve roja por encima de 80 °C; el rango válido es 0–100 °C.
4. Lea el indicador de texto **Volts / Amps** para conocer la tensión de red y la corriente de drenaje. El formato es `Volts: xxxV  Amps: x.xA`. Este indicador permanece oculto hasta que llega la primera telemetría del PGXL.

## Qué muestra cada control

| Control | Qué muestra | Umbral rojo | Rango válido |
|---|---|---|---|
| Temp | Temperatura del disipador del PGXL | > 80 °C | 0–100 °C |
| Volts / Amps | Tensión de red (voltios enteros) y corriente de drenaje (un decimal, amperios) | — | Voltios enteros; x.x A |

## Consejos

- El indicador **Volts / Amps** permanece oculto hasta que el PGXL envía su primera actualización de telemetría. Si no aparece, es posible que el amplificador aún no esté transmitiendo telemetría — verifique que el PGXL esté encendido y comunicándose con el radio.
- El indicador **Temp** usa tres zonas de color: verde por debajo de 55 °C, amarillo de 55 °C a 80 °C, y rojo por encima de 80 °C.

## Solución de problemas

- **El botón de bandeja AMP no es visible** — El radio no ha detectado un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **La línea Volts / Amps no aparece** — El applet oculta este indicador hasta que llega la primera telemetría. Espere a que el PGXL envíe una actualización de telemetría, o verifique la conexión del amplificador.

## Relacionados

- [Descripción general del amplificador](overview.md)
- [Monitorear potencia directa y ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
