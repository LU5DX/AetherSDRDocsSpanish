# Supervisar la temperatura, corriente de drenaje y tensión de red del PGXL

El applet Amplifier muestra en tiempo real la temperatura del disipador, la corriente de drenaje y la tensión de red de un Power Genius XL conectado. Use estas lecturas para monitorear la salud del amplificador durante una sesión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El radio debe haber detectado un amplificador Power Genius XL. El botón AMP en la bandeja no aparece hasta que el radio reporte un PGXL.

## Pasos

1. Localice el botón AMP en la bandeja del panel de applets, en la barra lateral derecha.
2. Haga clic en AMP para abrir el applet Amplifier.
3. Lea el medidor **Temp** para ver la temperatura del disipador. La barra se vuelve roja por encima de 80 °C; el rango válido es 0–100 °C.
4. Lea el indicador de texto **Volts / Amps** para ver la tensión de red y la corriente de drenaje. El formato es `Volts: xxxV  Amps: x.xA`. Este indicador permanece oculto hasta que llega la primera telemetría del PGXL.

## Qué muestra cada control

| Control | Qué muestra | Umbral rojo | Rango válido |
|---|---|---|---|
| Temp | Temperatura del disipador del PGXL | > 80 °C | 0–100 °C |
| Volts / Amps | Tensión de red (voltios enteros) y corriente de drenaje (un decimal, amperios) | — | Voltios enteros; x.x A |

## Consejos

- El indicador **Volts / Amps** permanece oculto hasta que el PGXL envía su primera actualización de telemetría. Si no aparece, es posible que el amplificador aún no esté transmitiendo telemetría — verifique que el PGXL esté encendido y comunicándose con el radio.
- El medidor **Temp** usa tres zonas de color: verde por debajo de 55 °C, amarillo entre 55 °C y 80 °C, y rojo por encima de 80 °C.

## Solución de problemas

- **El botón AMP no es visible** — El radio no ha detectado un Power Genius XL. Confirme que el PGXL esté encendido y conectado al radio Flex.
- **La línea Volts / Amps no aparece** — El applet oculta este indicador hasta que llega la primera telemetría. Espere a que el PGXL envíe una actualización de telemetría, o verifique la conexión del amplificador.

## Relacionados

- [Descripción general del amplificador](overview.md)
- [Supervisar la potencia directa y el SWR en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
