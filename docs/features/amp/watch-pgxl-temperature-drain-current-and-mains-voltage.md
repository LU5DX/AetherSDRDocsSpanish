# Ver telemetría del PGXL y controlar OPERATE/STANDBY

El applet del amplificador muestra telemetría en vivo de un Power Genius XL conectado: potencia directa, ROE, corriente de drenaje, temperatura del disipador, tensión de red y eficiencia del amplificador. También proporciona un botón OPERATE/STANDBY para controlar el estado del amplificador y un botón Fan Speed para recorrer los modos de ventilador.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El amplificador Power Genius XL debe ser detectado por la radio. El botón de bandeja AMP no aparece hasta que la radio reporte un PGXL.

## Pasos

1. Localice el botón de bandeja AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet del amplificador.
3. Lea el indicador **PWR** para la potencia directa. La barra se vuelve roja por encima de 1500 W; el rango válido es 0–2000 W. La barra sube rápidamente en ráfagas de RF y decae en ~800 ms para mantener visibles las transmisiones breves.
4. Lea el indicador **SWR** para la ROE. La barra se vuelve roja por encima de 2.5; el rango válido es 1.0–3.0. El indicador se limpia a 1.0 cuando la potencia directa cae por debajo de 5 W y restaura el valor en caché cuando la potencia se reanuda.
5. Lea el indicador **Id** para la corriente de drenaje. La barra se vuelve roja por encima de 60 A; el rango válido es 0–70 A.
6. Lea el texto **Temp** para la temperatura del disipador.
7. Lea el texto **Vdd** para la tensión de drenaje. Muestra una raya cuando la alimentación de drenaje está apagada (tensión por debajo de 1.0 V).
8. Lea el texto **Vac** para la tensión de red.
9. Lea el indicador **MEffA** para la métrica de eficiencia del amplificador (añadido en v26.5.1). Este indicador está oculto hasta que llegue la primera telemetría.
10. Haga clic en el botón **Fan Speed** para recorrer los modos STANDARD, CONTEST y BROADCAST. El botón muestra una sola letra (S, C o B). El botón está oculto hasta que llegue el primer estado del modo de ventilador desde una conexión directa al PGXL. Añadido en v26.6.3.
11. Haga clic en **OPERATE** para alternar el amplificador entre OPERATE y STANDBY. El botón muestra "OPERATE" (verde) cuando el amplificador está en los estados IDLE, OPERATE o TRANSMIT_*, y "STANDBY" en caso contrario. El botón está oculto hasta que llegue el primer reporte de estado.

## Qué hace cada control

| Control | Qué muestra | Umbral rojo | Notas |
|---|---|---|---|
| PWR | Potencia directa del PGXL | > 1500 W | Indicador con decaimiento balístico para transmisiones breves; nombre accesible "Forward power" |
| SWR | ROE del PGXL | > 2.5 | Se limpia a 1.0 cuando la potencia directa cae por debajo de 5 W; nombre accesible "SWR" |
| Id | Corriente de drenaje del PGXL | > 60 A | Nombre accesible "Drain current" |
| Temp | Temperatura del disipador del PGXL | > 80 °C | Se muestra como etiqueta de texto |
| Vdd | Tensión de drenaje del PGXL | — | Muestra raya cuando está por debajo de 1.0 V |
| Vac | Tensión de red del PGXL | — | Se muestra como etiqueta de texto |
| MEffA | Métrica de eficiencia del amplificador PGXL | — | Oculto hasta la primera telemetría. Añadido en v26.5.1 |
| Fan Speed | Recorrer STANDARD / CONTEST / BROADCAST | — | Oculto hasta que la conexión directa al PGXL entregue el modo de ventilador. Muestra la primera letra del modo actual (S/C/B). Añadido en v26.6.3 |
| OPERATE | Alternar amplificador entre OPERATE y STANDBY | — | Oculto hasta el primer reporte de estado. Verde para OPERATE, predeterminado para STANDBY |

## Consejos

- El indicador **PWR** utiliza decaimiento balístico para mantener visibles las transmisiones breves: la barra sube inmediatamente con RF y decae en aproximadamente 800 ms.
- El indicador **SWR** se limpia automáticamente a 1.0 cuando la potencia directa cae por debajo de 5 W porque la ROE no tiene sentido en reposo. El valor en caché se restaura cuando la potencia se reanuda.
- El indicador **MEffA** permanece oculto hasta que el PGXL envíe su primera telemetría de eficiencia. Si no aparece, es posible que el amplificador aún no esté enviando esta métrica.
- El botón **OPERATE** se mantiene sincronizado con el estado autoritativo de la radio. Si el estado del PGXL cambia a través de la ruta TCP directa, el botón se actualiza inmediatamente (v0.9.8+).
- El indicador **Temp** usa tres zonas de color: verde por debajo de 55 °C, amarillo de 55 °C a 80 °C y rojo por encima de 80 °C.
- El botón **Fan Speed** solo aparece cuando se establece una conexión directa al PGXL y entrega el primer estado del modo de ventilador. Haga clic para recorrer los modos STANDARD, CONTEST y BROADCAST.
- La etiqueta **Vdd** muestra una raya cuando la alimentación de drenaje está apagada (tensión por debajo de 1.0 V), indicando claramente que la alimentación está apagada en lugar de marcar cero.

## Solución de problemas

- **El botón de bandeja AMP no es visible** — La radio no ha detectado un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **El indicador MEffA no aparece** — El applet oculta este indicador hasta la primera actualización de telemetría. Espere a que el PGXL envíe una medición de eficiencia, o verifique la conexión del amplificador.
- **El botón OPERATE no aparece** — El botón está oculto hasta que el amplificador envíe su primer reporte de estado. Espere a que el PGXL se conecte completamente.
- **El botón Fan Speed no aparece** — El botón está oculto hasta que una conexión directa al PGXL entregue el primer estado del modo de ventilador. Asegúrese de que el PGXL esté conectado directamente y enviando telemetría del modo de ventilador.
- **Falta el indicador antiguo de Voltios/Amperios** — En v26.6.1, el indicador de texto Voltios/Amperios fue reemplazado por indicadores separados Vdd, Vac e Id. Use el nuevo indicador Id para la corriente de drenaje y las etiquetas Vdd/Vac para las lecturas de tensión.

## Relacionado

- [Descripción general del amplificador](overview.md)
- [Monitorear potencia directa y ROE a la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
