# Monitorear la temperatura del PGXL, la corriente de drenaje y el voltaje de la red eléctrica

El applet Amplificador muestra en vivo la temperatura del disipador de calor, la corriente de drenaje y el voltaje de la red eléctrica de un Power Genius XL conectado. Utilice estas lecturas para monitorear la salud del amplificador durante una sesión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El amplificador Power Genius XL debe ser detectado por la radio. El botón AMP en la bandeja no aparece hasta que la radio reporta un PGXL.

## Pasos

1.  Localice el botón AMP en la bandeja, en la barra lateral derecha del panel de applets.
2.  Haga clic en AMP para abrir el applet Amplificador.
3.  Lea el indicador **Temp** para conocer la temperatura del disipador de calor. La barra se vuelve roja por encima de 80 °C; el rango válido es de 0 a 100 °C.
4.  Lea el indicador de texto **Volts / Amps** para conocer el voltaje de la red eléctrica y la corriente de drenaje. El formato es `Volts: xxxV  Amps: x.xA`. Este indicador está oculto hasta que llega la primera telemetría del PGXL.

## Función de cada control

| Control      | Qué muestra                                                                    | Umbral rojo |
|--------------|--------------------------------------------------------------------------------|-------------|
| Temp         | Temperatura del disipador de calor del PGXL                                    | > 80 °C     |
| Volts / Amps | Voltaje de la red eléctrica (voltios enteros) y corriente de drenaje (amperios con un decimal) | —           |

## Consejos

- El indicador **Volts / Amps** permanece oculto hasta que el PGXL envía su primera actualización de telemetría. Si no aparece, es posible que el amplificador aún no esté transmitiendo telemetría; verifique que el PGXL esté encendido y comunicándose con la radio.
- El indicador **Temp** utiliza tres zonas de color: verde por debajo de 55 °C, amarillo de 55 °C a 80 °C y rojo por encima de 80 °C.

## Solución de problemas

- **El botón AMP de la bandeja no es visible** — La radio no ha detectado un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **La línea de Volts / Amps no aparece** — El applet oculta este indicador hasta que llega la primera telemetría. Espere a que el PGXL envíe una actualización de telemetría o verifique la conexión del amplificador.

## Relacionados

- [Resumen del amplificador](overview.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
