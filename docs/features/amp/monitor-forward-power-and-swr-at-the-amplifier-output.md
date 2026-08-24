# Supervisar la potencia directa y la ROE en la salida del amplificador

El applet Amplifier muestra lecturas en tiempo real de potencia directa, ROE, corriente de drenaje y temperatura de un amplificador Power Genius XL (PGXL) conectado. Utilice estos medidores para confirmar la potencia de salida y la adaptación de la antena durante la transmisión, así como para supervisar el estado del amplificador.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- La radio debe detectar un amplificador Power Genius XL. El botón de la bandeja AMP no aparece hasta que el PGXL esté presente.

## Pasos

1. Localice el botón de la bandeja AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet Amplifier.
3. Transmita. Observe cómo los medidores PWR, SWR e Id se actualizan en tiempo real.

## Qué hace cada control

| Control             | Qué muestra                                                                                                                                                                            | Rango                                                                                                                                                                 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PWR                 | Muestra la potencia directa del PGXL con una marca de pico blanca que se mantiene durante 2,5 s después del último pico nuevo; la etiqueta numérica solo muestra un valor cuando la potencia es >= 5 W.                                         | 0–2000 W (rojo > 1500)                                                                                                                                                 |
| SWR                 | Muestra la ROE del PGXL; la etiqueta numérica solo aparece cuando la potencia directa es >= 5 W.                                                                                                                | 1,0–3,0 (rojo > 2,5)                                                                                                                                                   |
| Id                  | Muestra la corriente de drenaje del PGXL; la etiqueta numérica solo aparece cuando la corriente es >= 0,5 A.                                                                                                          | 0–70 A (rojo > 60)                                                                                                                                                     |
| Temp (botón C/F)    | Muestra la temperatura del amplificador (TEMP_A y TEMP_B si están presentes) y alterna entre Celsius y Fahrenheit al hacer clic. La elección se guarda en el objeto de configuración `AmpApplet` (campo tempFahrenheit). | Celsius / Fahrenheit. Muestra `tempA/tempB °C` cuando ambos sensores informan, o `tempA °C` en caso contrario. La información sobre herramientas indica la unidad a la que se cambiaría al hacer clic.               |
| Vdd (tensión de drenaje) | Muestra la tensión de drenaje `Vdd  x.x V` en una conexión directa al PGXL; muestra un guion cuando la fuente de drenaje está apagada (vdd < 1 V) o cuando se conecta a través del proxy de la radio.                               | Solo se actualiza en conexión directa; atenuado cuando se usa el proxy de la radio.                                                                                       |
| Vac (tensión de red) | Muestra la tensión de red `Vac  N V` en una conexión directa al PGXL.                                                                                                                              | Solo se actualiza en conexión directa; atenuado cuando se usa el proxy de la radio.                                                                                       |
| Etiqueta de fuente   | Indica si la telemetría se transmite a través de la radio (RADIO) o se lee directamente del PGXL (DIRECT).                                                                                | Vdd/Vac/modo de ventilador solo están disponibles en la ruta DIRECT.                                                                                                               |
| Velocidad del ventilador | Selecciona el modo del ventilador del PGXL; emite `fanModeChanged` con el modo en mayúsculas.                                                                                                               | STANDARD / CONTEST / BROADCAST                                                                                                                                        |
| OPERATE             | Alterna el amplificador entre OPERATE y STANDBY; emite `operateToggled`.                                                                                                               | Oculto hasta que llega `setState`. Muestra `OPERATE` (verde) para los estados IDLE/OPERATE/TRANSMIT_*, y `STANDBY` en caso contrario (se mantiene sincronizado mediante `RadioModel::ampStateChanged`).     |

Los tres medidores de barra (PWR, SWR, Id) se muestran como barras horizontales con una etiqueta en el lado izquierdo que indica el nombre del campo y el valor en vivo (p. ej., "PWR 1148"). La barra rellena se vuelve roja cuando el valor entra en la zona roja. Las marcas de escala se dibujan en la parte superior de cada medidor en los siguientes puntos de referencia:

- **PWR:** 0, 500, 1000, 1,5K, 2K
- **SWR:** 1, 1,5, 2, 2,5, 3
- **Id:** 0, 10, 20, 30, 40, 50, 60, 70

