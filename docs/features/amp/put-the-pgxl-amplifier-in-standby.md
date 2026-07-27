# Poner el amplificador PGXL en STANDBY

Use esta página para cambiar un amplificador Power Genius XL conectado del modo OPERATE a STANDBY, deteniendo así la amplificación de las señales transmitidas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El botón de la bandeja AMP solo aparece después de detectar un Power Genius XL.
- La applet del amplificador debe estar abierta. Si no está visible, haga clic en el botón AMP en la barra lateral derecha para mostrarla.
- El botón OPERATE está oculto hasta que llegue el primer mensaje de estado del amplificador. Confirme que esté visible antes de continuar.

## Pasos

1. Abra la applet del amplificador haciendo clic en el botón AMP en la barra lateral derecha si aún no está visible.
2. Confirme que el botón OPERATE muestre la etiqueta "OPERATE" en verde. Esto indica que el amplificador se encuentra actualmente en un estado operativo (IDLE, OPERATE o TRANSMIT).
3. Haga clic en OPERATE.

La etiqueta del botón cambia a "STANDBY" y el fondo verde se reemplaza por el estilo oscuro predeterminado, lo que confirma que el amplificador ha pasado al modo STANDBY.

## Qué hace cada control

| Control | Comportamiento | Estados |
|---------|---------------|--------|
| OPERATE | Alterna el amplificador entre OPERATE y STANDBY; emite operateToggled. | Oculto hasta que llegue setState. Muestra 'OPERATE' (verde) para los estados IDLE/OPERATE/TRANSMIT_*, 'STANDBY' en caso contrario. En v0.9.8, setState se llama desde RadioModel::ampStateChanged (con autoridad), evitando que el botón se quede atascado con la etiqueta anterior (#2437). |
| Fan Speed | Botón etiquetado con el modo de ventilador actual ("Fan: Std", "Fan: Contest" o "Fan: Bcast") que cicla el modo del ventilador del PGXL entre STANDARD, CONTEST y BROADCAST. | Oculto hasta que una conexión directa al PGXL entregue el primer estado del modo de ventilador. Tooltip: "Fan Speed\nClick to cycle STANDARD / CONTEST / BROADCAST". El nombre accesible se actualiza con el modo actual, p. ej., "Fan speed: STANDARD". |
| Conmutador de unidad de temperatura | Haga clic en la pantalla de temperatura para alternar entre Celsius (°C) y Fahrenheit (°F). El ajuste persiste al reiniciar la aplicación. | Muestra la temperatura actual con un decimal. Oculto hasta que llegue la primera telemetría. |

## Indicadores de telemetría

La applet del amplificador muestra los valores de telemetría del amplificador Power Genius XL conectado. Estos indicadores aparecen en la sección inferior de la applet.

| Indicador | Formato de visualización | Rango | Comportamiento | Notas |
|-----------|-------------------------|-------|---------------|-------|
| PWR | Valor numérico a la izquierda del indicador Fwd Pwr, p. ej., "1148" | 0-2000 W | Muestra la potencia directa del PGXL en vatios. La barra del indicador sube rápidamente en ráfagas de RF pero decae en aproximadamente 800 ms, imitando la sensación de retención de pico del S-meter. El indicador se vuelve rojo por encima de 1500 W. El indicador de ROE se limpia a 1.0 cuando la potencia directa cae por debajo de 5 W (inactivo). Cuando la potencia directa se reanuda por encima de 5 W, el indicador de ROE restaura el valor en caché. | Añadido en v26.6.1. La etiqueta de valor reemplaza la etiqueta anterior "Fwd Pwr". |
| SWR | Valor numérico a la izquierda del indicador SWR | 1.0-3.0 | Muestra la ROE del PGXL. El indicador se vuelve rojo por encima de 2.5. El indicador solo muestra un valor cuando la potencia directa es de 5 W o más; la ROE no es significativa en reposo y la radio/PGXL puede reportar valores obsoletos o ruidosos. | Añadido en v26.6.1. La etiqueta de valor reemplaza la etiqueta independiente anterior del indicador. |
| Id | Valor numérico a la izquierda del indicador | 0-70 A | Muestra la corriente de drenaje (Id) del PGXL. El indicador se vuelve rojo por encima de 60 A. | Añadido en v26.6.1. Reemplaza la visualización de texto "Amps" anterior. |
| Temp | Etiqueta de texto en la que se puede hacer clic, p. ej., "45.0 °C" o "113.0 °F" | — | Muestra la temperatura del disipador del PGXL. Haga clic para alternar entre Celsius y Fahrenheit. El ajuste persiste al reiniciar la aplicación. | Oculto hasta que llegue la primera telemetría. |
| Vdd | Etiqueta de texto, p. ej., "Vdd 50 V" o "Vdd — V" | — | Muestra el voltaje de drenaje del PGXL. Muestra "Vdd — V" cuando la fuente de drenaje está apagada (voltaje por debajo de 1.0 V) para indicar claramente que la fuente está apagada en lugar de leer cero. | Oculto hasta que llegue la primera telemetría. |
| Vac | Etiqueta de texto, p. ej., "Vac 120 V" | — | Muestra el voltaje de red del PGXL. | Oculto hasta que llegue la primera telemetría. |
| MEffA | Etiqueta de texto | — | Muestra la métrica de eficiencia del amplificador PGXL (meffa) reenviada desde la telemetría de la radio/proxy. | Oculto hasta que se llame a setMeff. Añadido en v26.5.1. |
| ● RADIO | Indicador de fuente | — | Muestra la fuente de datos de telemetría. Siempre muestra "● RADIO". | Añadido en v26.6.1. |

## Cambios de diseño en v26.6.1

A partir de v26.6.1, la applet del amplificador tiene un diseño rediseñado:

- **Fila superior**: Indicador PWR con etiqueta de valor numérico a la izquierda (p. ej., "PWR 1148")
- **Segunda fila**: Indicador SWR con etiqueta de valor numérico a la izquierda (p. ej., "SWR 1.2")
- **Tercera fila**: Indicador Id (corriente de drenaje) con etiqueta de valor numérico a la izquierda (p. ej., "Id 12.5")
- **Fila inferior**: Temperatura (Temp, en la que se puede hacer clic), voltaje de drenaje (Vdd), voltaje de red (Vac) e indicador de fuente apilados a la izquierda, con el botón OPERATE a la derecha

La balística de los indicadores para PWR utiliza un ataque rápido (30 ms) y una liberación lenta (800 ms) para mantener visibles las transmisiones breves en el medidor.

## Control de velocidad del ventilador

El botón Fan Speed aparece solo cuando una conexión directa al PGXL entrega el primer estado del modo de ventilador. El botón está oculto hasta entonces.

- Haga clic en el botón para ciclar los modos de velocidad del ventilador: STANDARD → CONTEST → BROADCAST → STANDARD.
- El texto del botón muestra la etiqueta del modo: "Fan: Std", "Fan: Contest" o "Fan: Bcast".
- El nombre accesible se actualiza con el modo actual, p. ej., "Fan speed: STANDARD".

## Conmutador de unidad de temperatura

La pantalla de temperatura también funciona como control. Haga clic en ella para alternar entre Celsius y Fahrenheit.

- La temperatura se muestra con un decimal (p. ej., "45.0 °C" o "113.0 °F").
- El ajuste persiste al reiniciar la aplicación.
- El botón tiene un indicador de enfoque visible y un efecto de desplazamiento.

## Solución de problemas

- **El botón AMP no está visible** — La applet está oculta hasta que la radio detecte un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **El botón OPERATE no está visible** — El botón está oculto hasta que llegue el primer mensaje de estado del amplificador. Espere un momento después de abrir la applet; si no aparece, verifique la conexión del amplificador.
- **Al hacer clic en OPERATE no sucede nada** — Confirme que AetherSDR todavía esté conectado a la radio. Desconéctelo y reconéctelo si es necesario.
- **Los valores de telemetría muestran guiones** — Espere a que llegue el primer paquete de telemetría del amplificador. Si los valores no aparecen, verifique la conexión del amplificador y el enlace de radio/proxy.
- **El botón Fan Speed no está visible** — El botón está oculto hasta que una conexión directa al PGXL entregue el primer estado del modo de ventilador. Espere a que se establezca la conexión; si no aparece, verifique que el PGXL esté conectado directamente (no a través de un proxy).
- **El indicador SWR no muestra ningún valor** — El indicador solo muestra un valor cuando la potencia directa es de 5 W o más. Esto es normal; la ROE no es significativa cuando el amplificador está inactivo.

## Relacionados

- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Monitorizar la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Observar la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Descripción general del amplificador](overview.md)
