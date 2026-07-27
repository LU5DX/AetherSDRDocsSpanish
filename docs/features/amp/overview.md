# Resumen del amplificador

El applet Amplificador proporciona telemetría en tiempo real y control OPERATE/STANDBY para un amplificador Power Genius XL (PGXL) conectado. Úselo para monitorear la potencia directa, la ROE, la corriente de drenaje, la temperatura, el voltaje de drenaje, el voltaje de la red eléctrica, la eficiencia del amplificador y la velocidad del ventilador.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- Un amplificador Power Genius XL debe ser detectado por la radio. El applet y su botón en la bandeja están ocultos hasta que la radio reporte un PGXL.

## Cómo funciona

El applet Amplificador aparece en el panel derecho de applets cuando AetherSDR detecta un amplificador PGXL en la red. Ábralo o ciérrelo con el botón de bandeja **AMP** en la barra lateral derecha.

Toda la telemetría se envía desde la radio en tiempo real. Los indicadores se actualizan a medida que el PGXL reporta nuevos valores; no es necesario sondear ni actualizar manualmente. El botón **OPERATE** / **STANDBY** refleja el estado actual del amplificador y le permite cambiar entre ambos.

En la v26.7.4, la pantalla de temperatura ganó un conmutador de unidad. Haga clic en la etiqueta de temperatura para cambiar entre Celsius (°C) y Fahrenheit (°F); la elección se conserva entre sesiones.

## Qué hace cada control

| Control             | Tipo              | Comportamiento                                                                                                                                                                                                                                                          |
|---------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **PWR**             | Valor + Indicador | Muestra la potencia de salida directa del PGXL como un valor numérico y un indicador. La barra del indicador sube rápidamente en las ráfagas de RF y disminuye en unos 800 milisegundos, lo que permite ver transmisiones breves. El indicador se vuelve rojo por encima de 1500 W. El indicador de ROE se reinicia a 1.0 cuando la potencia directa cae por debajo de 5 W. |
| **SWR**             | Valor + Indicador | Muestra la ROE del PGXL en la salida del amplificador como un valor numérico y un indicador. El indicador se vuelve rojo por encima de 2.5. El indicador solo se actualiza cuando la potencia directa es de 5 W o más; la ROE no es significativa en reposo.                                          |
| **Id**              | Valor + Indicador | Muestra la corriente de drenaje del PGXL como un valor numérico y un indicador. El indicador se vuelve rojo por encima de 60 A.                                                                                                                                        |
| **Temp**            | Texto en el que se puede hacer clic | Muestra la temperatura del disipador del PGXL como `xx.x C` (predeterminado) o `xx.x F`. Haga clic para alternar entre Celsius y Fahrenheit. La preferencia se guarda y restaura en la próxima sesión. Añadido en v26.7.4.                                         |
| **Vdd**             | Indicador de texto | Muestra el voltaje de drenaje del PGXL como `Vdd xx V`. Cuando la fuente de drenaje está apagada (standby), muestra `Vdd — V` en lugar de `0.0 V`.                                                                                                                    |
| **Vac**             | Indicador de texto | Muestra el voltaje de la red eléctrica del PGXL como `Vac xx V`.                                                                                                                                                                                                        |
| **MEffA**           | Indicador de texto | Muestra la métrica de eficiencia del amplificador PGXL (meffa). Oculto hasta que llegue la primera telemetría de meffa. Añadido en v26.5.1.                                                                                                                            |
| **● RADIO**         | Indicador de texto | Muestra la fuente de los datos de telemetría. Aparece después de que llegue la primera telemetría.                                                                                                                                                                     |
| **Fan: Std** / **Fan: Contest** / **Fan: Bcast** | Botón | Botón de control de velocidad del ventilador con etiqueta textual. Oculto hasta que una conexión directa al PGXL entregue el primer estado del modo del ventilador. Haga clic para recorrer STANDARD, CONTEST y BROADCAST. En v26.7.4, la etiqueta cambió de una sola letra (S/C/B) a un texto descriptivo. |
| **OPERATE**         | Botón            | Cambia el amplificador entre OPERATE y STANDBY. Oculto hasta que la radio reporte el estado del amplificador. Muestra **OPERATE** (verde) cuando el PGXL está en estado IDLE, OPERATE, TRANSMIT_A o TRANSMIT_B. Muestra **STANDBY** cuando el PGXL está en estado STANDBY, POWERUP o FAULT. |

Los tres indicadores usan una barra codificada por colores: verde por debajo del umbral amarillo, amarillo-ámbar en la zona de precaución y rojo por encima del umbral rojo. Las marcas de graduación en cada indicador tienen el color de su zona correspondiente.

La preferencia de unidad de temperatura es la única configuración persistente; todos los demás valores provienen en vivo del PGXL.

## Disposición

El applet Amplificador muestra la telemetría en dos secciones:

1. **Sección superior:** Tres filas, cada una con una etiqueta a la izquierda y un indicador a la derecha:
   - **PWR** — potencia directa (0–2000 W, rojo > 1500 W)
   - **SWR** — ROE (1.0–3.0, rojo > 2.5)
   - **Id** — corriente de drenaje (0–70 A, rojo > 60 A)

2. **Sección inferior:** Una pila de información textual a la izquierda y el botón **OPERATE** a la derecha:
   - Temperatura (Temp, se puede hacer clic para alternar °C/°F)
   - Voltaje de drenaje (Vdd)
   - Voltaje de la red eléctrica (Vac)
   - Eficiencia del amplificador (MEffA)
   - Indicador de fuente de datos (`● RADIO`)
   - Botón de control de velocidad del ventilador

Las etiquetas de valor numérico (PWR, SWR, Id) muestran el nombre del campo y el valor en vivo en texto azul claro y negrita.

## Conmutador de unidad de temperatura

- Haga clic en la etiqueta de temperatura para cambiar entre Celsius y Fahrenheit.
- La unidad elegida se conserva entre sesiones de AetherSDR.
- La etiqueta muestra un decimal independientemente de la unidad.

## Accesibilidad

Todos los indicadores tienen nombres accesibles establecidos como "Potencia directa", "ROE" y "Corriente de drenaje" respectivamente. El botón de velocidad del ventilador establece su nombre accesible de forma dinámica, por ejemplo "Velocidad del ventilador: STANDARD". El botón de alternancia de temperatura tiene una descripción accesible "Alterna la temperatura del amplificador entre Celsius y Fahrenheit" y se puede alcanzar con el foco de la tecla Tab.

## Relacionado

- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Ver la temperatura, la corriente de drenaje y el voltaje de la red eléctrica del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- Cambiar la velocidad del ventilador del PGXL