El medidor PWR tiene balística de liberación lenta: la barra sube rápidamente en ráfagas de RF pero decae en aproximadamente 800 ms, de modo que las transmisiones breves permanecen visibles. Esto proporciona una sensación de retención de pico con liberación lenta similar al S-meter. Las etiquetas de valor numérico (PWR, SWR, Id) se actualizan a 10 Hz para evitar parpadeo.

**Marca de pico del medidor PWR:** El medidor de potencia directa muestra una marca de pico blanca que se mantiene durante 2,5 segundos después del último pico nuevo, lo que facilita la lectura de picos de potencia breves.

**Comportamiento del medidor SWR:** El medidor de ROE solo se actualiza cuando la potencia directa es de al menos 5,0 W. Cuando la potencia directa cae por debajo de 5,0 W, el medidor de ROE se restablece a 1,0. Esto evita que se muestren valores obsoletos o de ruido cuando el amplificador está en reposo. El valor almacenado en caché se restaura cuando se reanuda la potencia.

**Comportamiento de la etiqueta Vdd:** Cuando la tensión de la fuente de drenaje (Vdd) cae por debajo de 1,0 V (lo que indica que la fuente de drenaje está apagada durante STANDBY), la etiqueta Vdd muestra "Vdd — V" en lugar de "Vdd 0,0 V" para mayor claridad.

**Selector de velocidad del ventilador:** El selector de velocidad del ventilador es un menú desplegable que aparece solo después de que una conexión directa al PGXL envía el primer estado de modo del ventilador. Seleccione STANDARD, CONTEST o BROADCAST en el menú desplegable. El selector utiliza un cuadro combinado protegido, por lo que el desplazamiento accidental con la rueda del ratón mientras se pasa el cursor sobre el selector cerrado no cambia el modo del ventilador; solo responde a la entrada de la rueda cuando el menú desplegable está abierto.

**Alternancia de unidad de temperatura:** La pantalla de temperatura es un botón en el que se puede hacer clic y que alterna entre Celsius y Fahrenheit. El botón muestra la temperatura actual con el símbolo de la unidad (p. ej., "40,5 °C" o "104,9 °F"). Haga clic en el botón para cambiar de unidad. La configuración se guarda y se recuerda entre reinicios.

Ninguno de los medidores tiene una clave de configuración persistente. Los valores son telemetría de solo lectura del PGXL.

## Consejos

- Los medidores de barra utilizan animación suavizada. Un pequeño retraso entre el valor real y la barra mostrada es normal durante condiciones que cambian rápidamente, como el inicio de una transmisión.
- Si la ROE entra en la zona roja (por encima de 2,5), revise su sistema de antena antes de continuar transmitiendo a alta potencia.
- El medidor de corriente de drenaje (Id) ayuda a supervisar el estado del amplificador. Si Id supera los 60 A, considere reducir la potencia de excitación.
- El campo MEffA muestra la métrica de eficiencia del amplificador PGXL. Este campo está oculto hasta que llega la telemetría.
- La etiqueta de texto Volts / Amps está oculta hasta que llega la primera telemetría.

## Solución de problemas

- **El botón de la bandeja AMP no es visible** — La radio no ha detectado el PGXL. Verifique que el amplificador esté encendido y conectado a la radio Flex. AetherSDR muestra el botón AMP solo después de que la radio informe que hay un amplificador presente.
- **Los medidores PWR y SWR no muestran movimiento durante la transmisión** — Confirme que el amplificador esté en estado OPERATE y no en STANDBY. Consulte [Put the PGXL amplifier in OPERATE](put-the-pgxl-amplifier-in-operate.md).
- **El selector de velocidad del ventilador no aparece** — Se requiere una conexión directa al PGXL. El selector se vuelve visible solo después de recibir el primer estado de modo del ventilador del amplificador.

## Relacionado

- [Amplifier overview](overview.md)
- [Put the PGXL amplifier in OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Put the PGXL amplifier in STANDBY](put-the-pgxl-amplifier-in-standby.md)
- Observe la temperatura del PGXL, la tensión de drenaje y la tensión de red.
