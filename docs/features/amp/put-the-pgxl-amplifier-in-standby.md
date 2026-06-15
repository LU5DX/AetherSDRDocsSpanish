# Poner el amplificador PGXL en STANDBY

Use esta página para cambiar un amplificador Power Genius XL conectado de OPERATE a STANDBY, deteniendo así la amplificación de las señales transmitidas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El botón de la bandeja AMP aparece solo después de detectar un Power Genius XL.
- La aplicación Amplifier debe estar abierta. Si no está visible, haga clic en el botón AMP de la bandeja en la barra lateral derecha para mostrarla.
- El botón OPERATE está oculto hasta que llegue el primer mensaje de estado del amplificador. Confirme que esté visible antes de continuar.

## Pasos

1. Abra la aplicación Amplifier haciendo clic en el botón AMP de la bandeja en la barra lateral derecha si aún no está visible.
2. Confirme que el botón OPERATE muestra la etiqueta "OPERATE" en color verde. Esto indica que el amplificador está actualmente en un estado operativo (IDLE, OPERATE o TRANSMIT).
3. Haga clic en OPERATE.

La etiqueta del botón cambia a "STANDBY" y el fondo verde se reemplaza con el estilo oscuro predeterminado, confirmando que el amplificador ha pasado a STANDBY.

## Función de cada control

