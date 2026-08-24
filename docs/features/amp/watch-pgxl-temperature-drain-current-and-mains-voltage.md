# Ver telemetría del PGXL y controlar OPERATE/STANDBY

El applet Amplifier muestra telemetría en vivo de un Power Genius XL conectado: potencia directa, ROE, corriente de drenaje, temperatura del disipador (conmutable °C/°F), voltaje de drenaje y de red (conexión directa), modo de velocidad del ventilador y estado operate/standby. También proporciona un botón OPERATE/STANDBY para controlar el estado del amplificador y un selector de velocidad del ventilador.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El radio debe detectar un amplificador Power Genius XL. El botón de la bandeja AMP no aparece hasta que el radio reporta un PGXL.

## Pasos

1. Localice el botón de la bandeja AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet Amplifier.
3. Lea el indicador **PWR** para la potencia directa. La barra se pone roja por encima de 1500 W; el rango válido es de 0 a 2000 W. El indicador muestra una marca de pico blanca sostenida durante 2,5 s después del último pico nuevo. La etiqueta numérica solo muestra un valor cuando la potencia es de al menos 5 W.
4. Lea el indicador **SWR**. La barra se pone roja por encima de 2.5; el rango válido es de 1.0 a 3.0. El indicador se limpia a 1.0 cuando la potencia directa baja de 5 W y restaura el valor almacenado en caché cuando la potencia se reanuda. La etiqueta numérica solo aparece cuando la potencia directa es de al menos 5 W.
5. Lea el indicador **Id** para la corriente de drenaje. La barra se pone roja por encima de 60 A; el rango válido es de 0 a 70 A. La etiqueta numérica solo aparece cuando la corriente es de al menos 0.5 A.
6. Lea el texto **Temp** para la temperatura del disipador. Haga clic en la etiqueta de temperatura para alternar entre Celsius y Fahrenheit; la elección se conserva entre sesiones. La etiqueta muestra "tempA/tempB °C" cuando ambos sensores reportan, o "tempA °C" en caso contrario.
7. Lea el texto **Vdd** para el voltaje de drenaje en una conexión PGXL directa. Muestra un guion cuando la fuente de drenaje está apagada (voltaje por debajo de 1.0 V) o cuando se conecta mediante el proxy del radio.
8. Lea el texto **Vac** para el voltaje de red en una conexión PGXL directa.
9. Lea la **etiqueta de fuente** para ver si la telemetría se realiza mediante proxy a través del radio (● RADIO) o se lee directamente del PGXL (● DIRECT).
10. Seleccione el menú desplegable **Fan Speed** para elegir el modo de ventilador STANDARD, CONTEST o BROADCAST. El menú desplegable está oculto hasta que una conexión PGXL directa entrega el primer estado del modo de ventilador.
11. Haga clic en **OPERATE** para alternar el amplificador entre OPERATE y STANDBY. El botón muestra "OPERATE" (verde) cuando el amplificador está en estado IDLE, OPERATE o TRANSMIT_*, y "STANDBY" en caso contrario. El botón está oculto hasta que llega el primer informe de estado.

## Qué hace cada control

