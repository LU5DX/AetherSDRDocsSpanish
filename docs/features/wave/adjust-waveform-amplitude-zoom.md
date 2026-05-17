# Ajustar el zoom de amplitud y la ventana de tiempo de la forma de onda

El control deslizante Zoom en el applet Waveform ajusta la escala del eje de amplitud de la visualización de la forma de onda. Aumentar el zoom estira verticalmente las señales pequeñas para que sean más fáciles de leer; disminuirlo evita que los artefactos de recorte oculten la traza en señales fuertes. El control deslizante Window controla la ventana de tiempo mostrada en la visualización de la forma de onda.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo se ve la traza de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. Localice la fila Zoom o la fila Window en el cajón de configuración.
3. Ajuste el control deslizante deseado:
   - Arrastre el control deslizante **Zoom** hacia la izquierda para disminuir el zoom o hacia la derecha para aumentarlo. La lectura a la derecha del control deslizante se actualiza inmediatamente, mostrando el valor actual como un multiplicador (por ejemplo, `1.7x`).
   - Arrastre el control deslizante **Window** hacia la izquierda para disminuir la ventana de tiempo o hacia la derecha para aumentarla. La lectura a la derecha del control deslizante se actualiza inmediatamente, mostrando el valor actual en milisegundos o segundos (por ejemplo, `1 s` o `240 ms`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente en `WaveApplet_ZoomPercent` o `WaveApplet_TimeWindowMs`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Zoom | 170 (1.7x) | 100–600 (mostrado como 1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` |

El valor del control deslizante Zoom es un porcentaje entero. La visualización de la forma de onda lo divide por 100 para producir el multiplicador que se muestra en la lectura. Un valor de 100 significa sin zoom (1.0x); 600 es el zoom máximo (6.0x).

El control deslizante Window selecciona entre pasos discretos de ventana de tiempo. Las primeras dos marcas proporcionan detalle de subsegundos (240 ms y 480 ms), seguidas de incrementos de un segundo desde 1 segundo hasta 10 segundos. Cada marca es una parada deliberada, no un rango continuo.

## Consejos

- Con niveles de zoom altos, las señales cercanas a la escala completa producirán resaltes de recorte (énfasis en columnas rojas y un contador CLIP N en el encabezado). Si ve indicadores de recorte frecuentes después de aumentar el zoom, reduzca el valor hasta que la traza quepa dentro de la visualización sin tocar los bordes.
- Los ajustes de zoom y ventana se aplican por igual a las rutas de RX y TX. El tinte de dirección (frío para RX, cálido para TX) aún distingue qué ruta está activa independientemente del nivel de zoom.
- Para inspeccionar un transitorio con mayor zoom sin perderlo en tiempo real, primero pause la visualización haciendo un solo clic en la forma de onda, luego ajuste el zoom mientras la instantánea está congelada.
- Use una ventana más corta (240 ms o 480 ms) para ver detalles finos en formas de onda rápidas. Use una ventana más larga (5 s a 10 s) para ver cambios generales de nivel a lo largo del tiempo.

## Solución de problemas

- **El cajón de configuración no es visible** — Haga doble clic en la visualización de la forma de onda para abrirlo. El cajón está debajo de la traza de la forma de onda.
- **El control deslizante Zoom vuelve a su posición después de arrastrarlo** — Esto puede ocurrir si no llega audio y la visualización muestra el marcador de posición sin audio. El valor del control deslizante aún se guarda; surte efecto tan pronto como se reanude el audio.
- **El zoom se reinicia después de reiniciar AetherSDR** — Verifique que el valor se esté persistiendo. Si la aplicación se cerró de forma anómala, es posible que el ajuste `WaveApplet_ZoomPercent` no se haya escrito. Ajuste el control deslizante al valor deseado después de un inicio limpio.
- **El ajuste de ventana cambió inesperadamente después de una actualización** — Si actualiza desde una versión anterior que usaba el ajuste `WaveApplet_TimeWindowSec` (1–20 s lineal), el valor se migra automáticamente al paso discreto más cercano en `WaveApplet_TimeWindowMs`. Verifique el ajuste y ajústelo si es necesario.
- **El mensaje de marcador de posición sin audio cambió** — Cuando no llega audio de RX, la visualización ahora muestra "Enable PC Audio" en lugar de "no RX audio". Esto indica que debe habilitar el audio de PC en la configuración de radio o en la configuración de audio. Para TX, el mensaje aún muestra "no TX audio".

## Relacionado

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