| Control | Comportamiento | Estados |
|---------|--------------|---------|
| OPERATE | Alterna el amplificador entre OPERATE y STANDBY; emite operateToggled. | Oculto hasta que llegue setState. Muestra 'OPERATE' (verde) para los estados IDLE/OPERATE/TRANSMIT_*, 'STANDBY' en caso contrario. En v0.9.8, se llama a setState desde RadioModel::ampStateChanged (autoritativo), evitando que el botón se quede atascado con la etiqueta anterior (#2437). |
| Fan Speed | Botón de una sola letra (S, C o B) que cambia el modo del ventilador del PGXL entre STANDARD, CONTEST y BROADCAST. | Oculto hasta que una conexión directa con el PGXL entregue el primer estado del modo del ventilador. Tooltip: "Fan Speed\nClick to cycle STANDARD / CONTEST / BROADCAST". El nombre accesible se actualiza con el modo actual, por ejemplo, "Fan speed: STANDARD". |

## Indicadores de telemetría

La aplicación Amplifier muestra los valores de telemetría del amplificador Power Genius XL conectado. Estos indicadores aparecen en la sección inferior de la aplicación.

| Indicador | Formato de visualización | Rango | Comportamiento | Notas |
|-----------|-------------------------|-------|---------------|-------|
| PWR | Valor numérico a la izquierda del medidor Fwd Pwr, por ejemplo "1148" | 0-2000 W | Muestra la potencia directa del PGXL en vatios. La barra del medidor sube rápidamente con las ráfagas de RF pero disminuye en aproximadamente 800 ms, imitando la sensación de retención de pico del S-meter. El medidor se vuelve rojo por encima de 1500 W. El medidor SWR se limpia a 1.0 cuando la potencia directa cae por debajo de 5 W (inactivo). Cuando la potencia directa supera los 5 W, el medidor SWR restaura el valor en caché. | Agregado en v26.6.1. La etiqueta de valor reemplaza la etiqueta anterior "Fwd Pwr". |
| SWR | Valor numérico a la izquierda del medidor SWR | 1.0-3.0 | Muestra la ROE del PGXL. El medidor se vuelve rojo por encima de 2.5. El medidor solo muestra un valor cuando la potencia directa es de 5 W o más — la ROE no es significativa en reposo y la radio/PGXL puede reportar valores obsoletos o de ruido. | Agregado en v26.6.1. La etiqueta de valor reemplaza la etiqueta independiente anterior del medidor. |
| Id | Valor numérico a la izquierda del medidor | 0-70 A | Muestra la corriente de drenaje (Id) del PGXL. El medidor se vuelve rojo por encima de 60 A. | Agregado en v26.6.1. Reemplaza la visualización de texto "Amps" anterior. |
| Temp | Etiqueta de texto, por ejemplo "45 C" | — | Muestra la temperatura del disipador de calor del PGXL en grados Celsius. | Oculto hasta que llegue la primera telemetría. |
| Vdd | Etiqueta de texto, por ejemplo "Vdd 50 V" o "Vdd — V" | — | Muestra el voltaje de drenaje del PGXL. Muestra "Vdd — V" cuando la fuente de drenaje está apagada (voltaje por debajo de 1.0 V) para indicar claramente que la fuente está apagada en lugar de leer cero. | Oculto hasta que llegue la primera telemetría. |
| Vac | Etiqueta de texto, por ejemplo "Vac 120 V" | — | Muestra el voltaje de red del PGXL. | Oculto hasta que llegue la primera telemetría. |
| MEffA | Etiqueta de texto | — | Muestra la métrica de eficiencia del amplificador PGXL (meffa) reenviada desde la telemetría de la radio/proxy. | Oculto hasta que se llame a setMeff. Agregado en v26.5.1. |
| ● RADIO | Indicador de fuente | — | Muestra la fuente de datos de telemetría. Siempre muestra "● RADIO". | Agregado en v26.6.1. |

## Cambios de diseño en v26.6.1

A partir de v26.6.1, la aplicación Amplifier tiene un diseño rediseñado:

- **Fila superior**: Medidor PWR con etiqueta de valor numérico a la izquierda (por ejemplo, "PWR 1148")
- **Segunda fila**: Medidor SWR con etiqueta de valor numérico a la izquierda (por ejemplo, "SWR 1.2")
- **Tercera fila**: Medidor Id (corriente de drenaje) con etiqueta de valor numérico a la izquierda (por ejemplo, "Id 12.5")
- **Fila inferior**: Temperatura (Temp), voltaje de drenaje (Vdd), voltaje de red (Vac) e indicador de fuente apilados a la izquierda, con el botón OPERATE a la derecha

El comportamiento balístico del medidor para PWR utiliza un ataque rápido (30 ms) y una liberación lenta (800 ms) para mantener visibles las transmisiones breves en el medidor.

## Control de velocidad del ventilador

El botón Fan Speed aparece solo cuando una conexión directa con el PGXL entrega el primer estado del modo del ventilador. El botón está oculto hasta entonces.

- Haga clic en el botón para cambiar entre los modos de velocidad del ventilador: STANDARD (S) → CONTEST (C) → BROADCAST (B) → STANDARD.
- El texto del botón muestra una sola letra: S, C o B.
- El nombre accesible se actualiza con el modo actual, por ejemplo, "Fan speed: STANDARD".

## Solución de problemas

- **El botón AMP de la bandeja no está visible** — La aplicación está oculta hasta que la radio detecte un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **El botón OPERATE no está visible** — El botón está oculto hasta que llegue el primer mensaje de estado del amplificador. Espere un momento después de abrir la aplicación; si no aparece, verifique la conexión del amplificador.
- **Hacer clic en OPERATE no tiene efecto** — Confirme que AetherSDR siga conectado a la radio. Desconecte y reconecte si es necesario.
- **Los valores de telemetría muestran guiones** — Espere a que llegue el primer paquete de telemetría del amplificador. Si los valores no aparecen, verifique la conexión del amplificador y el enlace de la radio/proxy.
- **El botón Fan Speed no está visible** — El botón está oculto hasta que una conexión directa con el PGXL entregue el primer estado del modo del ventilador. Espere a que se establezca la conexión; si no aparece, verifique que el PGXL esté conectado directamente (no a través de un proxy).
- **El medidor SWR no muestra ningún valor** — El medidor solo muestra un valor cuando la potencia directa es de 5 W o más. Esto es normal; la ROE no es significativa cuando el amplificador está inactivo.

## Relacionados

- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Ver la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Descripción general del amplificador](overview.md)
