# Poner el amplificador PGXL en STANDBY

Use esta página para cambiar un amplificador Power Genius XL conectado del modo OPERATE a STANDBY, deteniendo su amplificación de las señales transmitidas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El botón de la bandeja AMP solo aparece después de detectar un Power Genius XL.
- El applet del amplificador debe estar abierto. Si no está visible, haga clic en el botón AMP en la barra lateral derecha para mostrarlo.
- El botón OPERATE está oculto hasta que llegue el primer mensaje de estado desde el amplificador. Confirme que es visible antes de continuar.

## Pasos

1. Abra el applet del amplificador haciendo clic en el botón AMP en la barra lateral derecha si aún no está visible.
2. Confirme que el botón OPERATE muestra la etiqueta "OPERATE" en verde. Esto indica que el amplificador está actualmente en un estado operativo (IDLE, OPERATE o TRANSMIT).
3. Haga clic en OPERATE.

La etiqueta del botón cambia a "STANDBY" y el fondo verde se reemplaza con el estilo oscuro predeterminado, confirmando que el amplificador ha pasado a STANDBY.

## Qué hace cada control

| Control | Comportamiento | Estados |
|---------|---------------|---------|
| OPERATE | Alterna el amplificador entre OPERATE y STANDBY; emite operateToggled. | Oculto hasta que llegue setState. Muestra 'OPERATE' (verde) para estados IDLE/OPERATE/TRANSMIT_*, y 'STANDBY' en caso contrario. En v0.9.8, se llama a setState desde RadioModel::ampStateChanged (autoritativo), evitando que el botón se quede atascado con la etiqueta anterior (#2437). |

## Indicadores de telemetría

El applet del amplificador muestra valores de telemetría del amplificador Power Genius XL conectado. Estos indicadores aparecen en la sección inferior del applet.

| Indicador | Formato de visualización | Rango | Comportamiento | Notas |
|-----------|--------------------------|-------|---------------|-------|
| PWR | Valor numérico a la izquierda del medidor Fwd Pwr, ej. "1148" | 0-2000 W | Muestra la potencia directa del PGXL en vatios. La barra del medidor sube rápidamente con ráfagas de RF pero decae en aproximadamente 800 ms, similar a la retención de pico del medidor S. El medidor se vuelve rojo por encima de 1500 W. | Añadido en v26.6.1. La etiqueta de valor reemplaza la etiqueta anterior "Fwd Pwr". |
| SWR | Valor numérico a la izquierda del medidor SWR | 1.0-3.0 | Muestra la ROE del PGXL. El medidor se vuelve rojo por encima de 2.5. | Añadido en v26.6.1. La etiqueta de valor reemplaza la etiqueta independiente anterior del medidor. |
| Id | Valor numérico a la izquierda del medidor | 0-70 A | Muestra la corriente de drenaje (Id) del PGXL. El medidor se vuelve rojo por encima de 60 A. | Añadido en v26.6.1. Reemplaza la visualización de texto "Amps" anterior. |
| Temp | Etiqueta de texto, ej. "45 C" | — | Muestra la temperatura del disipador del PGXL en grados Celsius. | Oculto hasta que llegue la primera telemetría. |
| Vdd | Etiqueta de texto, ej. "Vdd 50 V" | — | Muestra el voltaje de drenaje del PGXL. | Oculto hasta que llegue la primera telemetría. |
| Vac | Etiqueta de texto, ej. "Vac 120 V" | — | Muestra el voltaje de red del PGXL. | Oculto hasta que llegue la primera telemetría. |
| MEffA | Etiqueta de texto | — | Muestra la métrica de eficiencia del amplificador PGXL (meffa) reenviada desde la telemetría de la radio/proxy. | Oculto hasta que se llame a setMeff. Añadido en v26.5.1. |
| ● RADIO | Indicador de fuente | — | Muestra la fuente de datos de telemetría. Siempre muestra "● RADIO". | Añadido en v26.6.1. |

## Cambios de diseño en v26.6.1

A partir de v26.6.1, el applet del amplificador tiene un diseño rediseñado:

- **Fila superior**: Medidor PWR con etiqueta de valor numérico a la izquierda (ej., "PWR 1148")
- **Segunda fila**: Medidor SWR con etiqueta de valor numérico a la izquierda (ej., "SWR 1.2")
- **Tercera fila**: Medidor Id (corriente de drenaje) con etiqueta de valor numérico a la izquierda (ej., "Id 12.5")
- **Fila inferior**: Temperatura (Temp), voltaje de drenaje (Vdd), voltaje de red (Vac) e indicador de fuente apilados a la izquierda, con el botón OPERATE a la derecha

La respuesta balística del medidor PWR utiliza un ataque rápido (30 ms) y una liberación lenta (800 ms) para mantener visibles las transmisiones breves en el medidor.

## Solución de problemas

- **El botón AMP no está visible** — El applet se oculta hasta que la radio detecta un Power Genius XL. Confirme que el PGXL está encendido y conectado a la radio Flex.
- **El botón OPERATE no está visible** — El botón se oculta hasta que llegue el primer mensaje de estado desde el amplificador. Espere un momento después de abrir el applet; si no aparece, verifique la conexión del amplificador.
- **Hacer clic en OPERATE no tiene efecto** — Confirme que AetherSDR aún está conectado a la radio. Desconecte y reconecte si es necesario.
- **Los valores de telemetría muestran guiones** — Espere a que llegue el primer paquete de telemetría desde el amplificador. Si los valores no aparecen, verifique la conexión del amplificador y el enlace de radio/proxy.

## Relacionado

- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Monitorear la potencia directa y la ROE a la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Ver la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Descripción general del amplificador](overview.md)
