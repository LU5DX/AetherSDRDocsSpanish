# Descripción general del amplificador

El applet Amplifier proporciona telemetría en tiempo real y control OPERATE/STANDBY para un amplificador Power Genius XL (PGXL) conectado. Úselo para monitorear la potencia directa, la ROE, la corriente de drenaje, la temperatura, el voltaje de drenaje, el voltaje de red y la velocidad del ventilador.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- La radio debe detectar un amplificador Power Genius XL. El applet y su botón de bandeja están ocultos hasta que la radio informe de un PGXL.

## Cómo funciona

El applet Amplifier aparece en el panel de applets del lado derecho cuando AetherSDR detecta un amplificador PGXL en la red. Ábralo o ciérrelo con el botón de bandeja **AMP** en la barra lateral derecha.

Toda la telemetría se envía desde la radio en tiempo real. Los medidores se actualizan a medida que el PGXL informa nuevos valores; no se necesita sondeo ni actualización manual. Las etiquetas de valor en vivo (PWR, SWR, Id) se actualizan a 10 Hz para evitar parpadeos, y la balística del medidor ofrece una sensación de retención de pico con liberación lenta que coincide con el S-meter. El botón **OPERATE** / **STANDBY** refleja el estado actual del amplificador y le permite alternar entre ambos.

En v26.7.4, la visualización de temperatura ganó un conmutador de unidades. Haga clic en la etiqueta de temperatura para alternar entre Celsius (°C) y Fahrenheit (°F); la elección se conserva entre sesiones. En v26.8.4, el control de velocidad del ventilador cambió de un botón cíclico a un menú desplegable que muestra los tres modos.

## Qué hace cada control

