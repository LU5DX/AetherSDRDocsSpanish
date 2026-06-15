# Resumen del amplificador

El applet Amplificador proporciona telemetría en tiempo real y control OPERATE/STANDBY para un amplificador Power Genius XL (PGXL) conectado. Úselo para monitorear la potencia directa, la ROE, la corriente de drenaje, la temperatura, el voltaje de drenaje, el voltaje de la red eléctrica, la eficiencia del amplificador y la velocidad del ventilador.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- La radio debe detectar un amplificador Power Genius XL. El applet y su botón en la bandeja están ocultos hasta que la radio reporta un PGXL.

## Cómo funciona

El applet Amplificador aparece en el panel de applets del lado derecho cuando AetherSDR detecta un amplificador PGXL en la red. Ábralo o ciérrelo con el botón **AMP** en la bandeja de la barra lateral derecha.

Toda la telemetría se envía desde la radio en tiempo real. Los indicadores se actualizan a medida que el PGXL reporta nuevos valores; no es necesario sondear ni actualizar manualmente. El botón **OPERATE** / **STANDBY** refleja el estado actual del amplificador y le permite cambiar entre ambos estados.

## Qué hace cada control

| Control          | Tipo            | Comportamiento                                                                                                                                                                                                                                                              |
|------------------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **PWR**          | Valor + Indicador | Muestra la potencia directa de salida del PGXL como un valor numérico y en un indicador gráfico. La barra del indicador sube rápidamente durante las ráfagas de RF y disminuye en unos ~800 milisegundos, lo que hace visibles las transmisiones breves. El indicador se pone rojo por encima de 1500 W. El indicador de ROE se reinicia a 1.0 cuando la potencia directa cae por debajo de 5 W. |
| **SWR**          | Valor + Indicador | Muestra la ROE del PGXL en la salida del amplificador como un valor numérico y en un indicador gráfico. El indicador se pone rojo por encima de 2.5. El indicador solo se actualiza cuando la potencia directa es de 5 W o más; la ROE no es significativa en reposo.                                                                   |
| **Id**           | Valor + Indicador | Muestra la corriente de drenaje del PGXL como un valor numérico y en un indicador gráfico. El indicador se pone rojo por encima de 60 A.                                                                                                                                      |
| **Temp**         | Indicador de texto | Muestra la temperatura del disipador del PGXL como `xx C`.                                                                                                                                                                                                                  |
| **Vdd**          | Indicador de texto | Muestra el voltaje de drenaje del PGXL como `Vdd xx V`. Cuando la alimentación de drenaje está apagada (standby), muestra `Vdd — V` en lugar de `0.0 V`.                                                                                                                      |
| **Vac**          | Indicador de texto | Muestra el voltaje de la red eléctrica del PGXL como `Vac xx V`.                                                                                                                                                                                                            |
| **MEffA**        | Indicador de texto | Muestra la métrica de eficiencia del amplificador PGXL (meffa). Se oculta hasta que llega la primera telemetría de meffa. Añadido en v26.5.1.                                                                                                                               |
| **● RADIO**      | Indicador de texto | Muestra la fuente de los datos de telemetría. Aparece después de que llega la primera telemetría.                                                                                                                                                                          |
| **5** / **C** / **B** | Botón           | Botón de control de velocidad del ventilador (una sola letra: **5** para STANDARD, **C** para CONTEST, **B** para BROADCAST). Se oculta hasta que una conexión directa PGXL entrega el primer estado del modo del ventilador. Haga clic para recorrer las tres velocidades. Mejorado en v26.6.3. |
| **OPERATE**      | Botón           | Cambia el amplificador entre OPERATE y STANDBY. Se oculta hasta que la radio reporta el estado del amplificador. Muestra **OPERATE** (verde) cuando el PGXL está en estado IDLE, OPERATE, TRANSMIT_A o TRANSMIT_B. Muestra **STANDBY** cuando el PGXL está en estado STANDBY, POWERUP o FAULT. |

Los tres indicadores gráficos utilizan una barra codificada por colores: verde por debajo del umbral amarillo, amarillo-ámbar en la zona de precaución y rojo por encima del umbral rojo. Las etiquetas de las marcas en cada indicador tienen el color correspondiente a su zona.

Ninguno de los controles tiene configuraciones persistentes; todos los valores provienen en vivo del PGXL.

## Disposición

El applet Amplificador muestra la telemetría en dos secciones:

1. **Sección superior:** Tres filas, cada una con una etiqueta a la izquierda y un indicador gráfico a la derecha:
   - **PWR** — potencia directa (0–2000 W, rojo > 1500 W)
   - **SWR** — ROE (1.0–3.0, rojo > 2.5)
   - **Id** — corriente de drenaje (0–70 A, rojo > 60 A)

2. **Sección inferior:** Una pila de información de texto a la izquierda y el botón **OPERATE** a la derecha:
   - Temperatura (Temp)
   - Voltaje de drenaje (Vdd)
   - Voltaje de la red eléctrica (Vac)
   - Eficiencia del amplificador (MEffA)
   - Indicador de fuente de datos (`● RADIO`)
   - Botón de control de velocidad del ventilador

Las etiquetas de valor numérico (PWR, SWR, Id) muestran el nombre del campo y el valor en vivo en texto azul claro y negrita.

## Accesibilidad

Todos los indicadores gráficos tienen nombres accesibles establecidos como "Forward power", "SWR" y "Drain current" respectivamente. El botón de velocidad del ventilador establece su nombre accesible de forma dinámica, por ejemplo "Fan speed: STANDARD".

## Relacionados

- [Put the PGXL amplifier in OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Put the PGXL amplifier in STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Monitor forward power and SWR at the amplifier output](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Watch PGXL temperature, drain current, and mains voltage](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Change PGXL fan speed](change-pgxl-fan-speed.md)
