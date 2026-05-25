# Ajustar el zoom de amplitud y la ventana de tiempo de la forma de onda

El control deslizante Zoom en el applet Waveform escala el eje de amplitud de la visualización de la forma de onda. Al aumentar el zoom, las señales pequeñas se estiran verticalmente para que sean más fáciles de leer; al disminuirlo, se evita que los artefactos de recorte oculten la traza en señales fuertes. El control deslizante Window controla la ventana de tiempo que se muestra en la visualización de la forma de onda.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo se ve la traza de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón. El estado del cajón se conserva entre sesiones.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. Localice la fila Zoom o la fila Window en el cajón de configuración.
3. Ajuste el control deslizante deseado:
   - Arrastre el control deslizante **Zoom** hacia la izquierda para disminuir el zoom o hacia la derecha para aumentarlo. La lectura a la derecha del control deslizante se actualiza inmediatamente, mostrando el valor actual como un multiplicador (por ejemplo, `1.7x`).
   - Arrastre el control deslizante **Window** hacia la izquierda para disminuir la ventana de tiempo o hacia la derecha para aumentarla. La lectura a la derecha del control deslizante se actualiza inmediatamente, mostrando el valor actual en milisegundos o segundos (por ejemplo, `1 s` o `240 ms`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente en `WaveApplet_ZoomPercent` o `WaveApplet_TimeWindowMs`. El estado expandido/contraído del cajón también se guarda automáticamente en `WaveApplet_DrawerExpanded`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Zoom | 170 (1.7x) | 100–600 (mostrado como 1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` |

El valor del control deslizante Zoom es un porcentaje entero. La visualización de la forma de onda lo divide por 100 para producir el multiplicador que se muestra en la lectura. Un valor de 100 significa sin zoom (1.0x); 600 es el zoom máximo (6.0x).

El control deslizante Window selecciona entre pasos discretos de ventana de tiempo. Las dos primeras marcas proporcionan detalles de subsegundo (240 ms y 480 ms), seguidas de incrementos de un segundo desde 1 segundo hasta 10 segundos. Cada marca es una parada deliberada, no un rango continuo.

## El estado del cajón de configuración

El cajón de configuración (que contiene los controles View, Zoom, Window y FPS) recuerda si estaba abierto o cerrado la última vez que usó el applet. Cuando vuelva a abrir el applet Waveform, el cajón se restaurará a su estado anterior. Si siempre desea que el cajón esté abierto, déjelo abierto antes de cerrar el applet o reiniciar AetherSDR.

## Consejos

- Con niveles de zoom altos, las señales cercanas al nivel completo producirán indicadores de recorte (resalte de columna roja y un contador CLIP N en el encabezado). Si ve indicadores de recorte frecuentes después de aumentar el zoom, reduzca el valor hasta que la traza quepa dentro de la pantalla sin tocar los bordes.
- La configuración de zoom y ventana se aplica por igual a las rutas de RX y TX. El matiz de dirección (frío para RX, cálido para TX) aún distingue qué ruta está activa independientemente del nivel de zoom.
- Para inspeccionar un transitorio con mayor zoom sin perderlo en tiempo real, primero pause la pantalla haciendo clic una vez en la forma de onda y luego ajuste el zoom mientras la instantánea está congelada.
- Use una ventana más corta (240 ms o 480 ms) para ver detalles finos en formas de onda rápidas. Use una ventana más larga (5 s a 10 s) para ver cambios generales de nivel a lo largo del tiempo.
- El intervalo de discriminación de clics utilizado para distinguir un clic simple de un doble clic respeta el valor que estableció en Radio Setup → Interaction Settings. Los cambios en esa configuración surten efecto de inmediato sin reiniciar AetherSDR.

## Solución de problemas

- **El cajón de configuración no es visible** — Haga doble clic en la visualización de la forma de onda para alternar su apertura. El cajón está debajo de la traza de la forma de onda.
- **El control deslizante Zoom retrocede después de arrastrarlo** — Esto puede suceder si no llega audio y la pantalla muestra el marcador de posición de falta de audio. El valor del control deslizante aún se guarda; surte efecto tan pronto como se reanude el audio.
- **El zoom se restablece después de reiniciar AetherSDR** — Verifique que el valor se esté guardando. Si la aplicación se cerró de forma anormal, es posible que la configuración `WaveApplet_ZoomPercent` no se haya escrito. Establezca el control deslizante en el valor deseado después de un inicio limpio.
- **La configuración de ventana cambió inesperadamente después de una actualización** — Si actualiza desde una versión anterior que usaba la configuración `WaveApplet_TimeWindowSec` (1–20 s lineal), el valor se migra automáticamente al paso discreto más cercano en `WaveApplet_TimeWindowMs`. Verifique la configuración y ajústela si es necesario.
- **El mensaje del marcador de posición de falta de audio cambió** — Cuando no llega audio de RX, la pantalla ahora muestra "Enable PC Audio" en lugar de "no RX audio". Esto indica que debe habilitar el audio de PC en la configuración de radio o en la configuración de audio. Para TX, el mensaje sigue mostrando "no TX audio".

## Relacionados

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