| Control                                        | Tipo                                                                                                                                                                                      | Comportamiento                                                                                                                                                                                                                                                                             |
|------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **PWR**                                        | Valor + Medidor                                                                                                                                                                           | Muestra la potencia directa de salida del PGXL como valor numérico y medidor. El medidor muestra una marca de pico blanca sostenida durante 2,5 s después del último pico nuevo. La etiqueta numérica solo muestra un valor cuando la potencia es >= 5 W. El medidor se pone rojo por encima de 1500 W. El medidor de ROE se reinicia a 1.0 cuando la potencia directa baja de 5 W. |
| **SWR**                                        | Valor + Medidor                                                                                                                                                                           | Muestra la ROE del PGXL en la salida del amplificador como valor numérico y medidor. El medidor se pone rojo por encima de 2.5. La etiqueta numérica solo aparece cuando la potencia directa es de 5 W o más; la ROE no es significativa en reposo.                                              |
| **Id**                                         | Valor + Medidor                                                                                                                                                                           | Muestra la corriente de drenaje del PGXL como valor numérico y medidor. La etiqueta numérica solo aparece cuando la corriente es >= 0.5 A. El medidor se pone rojo por encima de 60 A.                                                                                                        |
| **Temp**                                       | Texto en el que se puede hacer clic                                                                                                                                                       | Muestra la temperatura del disipador del PGXL como `xx.x C` (predeterminado) o `xx.x F`. Haga clic para alternar entre Celsius y Fahrenheit. La preferencia se guarda y se restaura en la siguiente sesión. Muestra `tempA/tempB °C` cuando ambos sensores informan, o `tempA °C` en caso contrario. Añadido en v26.7.4. |
| **Vdd**                                        | Indicador de texto                                                                                                                                                                        | Muestra el voltaje de drenaje del PGXL como `Vdd xx V` en una conexión directa al PGXL. Muestra un guion cuando la fuente de drenaje está apagada (vdd < 1 V) o cuando se conecta a través del proxy de la radio. Se atenúa cuando se usa el proxy a través de la radio.                     |
| **Vac**                                        | Indicador de texto                                                                                                                                                                        | Muestra el voltaje de red del PGXL como `Vac xx V` en una conexión directa al PGXL. Solo se actualiza en conexión directa; se atenúa cuando se usa el proxy a través de la radio.                                                                                                             |
| **● RADIO** / **● DIRECT**                     | Indicador de texto                                                                                                                                                                        | Muestra la fuente de los datos de telemetría. `● RADIO` cuando se usa el proxy a través de la radio, `● DIRECT` cuando se lee directamente del PGXL. Vdd/Vac/modo de ventilador solo están disponibles en la ruta DIRECT.                                                                      |
| **Fan speed** (cuadro combinado)               | Lista desplegable                                                                                                                                                                         | Selecciona el modo de ventilador del PGXL entre STANDARD, CONTEST y BROADCAST. Oculto hasta que una conexión directa al PGXL entregue el primer estado de modo de ventilador. Usa GuardedComboBox para que el desplazamiento accidental de la rueda del ratón al pasar el cursor no cambie el modo de ventilador cuando la lista está cerrada (#3905). |
| **OPERATE**                                    | Botón                                                                                                                                                                                     | Alterna el amplificador entre OPERATE y STANDBY. Oculto hasta que la radio informe del estado del amplificador. Muestra **OPERATE** (verde) cuando el PGXL está en estado IDLE, OPERATE, TRANSMIT_A o TRANSMIT_B. Muestra **STANDBY** cuando el PGXL está en estado STANDBY, POWERUP o FAULT. |

Los tres medidores usan una barra codificada por colores: verde por debajo del umbral amarillo, amarillo-ámbar en la zona de precaución y rojo por encima del umbral rojo. Las etiquetas de graduación de cada medidor están coloreadas según su zona.

La preferencia de unidad de temperatura es el único ajuste persistente: todos los demás valores provienen en vivo del PGXL.

## Diseño

El applet Amplifier muestra la telemetría en dos secciones:

1. **Sección superior:** Tres filas, cada una con una etiqueta a la izquierda y un medidor a la derecha:
   - **PWR** — potencia directa (0–2000 W, rojo > 1500 W)
   - **SWR** — ROE (1.0–3.0, rojo > 2.5)
   - **Id** — corriente de drenaje (0–70 A, rojo > 60 A)

2. **Sección inferior:** Una pila de información de texto a la izquierda y el botón **OPERATE** a la derecha:
   - Temperatura (Temp, en la que se puede hacer clic para alternar °C/°F)
   - Voltaje de drenaje (Vdd)
   - Voltaje de red (Vac)
   - Indicador de fuente de datos (`● RADIO` / `● DIRECT`)
   - Control de velocidad del ventilador (desplegable)

Las etiquetas de valor numérico (PWR, SWR, Id) muestran el nombre del campo y el valor en vivo en texto azul claro y negrita.

## Conmutador de unidad de temperatura

- Haga clic en la etiqueta de temperatura para alternar entre Celsius y Fahrenheit.
- La unidad elegida se conserva entre sesiones de AetherSDR.
- La etiqueta muestra un decimal independientemente de la unidad.
- La información sobre herramientas anuncia la unidad a la que se cambiará al hacer clic.

## Control de velocidad del ventilador

- Seleccione el modo de ventilador en el desplegable **Fan speed**: STANDARD, CONTEST o BROADCAST.
- El control está oculto hasta que una conexión directa al PGXL entregue el primer estado de modo de ventilador.
- El desplegable evita cambios accidentales del modo de ventilador por el desplazamiento de la rueda del ratón al pasar el cursor sobre el control cuando la lista está cerrada.

## Accesibilidad

Todos los medidores tienen nombres accesibles establecidos como "Forward power", "SWR" y "Drain current", respectivamente. El control de velocidad del ventilador establece su nombre accesible dinámicamente, por ejemplo "Fan speed: STANDARD". El botón de alternar temperatura tiene una descripción accesible "Toggles amplifier temperature between Celsius and Fahrenheit" y se puede alcanzar con el foco de la tecla Tab.

## Relacionado

- [Put the PGXL amplifier in OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Put the PGXL amplifier in STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Monitor forward power and SWR at the amplifier output](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Watch PGXL temperature, drain current, and mains voltage](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- Change PGXL fan speed
