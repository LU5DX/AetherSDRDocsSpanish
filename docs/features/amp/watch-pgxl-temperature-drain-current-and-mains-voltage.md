# Ver telemetría del PGXL y controlar OPERATE/STANDBY

El applet del amplificador muestra telemetría en vivo de un Power Genius XL conectado: potencia directa, ROE, corriente de drenaje, temperatura del disipador, tensión de red y eficiencia del amplificador. También proporciona un botón OPERATE/STANDBY para controlar el estado del amplificador y un botón de velocidad del ventilador para cambiar entre los modos de ventilador.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- Un amplificador Power Genius XL debe ser detectado por la radio. El botón de la bandeja AMP no aparece hasta que la radio reporta un PGXL.

## Pasos

1. Localice el botón de la bandeja AMP en la barra lateral derecha del panel del applet.
2. Haga clic en AMP para abrir el applet del amplificador.
3. Lea el indicador **PWR** para la potencia directa. La barra se vuelve roja por encima de 1500 W; el rango válido es 0–2000 W. La barra sube rápidamente en ráfagas de RF y decae en ~800 ms para mantener visibles las transmisiones breves.
4. Lea el indicador **SWR**. La barra se vuelve roja por encima de 2.5; el rango válido es 1.0–3.0. El indicador se limpia a 1.0 cuando la potencia directa cae por debajo de 5 W y restaura el valor en caché cuando la potencia se reanuda.
5. Lea el indicador **Id** para la corriente de drenaje. La barra se vuelve roja por encima de 60 A; el rango válido es 0–70 A.
6. Lea el texto **Temp** para la temperatura del disipador. Haga clic en la etiqueta de temperatura para alternar entre Celsius y Fahrenheit. La etiqueta de temperatura es un botón en el que se puede hacer clic; la unidad actual se indica con el sufijo °C o °F.
7. Lea el texto **Vdd** para la tensión de drenaje. Muestra un guion cuando la alimentación de drenaje está apagada (tensión por debajo de 1.0 V).
8. Lea el texto **Vac** para la tensión de red.
9. Lea el indicador **MEffA** para la métrica de eficiencia del amplificador (añadido en v26.5.1). Este indicador está oculto hasta que llega la primera telemetría.
10. Haga clic en el botón **Fan Speed** para cambiar entre los modos STANDARD, CONTEST y BROADCAST. El botón muestra el modo actual como "Fan: Std", "Fan: Contest" o "Fan: Bcast". El botón está oculto hasta que llega el primer estado del modo de ventilador desde una conexión PGXL directa. Añadido en v26.6.3.
11. Haga clic en **OPERATE** para alternar el amplificador entre OPERATE y STANDBY. El botón muestra "OPERATE" (verde) cuando el amplificador está en estado IDLE, OPERATE o TRANSMIT_*, y "STANDBY" en caso contrario. El botón está oculto hasta que llega el primer informe de estado.

## Qué hace cada control

| Control | Qué muestra | Umbral rojo | Notas |
|---|---|---|---|
| PWR | Potencia directa del PGXL | > 1500 W | Indicador con decaimiento balístico para transmisiones breves; nombre accesible "Forward power" |
| SWR | ROE del PGXL | > 2.5 | Se limpia a 1.0 cuando la potencia directa cae por debajo de 5 W; nombre accesible "SWR" |
| Id | Corriente de drenaje del PGXL | > 60 A | Nombre accesible "Drain current" |
| Temp | Temperatura del disipador del PGXL | > 80 °C | Botón en el que se puede hacer clic para alternar entre Celsius y Fahrenheit. Muestra "Temp: xx.x C" o "Temp: xx.x F". La configuración se conserva entre sesiones. Añadido en v26.7.4 |
| Vdd | Tensión de drenaje del PGXL | — | Muestra un guion cuando está por debajo de 1.0 V |
| Vac | Tensión de red del PGXL | — | Se muestra como etiqueta de texto |
| MEffA | Métrica de eficiencia del amplificador PGXL | — | Oculto hasta la primera telemetría. Añadido en v26.5.1 |
| Fan Speed | Cambiar entre STANDARD / CONTEST / BROADCAST | — | Oculto hasta que una conexión PGXL directa entrega el modo de ventilador. Muestra "Fan: Std", "Fan: Contest" o "Fan: Bcast". Añadido en v26.6.3 |
| OPERATE | Alternar el amplificador entre OPERATE y STANDBY | — | Oculto hasta el primer informe de estado. Verde para OPERATE, color por defecto para STANDBY |

## Consejos

- El indicador **PWR** utiliza decaimiento balístico para mantener visibles las transmisiones breves: la barra sube inmediatamente con RF y decae en aproximadamente 800 ms.
- El indicador **SWR** se limpia automáticamente a 1.0 cuando la potencia directa cae por debajo de 5 W porque la ROE no es significativa en reposo. El valor en caché se restaura cuando la potencia se reanuda.
- El indicador **MEffA** permanece oculto hasta que el PGXL envía su primera telemetría de eficiencia. Si no aparece, es posible que el amplificador aún no esté enviando esta métrica.
- El botón **OPERATE** se mantiene sincronizado con el estado autoritativo de la radio. Si el estado del PGXL cambia a través de la ruta TCP directa, el botón se actualiza inmediatamente (v0.9.8+).
- El indicador **Temp** utiliza tres zonas de color: verde por debajo de 55 °C, amarillo de 55 °C a 80 °C y rojo por encima de 80 °C. Al cambiar a Fahrenheit, los umbrales equivalentes son: verde por debajo de 131 °F, amarillo de 131 °F a 176 °F y rojo por encima de 176 °F.
- El botón **Fan Speed** solo aparece cuando se establece una conexión PGXL directa y entrega el primer estado del modo de ventilador. Haga clic para cambiar entre los modos STANDARD, CONTEST y BROADCAST.
- La etiqueta **Vdd** muestra un guion cuando la alimentación de drenaje está apagada (tensión por debajo de 1.0 V), indicando claramente que la alimentación está apagada en lugar de mostrar cero.
- La configuración de **Temp** (Celsius/Fahrenheit) se guarda por sesión y se restaura al reiniciar.

## Solución de problemas

- **El botón de la bandeja AMP no es visible** — La radio no ha detectado un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **El indicador MEffA no aparece** — El applet oculta este indicador hasta la primera actualización de telemetría. Espere a que el PGXL envíe una medición de eficiencia, o verifique la conexión del amplificador.
- **El botón OPERATE no aparece** — El botón está oculto hasta que el amplificador envía su primer informe de estado. Espere a que el PGXL se conecte completamente.
- **El botón Fan Speed no aparece** — El botón está oculto hasta que una conexión PGXL directa entrega el primer estado del modo de ventilador. Asegúrese de que el PGXL esté conectado directamente y enviando telemetría del modo de ventilador.
- **El botón Temp no responde** — Asegúrese de hacer clic directamente en la etiqueta de texto de temperatura, no en el área circundante. El botón tiene un efecto de resaltado al pasar el cursor que indica cuándo está activo.
- **El indicador antiguo de Volts/Amps falta** — En v26.6.1, el indicador de texto de Volts/Amps fue reemplazado por los indicadores separados Vdd, Vac e Id. Utilice el nuevo indicador Id para la corriente de drenaje y las etiquetas Vdd/Vac para las lecturas de tensión.

## Relacionado

- [Descripción general del amplificador](overview.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
