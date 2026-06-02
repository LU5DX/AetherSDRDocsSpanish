# Ver telemetría del PGXL y controlar OPERATE/STANDBY

El applet del amplificador muestra telemetría en vivo de un Power Genius XL conectado: potencia directa, ROE, corriente de drenaje, temperatura del disipador, voltaje de red y eficiencia del amplificador. También proporciona un botón OPERATE/STANDBY para controlar el estado del amplificador.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El radio debe detectar un amplificador Power Genius XL. El botón de la bandeja AMP no aparece hasta que la radio informe de un PGXL.

## Pasos

1. Localice el botón de la bandeja AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet del amplificador.
3. Lea el indicador **PWR** para la potencia directa. La barra se vuelve roja por encima de 1500 W; el rango válido es 0-2000 W. La barra sube rápidamente en las ráfagas de RF y decae en unos 800 ms para mantener visibles las transmisiones breves.
4. Lea el indicador **SWR** para la ROE. La barra se vuelve roja por encima de 2.5; el rango válido es 1.0-3.0.
5. Lea el indicador **Id** para la corriente de drenaje. La barra se vuelve roja por encima de 60 A; el rango válido es 0-70 A.
6. Lea el texto **Temp** para la temperatura del disipador.
7. Lea el texto **Vdd** para el voltaje de drenaje.
8. Lea el texto **Vac** para el voltaje de red.
9. Lea el indicador **MEffA** para la métrica de eficiencia del amplificador (añadido en v26.5.1). Este indicador está oculto hasta que llegue la primera telemetría.
10. Haga clic en **OPERATE** para alternar el amplificador entre OPERATE y STANDBY. El botón muestra "OPERATE" (verde) cuando el amplificador está en estados IDLE, OPERATE o TRANSMIT_*, y "STANDBY" en caso contrario. El botón está oculto hasta que llegue el primer informe de estado.

## Qué hace cada control

| Control | Qué muestra | Umbral rojo | Notas |
|---|---|---|---|
| PWR | Potencia directa del PGXL | > 1500 W | Indicador con decaimiento balístico para transmisiones breves |
| SWR | ROE del PGXL | > 2.5 | — |
| Id | Corriente de drenaje del PGXL | > 60 A | Añadido en v26.6.1, reemplaza el indicador separado de Voltios/Amperios |
| Temp | Temperatura del disipador del PGXL | > 80 °C | Se muestra como etiqueta de texto |
| Vdd | Voltaje de drenaje del PGXL | — | Se muestra como etiqueta de texto |
| Vac | Voltaje de red del PGXL | — | Se muestra como etiqueta de texto |
| MEffA | Métrica de eficiencia del amplificador PGXL | — | Oculto hasta la primera telemetría. Añadido en v26.5.1 |
| OPERATE | Alternar el amplificador entre OPERATE y STANDBY | — | Oculto hasta el primer informe de estado. Verde para OPERATE, predeterminado para STANDBY |

## Consejos

- El indicador **PWR** utiliza decaimiento balístico para mantener visibles las transmisiones breves: la barra sube inmediatamente con RF y decae en aproximadamente 800 ms.
- El indicador **MEffA** permanece oculto hasta que el PGXL envía su primera telemetría de eficiencia. Si no aparece, es posible que el amplificador aún no esté enviando esta métrica.
- El botón **OPERATE** se mantiene sincronizado con el estado autoritativo de la radio. Si el estado del PGXL cambia a través de la ruta TCP directa, el botón se actualiza inmediatamente (v0.9.8+).
- El indicador **Temp** utiliza tres zonas de color: verde por debajo de 55 °C, amarillo de 55 °C a 80 °C y rojo por encima de 80 °C.

## Solución de problemas

- **El botón de la bandeja AMP no es visible** — La radio no ha detectado un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **El indicador MEffA no aparece** — El applet oculta este indicador hasta la primera actualización de telemetría. Espere a que el PGXL envíe una medición de eficiencia, o verifique la conexión del amplificador.
- **El botón OPERATE no aparece** — El botón está oculto hasta que el amplificador envíe su primer informe de estado. Espere a que el PGXL se conecte completamente.
- **Falta el indicador antiguo de Voltios/Amperios** — En v26.6.1, el indicador de texto de Voltios/Amperios fue reemplazado por los indicadores separados Vdd, Vac e Id. Use el nuevo indicador Id para la corriente de drenaje y las etiquetas Vdd/Vac para las lecturas de voltaje.

## Relacionado

- [Descripción general del amplificador](overview.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
