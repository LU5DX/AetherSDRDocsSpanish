# Ajustar el zoom de amplitud y la ventana de tiempo en la forma de onda

El control deslizante de Zoom en el applet de forma de onda escala el eje de amplitud de la visualización. Aumentar el zoom estira verticalmente las señales débiles para facilitar su lectura; disminuirlo evita que los artefactos de recorte oculten la traza en señales fuertes. El control deslizante de Ventana controla la ventana de tiempo mostrada en la visualización de la forma de onda.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo se ve la traza de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón. El estado del cajón se conserva entre sesiones.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. Localice la fila Zoom o la fila Ventana en el cajón de configuración.
3. Ajuste el control deslizante deseado:
   - Arrastre el control deslizante de **Zoom** hacia la izquierda para disminuir el zoom o hacia la derecha para aumentarlo. El indicador a la derecha del control se actualiza inmediatamente, mostrando el valor actual como un multiplicador (por ejemplo, `1.7x`).
   - Arrastre el control deslizante de **Ventana** hacia la izquierda para disminuir la ventana de tiempo o hacia la derecha para aumentarla. El indicador a la derecha del control se actualiza inmediatamente, mostrando el valor actual en milisegundos o segundos (por ejemplo, `1 s` o `240 ms`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente en `WaveApplet_ZoomPercent` o `WaveApplet_TimeWindowMs`. El estado expandido/contraído del cajón también se guarda automáticamente en `WaveApplet_DrawerExpanded`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Zoom | 170 (1.7x) | 100–600 (mostrado como 1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| Ventana | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` |

El valor del control deslizante de Zoom es un porcentaje entero. La visualización de la forma de onda lo divide entre 100 para producir el multiplicador mostrado en el indicador. Un valor de 100 significa sin zoom (1.0x); 600 es el zoom máximo (6.0x).

El control deslizante de Ventana selecciona entre pasos discretos de ventana de tiempo. Las dos primeras marcas proporcionan detalle de subsegundo (240 ms y 480 ms), seguidas de incrementos de un segundo desde 1 segundo hasta 10 segundos. Cada marca es una parada deliberada, no un rango continuo.

## El estado del cajón de configuración

El cajón de configuración (que contiene los controles Vista, Zoom, Ventana y FPS) recuerda si estaba abierto o cerrado la última vez que usó el applet. Cuando vuelva a abrir el applet de forma de onda, el cajón se restaurará a su estado anterior. Si siempre quiere el cajón abierto, déjelo abierto antes de cerrar el applet o reiniciar AetherSDR.

## Consejos

- Con niveles altos de zoom, las señales cercanas a la escala completa producirán indicaciones de recorte (énfasis de columna roja y un contador CLIP N en el encabezado). Si ve indicadores de recorte frecuentes después de aumentar el zoom, reduzca el valor hasta que la traza quepa dentro de la pantalla sin tocar los bordes.
- Los ajustes de zoom y ventana se aplican por igual a las rutas de RX y TX. El matiz de dirección (frío para RX, cálido para TX) aún distingue qué ruta está activa independientemente del nivel de zoom.
- Para inspeccionar un transitorio con mayor zoom sin perderlo en tiempo real, primero pause la pantalla haciendo un solo clic en la forma de onda, luego ajuste el zoom mientras la instantánea está congelada.
- Use una ventana más corta (240 ms o 480 ms) para ver detalles finos en formas de onda rápidas. Use una ventana más larga (5 s a 10 s) para ver cambios generales de nivel a lo largo del tiempo.
- El intervalo de discriminación de clic utilizado para distinguir un solo clic de un doble clic respeta el valor que estableció en Configuración de Radio → Ajustes de Interacción. Los cambios en esa configuración surten efecto inmediatamente sin reiniciar AetherSDR.

## Solución de problemas

- **El cajón de configuración no es visible** — Haga doble clic en la visualización de la forma de onda para abrirlo. El cajón está debajo de la traza de la forma de onda.
- **El control deslizante de Zoom vuelve a su posición después de arrastrarlo** — Esto puede ocurrir si no llega audio y la pantalla muestra el marcador de posición sin audio. El valor del control deslizante aún se guarda; surte efecto tan pronto como se reanude el audio.
- **El zoom se restablece después de reiniciar AetherSDR** — Verifique que el valor se esté guardando. Si la aplicación se cerró de forma anormal, es posible que la configuración `WaveApplet_ZoomPercent` no se haya escrito. Establezca el control deslizante al valor deseado después de un inicio limpio.
- **La configuración de Ventana cambió inesperadamente después de una actualización** — Si actualiza desde una versión anterior que usaba la configuración `WaveApplet_TimeWindowSec` (1–20 s lineal), el valor se migra automáticamente al paso discreto más cercano en `WaveApplet_TimeWindowMs`. Verifique la configuración y ajústela si es necesario.
- **El mensaje del marcador de posición sin audio cambió** — Cuando no llega audio de RX, la pantalla ahora muestra "Enable PC Audio" en lugar de "no RX audio". Esto indica que debe habilitar el audio de PC en la configuración de radio o en la configuración de audio. Para TX, el mensaje aún muestra "no TX audio".

## Relacionados

- [Visión general de la forma de onda](overview.md)
- [Monitorizar audio de TX o RX en la visualización de la forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Establecer la tasa de actualización de la forma de onda para reducir la carga de la CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
