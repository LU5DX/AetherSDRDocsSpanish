# Ponga el amplificador PGXL en STANDBY

Use esta página para cambiar un amplificador Power Genius XL conectado de OPERATE a STANDBY, deteniendo su amplificación de las señales transmitidas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El botón de la bandeja AMP aparece solo después de que se detecte un Power Genius XL.
- El applet Amplifier debe estar abierto. Si no está visible, haga clic en el botón AMP de la barra lateral derecha para mostrarlo.
- El botón OPERATE está oculto hasta que llegue el primer mensaje de estado del amplificador. Confirme que esté visible antes de continuar.

## Pasos

1. Abra el applet Amplifier haciendo clic en el botón AMP de la barra lateral derecha si no está ya visible.
2. Confirme que el botón OPERATE muestra la etiqueta "OPERATE" en verde. Esto indica que el amplificador se encuentra actualmente en un estado operativo (IDLE, OPERATE o TRANSMIT).
3. Haga clic en OPERATE.

La etiqueta del botón cambia a "STANDBY" y el fondo verde se reemplaza por el estilo oscuro predeterminado, confirmando que el amplificador ha pasado a STANDBY.

## Qué hace cada control

| Control                 | Comportamiento                                                                                                                                                                                 | Estados                                                                                                                                                                                                                |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OPERATE                 | Alterna el amplificador entre OPERATE y STANDBY; emite operateToggled.                                                                                                                 | Oculto hasta que llega setState. Muestra 'OPERATE' (verde) para los estados IDLE/OPERATE/TRANSMIT_*, 'STANDBY' en caso contrario (sincronizado mediante RadioModel::ampStateChanged, #2437).                                                 |
| Velocidad del ventilador               | Selecciona el modo de ventilador del PGXL; emite fanModeChanged con el modo en mayúsculas.                                                                                                                 | Oculto hasta que una conexión directa al PGXL entrega el primer estado de modo de ventilador. Usa GuardedComboBox para que el desplazamiento accidental de la rueda del ratón al pasar por encima no cambie el modo de ventilador cuando la lista desplegable está cerrada (#3905).           |
| Alternancia de unidad de temperatura | Haga clic en la pantalla de temperatura para alternar entre Celsius (°C) y Fahrenheit (°F). La configuración persiste entre reinicios de la aplicación.                                                      | Muestra la temperatura actual con un decimal. Oculto hasta que llega la primera telemetría.                                                                                                                               |
| PWR                     | Muestra la potencia directa del PGXL con una marca de pico blanca que se mantiene durante 2,5 s después del último pico nuevo; la etiqueta numérica solo muestra un valor cuando la potencia es >= 5 W.                                          | El medidor de SWR se restablece a 1.0 cuando la potencia baja de 5 W (no medible en reposo) y restaura el valor en caché cuando la potencia se reanuda.                                                                                           |
| SWR                     | Muestra la SWR del PGXL; la etiqueta numérica solo aparece cuando la potencia directa es >= 5 W.                                                                                                                |                                                                                                                                                                                                                       |
| Id                      | Muestra la corriente de drenaje del PGXL; la etiqueta numérica solo aparece cuando la corriente es >= 0.5 A.                                                                                                          |                                                                                                                                                                                                                       |
| Temp (botón C/F)       | Muestra la temperatura del amplificador (TEMP_A y TEMP_B si están presentes) y alterna entre Celsius y Fahrenheit al hacer clic. La elección se guarda en el objeto de configuración 'AmpApplet' (campo tempFahrenheit). | Muestra 'tempA/tempB °C' cuando ambos sensores informan, o 'tempA °C' en caso contrario. La información sobre herramientas anuncia la unidad a la que se cambiaría al hacer clic.                                                                                     |
| Vdd (voltaje de drenaje)     | Muestra el voltaje de drenaje 'Vdd x.x V' en una conexión directa al PGXL; muestra un guion cuando la fuente de drenaje está apagada (vdd < 1 V) o cuando se conecta mediante el proxy de la radio.                               | Solo se actualiza en una conexión directa; atenuado cuando se usa el proxy de la radio.                                                                                                                                       |
| Vac (voltaje de red)     | Muestra el voltaje de red 'Vac N V' en una conexión directa al PGXL.                                                                                                                              | Solo se actualiza en una conexión directa; atenuado cuando se usa el proxy de la radio.                                                                                                                                       |
| Etiqueta de fuente            | Indica si la telemetría se recibe a través del proxy de la radio (RADIO) o se lee directamente del PGXL (DIRECT).                                                                                | Vdd/Vac/modo de ventilador solo están disponibles en la ruta DIRECT.                                                                                                                                                               |

## Indicadores de telemetría

El applet Amplifier muestra los valores de telemetría del amplificador Power Genius XL conectado. Estos indicadores aparecen en la sección inferior del applet.

| Indicador | Formato de visualización | Rango | Comportamiento | Notas |
|-----------|---------------|-------|----------|-------|
| PWR | Valor numérico a la izquierda del medidor Fwd Pwr, p. ej., "1148" | 0-2000 W | Muestra la potencia directa del PGXL en vatios. La barra del medidor sube rápidamente con ráfagas de RF pero decae en aproximadamente 800 ms, manteniendo la sensación de retención de pico del S-meter. El medidor se pone en rojo por encima de 1500 W. El medidor de SWR se restablece a 1.0 cuando la potencia directa baja de 5 W (reposo). Cuando la potencia directa vuelve a superar los 5 W, el medidor de SWR restaura el valor en caché. | Añadido en v26.6.1. La etiqueta de valor reemplaza la etiqueta anterior "Fwd Pwr". |
| SWR | Valor numérico a la izquierda del medidor de SWR | 1.0-3.0 | Muestra la SWR del PGXL. El medidor se pone en rojo por encima de 2.5. El medidor solo muestra un valor cuando la potencia directa es de 5 W o más — la SWR no es significativa en reposo y la radio/PGXL puede informar valores obsoletos o de ruido. | Añadido en v26.6.1. La etiqueta de valor reemplaza la etiqueta independiente del medidor anterior. |
| Id | Valor numérico a la izquierda del medidor | 0-70 A | Muestra la corriente de drenaje del PGXL (Id). El medidor se pone en rojo por encima de 60 A. | Añadido en v26.6.1. Reemplaza la pantalla de texto "Amps" anterior. |
| Temp | Etiqueta de texto en la que se puede hacer clic, p. ej., "45.0 °C" o "113.0 °F" | — | Muestra la temperatura del disipador del PGXL. Haga clic para alternar entre Celsius y Fahrenheit. La configuración persiste entre reinicios de la aplicación. | Oculto hasta que llega la primera telemetría. |
| Vdd | Etiqueta de texto, p. ej., "Vdd 50 V" o "Vdd — V" | — | Muestra el voltaje de drenaje del PGXL. Muestra "Vdd — V" cuando la fuente de drenaje está apagada (voltaje por debajo de 1.0 V) para indicar claramente que la fuente está apagada en lugar de leer cero. | Oculto hasta que llega la primera telemetría. |
| Vac | Etiqueta de texto, p. ej., "Vac 120 V" | — | Muestra el voltaje de red del PGXL. | Oculto hasta que llega la primera telemetría. |
| MEffA | Etiqueta de texto | — | Muestra la métrica de eficiencia del amplificador PGXL (meffa) reenviada desde la telemetría de la radio/proxy. | Oculto hasta que se llama a setMeff. Añadido en v26.5.1. |
| ● RADIO | Indicador de fuente | — | Muestra la fuente de los datos de telemetría. Siempre muestra "● RADIO". | Añadido en v26.6.1. |

## Cambios de diseño en v26.6.1

A partir de v26.6.1, el applet Amplifier tiene un diseño rediseñado:

- **Fila superior**: medidor PWR con etiqueta de valor numérico a la izquierda (p. ej., "PWR 1148")
- **Segunda fila**: medidor SWR con etiqueta de valor numérico a la izquierda (p. ej., "SWR 1.2")
- **Tercera fila**: medidor Id (corriente de drenaje) con etiqueta de valor numérico a la izquierda (p. ej., "Id 12.5")
- **Fila inferior**: temperatura (Temp, en la que se puede hacer clic), voltaje de drenaje (Vdd), voltaje de red (Vac) e indicador de fuente apilados a la izquierda, con el botón OPERATE a la derecha

La balística del medidor para PWR usa un ataque rápido (30 ms) y una liberación lenta (800 ms) para mantener visibles las transmisiones breves en el medidor.

## Control de velocidad del ventilador

La lista desplegable Fan speed aparece solo cuando una conexión directa al PGXL entrega el primer estado de modo de ventilador. El control está oculto hasta entonces.

- Seleccione el modo de ventilador deseado en la lista desplegable: STANDARD, CONTEST o BROADCAST.
- El texto de la lista desplegable muestra la etiqueta del modo: "Fan: Std", "Fan: Contest" o "Fan: Bcast".
- El nombre accesible se actualiza con el modo actual, p. ej., "Fan speed: STANDARD".
- La lista desplegable es un GuardedComboBox: el desplazamiento accidental de la rueda del ratón al pasar por encima no cambia el modo de ventilador cuando la lista está cerrada.
- La lista desplegable se redimensiona para ajustarse a la etiqueta de elemento más ancha ("Fan: Contest") y aplica el estilo de tema de la aplicación a la lista emergente.

## Alternancia de unidad de temperatura

La pantalla de temperatura funciona también como control. Haga clic en ella para cambiar entre Celsius y Fahrenheit.

- La temperatura se muestra con un decimal (p. ej., "45.0 °C" o "113.0 °F").
- La configuración persiste entre reinicios de la aplicación.
- El botón tiene un indicador de enfoque visible y efecto de desplazamiento.

## Solución de problemas

- **El botón de la bandeja AMP no está visible** — El applet está oculto hasta que la radio detecta un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **El botón OPERATE no está visible** — El botón está oculto hasta que llega el primer mensaje de estado del amplificador. Espere un momento después de abrir el applet; si no aparece, verifique la conexión del amplificador.
- **Hacer clic en OPERATE no tiene efecto** — Confirme que AetherSDR sigue conectado a la radio. Desconecte y vuelva a conectar si es necesario.
- **Los valores de telemetría muestran guiones** — Espere a que llegue el primer paquete de telemetría del amplificador. Si los valores no aparecen, verifique la conexión del amplificador y el enlace radio/proxy.
- **La lista desplegable Fan speed no está visible** — El control está oculto hasta que una conexión directa al PGXL entrega el primer estado de modo de ventilador. Espere a que se establezca la conexión; si no aparece, verifique que el PGXL esté conectado directamente (no mediante un proxy).
- **El medidor de SWR no muestra ningún valor** — El medidor solo muestra un valor cuando la potencia directa es de 5 W o más. Esto es normal; la SWR no es significativa cuando el amplificador está en reposo.

## Relacionado

- [Ponga el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Supervise la potencia directa y la SWR en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Observe la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Descripción general del amplificador](overview.md)
