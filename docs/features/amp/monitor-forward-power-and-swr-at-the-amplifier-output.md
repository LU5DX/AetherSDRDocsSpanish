# Supervisar la potencia directa y la ROE en la salida del amplificador

El applet del amplificador muestra lecturas en vivo de la potencia directa y la ROE de un amplificador Power Genius XL (PGXL) conectado. Utilice estos medidores para confirmar la potencia de salida y la adaptación de la antena durante la transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El amplificador Power Genius XL debe ser detectado por la radio. El botón de la bandeja AMP no aparece hasta que el PGXL está presente.

## Pasos

1. Localice el botón de la bandeja AMP en la barra lateral derecha del panel del applet.
2. Haga clic en AMP para abrir el applet del amplificador.
3. Transmita. Observe cómo los medidores Fwd Pwr y SWR se actualizan en tiempo real.

## Qué hace cada control

| Control    | Qué muestra                                | Rango                |
|------------|--------------------------------------------|----------------------|
| PWR        | Potencia directa en la salida del PGXL     | 0–2000 W (rojo > 1500) |
| SWR        | Relación de onda estacionaria en la salida del PGXL | 1.0–3.0 (rojo > 2.5) |
| Id         | Corriente de drenaje                       | 0–70 A (rojo > 60)   |
| Temp       | Temperatura del disipador del PGXL         | 0–100 °C (rojo > 80) |
| Volts / Amps | Voltaje de red y corriente de drenaje en texto | voltios enteros, amperios con 1 decimal |
| MEffA      | Métrica de eficiencia del amplificador PGXL | —                    |
| Fan speed  | Cicla los modos de velocidad del ventilador | STANDARD / CONTEST / BROADCAST |
| OPERATE    | Alterna el amplificador entre OPERATE y STANDBY | —                    |

Los tres indicadores de barra (PWR, SWR, Id) se muestran como indicadores de barra horizontal con una etiqueta en el lado izquierdo que muestra el nombre del campo y el valor en vivo (p. ej., "PWR 1148"). La barra rellena se vuelve roja cuando el valor entra en la zona roja. Las marcas de graduación se dibujan en la parte superior de cada indicador en los siguientes puntos de referencia:

- **PWR:** 0, 500, 1000, 1.5K, 2K
- **SWR:** 1, 1.5, 2, 2.5, 3
- **Id:** 0, 10, 20, 30, 40, 50, 60, 70

El indicador PWR tiene balística de liberación lenta: la barra sube rápidamente en las ráfagas de RF, pero disminuye en aproximadamente 800 ms, por lo que las transmisiones breves permanecen visibles. Esto coincide con la sensación de retención de pico del medidor S.

Ninguno de los medidores tiene una clave de ajustes persistente. Los valores son telemetría de solo lectura del PGXL.

**Comportamiento del indicador SWR:** El indicador SWR solo se actualiza cuando la potencia directa es de al menos 5.0 W. Cuando la potencia directa cae por debajo de 5.0 W, el indicador SWR se reinicia a 1.0. Esto evita que se muestren valores obsoletos o de ruido cuando el amplificador está inactivo.

**Comportamiento de la etiqueta Vdd:** Cuando el voltaje de alimentación de drenaje (Vdd) cae por debajo de 1.0 V (lo que indica que la fuente de drenaje está apagada durante STANDBY), la etiqueta Vdd muestra "Vdd — V" en lugar de "Vdd 0.0 V" para mayor claridad.

**Botón de velocidad del ventilador:** El botón de velocidad del ventilador aparece solo después de que una conexión directa del PGXL entrega el primer estado del modo del ventilador. Haga clic en el botón para ciclar entre STANDARD, CONTEST y BROADCAST. El botón muestra el modo en una etiqueta legible: "Fan: Std", "Fan: Contest" o "Fan: Bcast".

**Alternancia de unidad de temperatura:** La pantalla de temperatura es un botón en el que se puede hacer clic y que alterna entre Celsius y Fahrenheit. El botón muestra la temperatura actual con el símbolo de la unidad (p. ej., "40.5 °C" o "104.9 °F"). Haga clic en el botón para cambiar de unidad. La configuración se mantiene y se recuerda entre reinicios.

## Consejos

- Los indicadores de barra utilizan una animación suavizada. Un breve retraso entre el valor real y la barra mostrada es normal durante condiciones que cambian rápidamente, como el inicio de una transmisión.
- Si la ROE entra en la zona roja (por encima de 2.5), verifique su sistema de antena antes de continuar transmitiendo a alta potencia.
- El indicador de corriente de drenaje (Id) ayuda a supervisar la salud del amplificador. Si Id supera los 60 A, considere reducir la potencia de excitación.
- El campo MEffA muestra la métrica de eficiencia del amplificador PGXL. Este campo está oculto hasta que llega la telemetría.
- La etiqueta de texto Volts / Amps está oculta hasta que llega la primera telemetría.

## Solución de problemas

- **El botón de la bandeja AMP no está visible** — La radio no ha detectado el PGXL. Verifique que el amplificador esté encendido y conectado a la radio Flex. AetherSDR muestra el botón AMP solo después de que la radio informa que hay un amplificador presente.
- **Los medidores PWR y SWR no muestran movimiento durante la transmisión** — Confirme que el amplificador esté en estado OPERATE, no en STANDBY. Consulte [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md).
- **El botón de velocidad del ventilador no aparece** — Se requiere una conexión directa del PGXL. El botón se vuelve visible solo después de que se recibe el primer estado del modo del ventilador desde el amplificador.

## Relacionados

- [Descripción general del amplificador](overview.md)
- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- Supervise la temperatura del PGXL, el voltaje de drenaje y el voltaje de red