| Control | Qué muestra | Umbral rojo | Notas |
|---|---|---|---|
| PWR | Potencia directa del PGXL | > 1500 W | Marca de pico blanca sostenida durante 2,5 s; etiqueta numérica solo cuando la potencia ≥ 5 W; la balística da una sensación de retención de pico de liberación lenta que coincide con el S-meter |
| SWR | ROE del PGXL | > 2.5 | Se limpia a 1.0 cuando la potencia directa baja de 5 W; etiqueta numérica solo cuando la potencia ≥ 5 W |
| Id | Corriente de drenaje del PGXL | > 60 A | Etiqueta numérica solo cuando la corriente ≥ 0.5 A |
| Temp | Temperatura del disipador del PGXL | — | Botón clicable que alterna entre Celsius y Fahrenheit; se guarda en el objeto de configuración `AmpApplet` (campo `tempFahrenheit`). Muestra "tempA/tempB °C" cuando ambos sensores reportan, o "tempA °C" en caso contrario |
| Vdd | Voltaje de drenaje del PGXL | — | Muestra "Vdd x.x V" en conexión directa; guion cuando está por debajo de 1.0 V o mediante proxy a través del radio. Atenuado cuando se usa proxy |
| Vac | Voltaje de red del PGXL | — | Muestra "Vac N V" en conexión directa. Atenuado cuando se usa proxy |
| Etiqueta de fuente | Fuente de telemetría | — | "● RADIO" cuando se usa proxy a través del radio, "● DIRECT" cuando se lee directamente del PGXL |
| Fan Speed | Seleccionar STANDARD / CONTEST / BROADCAST | — | Cuadro combinado; oculto hasta que la conexión directa entrega el modo de ventilador. Emite el modo en mayúsculas para `sendCommand`. Usa un cuadro combinado protegido para que el desplazamiento de la rueda del ratón al pasar por encima no cambie el modo cuando el menú desplegable está cerrado |
| OPERATE | Alternar el amplificador entre OPERATE y STANDBY | — | Oculto hasta el primer informe de estado. Muestra "OPERATE" (verde) para estados IDLE/OPERATE/TRANSMIT_*, "STANDBY" en caso contrario |

## Consejos

- Las etiquetas de valores en vivo (PWR / SWR / Id) se actualizan a 10 Hz para evitar parpadeos.
- El indicador **PWR** muestra una marca de pico blanca sostenida durante 2,5 s después del último pico nuevo. La balística del indicador da una sensación de retención de pico de liberación lenta que coincide con el S-meter.
- El indicador **SWR** se limpia automáticamente a 1.0 cuando la potencia directa baja de 5 W porque la ROE no es significativa en reposo. El valor almacenado en caché se restaura cuando la potencia se reanuda.
- El cuadro combinado **Fan Speed** solo aparece cuando se establece una conexión PGXL directa y entrega el primer estado del modo de ventilador. Seleccione el modo deseado en el menú desplegable; no es necesario recorrer los modos a ciegas.
- Las etiquetas **Vdd** y **Vac** solo se actualizan en una conexión PGXL directa. Cuando la telemetría se realiza mediante proxy a través del radio, están atenuadas. La **etiqueta de fuente** le indica qué ruta está activa.
- El botón **OPERATE** se mantiene sincronizado con el estado autoritativo del radio (`RadioModel::ampStateChanged`, #2437). Si el estado del PGXL cambia mediante la ruta TCP directa, el botón se actualiza de inmediato.
- La información sobre herramientas de **Temp** anuncia la unidad a la que se cambiaría al hacer clic.
- La configuración de **Temp** (Celsius/Fahrenheit) se guarda por sesión y se restaura al reiniciar.

## Solución de problemas

- **El botón de la bandeja AMP no es visible** — El radio no ha detectado un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **El botón OPERATE no aparece** — El botón está oculto hasta que el amplificador envía su primer informe de estado. Espere a que el PGXL se conecte por completo.
- **El menú desplegable Fan Speed no aparece** — El menú desplegable está oculto hasta que una conexión PGXL directa entrega el primer estado del modo de ventilador. Asegúrese de que el PGXL esté conectado directamente y esté enviando telemetría del modo de ventilador.
- **Las etiquetas Vdd/Vac están atenuadas** — Estos valores solo están disponibles en una conexión PGXL directa. Cuando la telemetría se realiza mediante proxy a través del radio, no se actualizan.
- **El botón Temp no responde** — Asegúrese de hacer clic directamente en la etiqueta de texto de temperatura, no en el área circundante. El botón tiene un efecto de resaltado al pasar el cursor que se activa cuando está en uso.
- **Falta el indicador Volts/Amps anterior** — En v26.6.1, el indicador de texto Volts/Amps se reemplazó por indicadores separados Vdd, Vac e Id. Use el nuevo indicador Id para la corriente de drenaje y las etiquetas Vdd/Vac para las lecturas de voltaje.

## Relacionado

- [Descripción general del amplificador](overview.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
