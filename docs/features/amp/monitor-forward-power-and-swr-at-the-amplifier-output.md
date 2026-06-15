# Monitorear la Potencia Directa y la ROE en la Salida del Amplificador

El applet del Amplificador muestra lecturas en vivo de la potencia directa y la ROE de un amplificador Power Genius XL (PGXL) conectado. Utilice estos medidores para confirmar la potencia de salida y la adaptación de la antena durante la transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- Un amplificador Power Genius XL debe ser detectado por la radio. El botón AMP en la bandeja no aparece hasta que el PGXL esté presente.

## Pasos

1. Localice el botón AMP en la bandeja, en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet del Amplificador.
3. Transmita. Observe cómo los medidores Fwd Pwr y SWR se actualizan en tiempo real.

## Qué hace cada control

| Control    | Qué muestra                                      | Rango                |
|------------|--------------------------------------------------|----------------------|
| PWR        | Potencia directa en la salida del PGXL           | 0–2000 W (rojo > 1500) |
| SWR        | Relación de onda estacionaria en la salida del PGXL | 1.0–3.0 (rojo > 2.5)   |
| Id         | Corriente de drenaje                             | 0–70 A (rojo > 60)    |
| Temp       | Temperatura del disipador del PGXL               | 0–100 °C (rojo > 80)  |
| Volts / Amps | Voltaje de red y corriente de drenaje en texto | voltios enteros, 1 decimal para amperios |
| MEffA      | Métrica de eficiencia del amplificador PGXL      | —                    |
| Fan speed  | Cicla los modos de velocidad del ventilador      | STANDARD / CONTEST / BROADCAST |
| OPERATE    | Conmuta el amplificador entre OPERATE y STANDBY  | —                    |

Los tres medidores de barra (PWR, SWR, Id) se muestran como indicadores de barra horizontales con una etiqueta en el lado izquierdo que muestra el nombre del campo y el valor en vivo (por ejemplo, "PWR 1148"). La barra llena se vuelve roja cuando el valor entra en la zona roja. Las marcas de referencia se dibujan a lo largo de la parte superior de cada indicador en los siguientes puntos:

- **PWR:** 0, 500, 1000, 1.5K, 2K
- **SWR:** 1, 1.5, 2, 2.5, 3
- **Id:** 0, 10, 20, 30, 40, 50, 60, 70

El indicador PWR tiene balística de liberación lenta: la barra sube rápidamente en ráfagas de RF pero decae en aproximadamente 800 ms, por lo que las transmisiones breves siguen siendo visibles. Esto coincide con la sensación de retención de pico del S-meter.

Ninguno de los medidores tiene una clave de ajustes persistente. Los valores son telemetría de solo lectura del PGXL.

**Comportamiento del indicador SWR:** El indicador SWR solo se actualiza cuando la potencia directa es de al menos 5.0 W. Cuando la potencia directa cae por debajo de 5.0 W, el indicador SWR se restablece a 1.0. Esto evita que se muestren valores obsoletos o de ruido cuando el amplificador está inactivo.

**Comportamiento de la etiqueta Vdd:** Cuando el voltaje de la fuente de drenaje (Vdd) cae por debajo de 1.0 V (lo que indica que la fuente de drenaje está apagada durante STANDBY), la etiqueta Vdd muestra "Vdd — V" en lugar de "Vdd 0.0 V" para mayor claridad.

**Botón de velocidad del ventilador:** El botón de velocidad del ventilador aparece solo después de que una conexión directa al PGXL entrega el primer estado del modo del ventilador. Haga clic en el botón para ciclar a través de STANDARD, CONTEST y BROADCAST. El botón muestra una sola letra: S (STANDARD), C (CONTEST) o B (BROADCAST).

## Consejos

- Los indicadores de barra utilizan animación suavizada. Un breve retardo entre el valor real y la barra mostrada es normal durante condiciones que cambian rápidamente, como el inicio de una transmisión.
- Si la ROE entra en la zona roja (por encima de 2.5), verifique su sistema de antena antes de continuar transmitiendo a alta potencia.
- El indicador de corriente de drenaje (Id) ayuda a monitorear la salud del amplificador. Si Id supera los 60 A, considere reducir la potencia de excitación.
- El campo MEffA muestra la métrica de eficiencia del amplificador PGXL. Este campo está oculto hasta que llegue la telemetría.
- La etiqueta de texto Volts / Amps está oculta hasta que llegue la primera telemetría.

## Solución de problemas

- **El botón AMP en la bandeja no es visible** — El PGXL no ha sido detectado por la radio. Verifique que el amplificador esté encendido y conectado a la radio Flex. AetherSDR muestra el botón AMP solo después de que la radio informa que hay un amplificador presente.
- **Los medidores PWR y SWR no muestran movimiento durante la transmisión** — Confirme que el amplificador esté en estado OPERATE, no en STANDBY. Consulte [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md).
- **El botón de velocidad del ventilador no aparece** — Se requiere una conexión directa al PGXL. El botón se vuelve visible solo después de que se recibe el primer estado del modo del ventilador desde el amplificador.

## Relacionado

- [Descripción general del amplificador](overview.md)
- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Observar la temperatura, el voltaje de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-voltage-and-mains-voltage.md)
