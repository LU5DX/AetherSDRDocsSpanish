# Ajustar el zoom de la amplitud de la forma de onda y la ventana de tiempo

El control deslizante Zoom del applet Waveform escala el eje de amplitud de la visualización de la forma de onda. Aumentar el zoom estira verticalmente las señales pequeñas para que sean más fáciles de leer; disminuirlo evita que los artefactos de recorte oculten la traza en señales fuertes. El control deslizante Window controla la ventana de tiempo que se muestra en la visualización de la forma de onda.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo se ve la traza de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón. El estado del cajón se conserva entre sesiones.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. Localice la fila Zoom o la fila Window en el cajón de configuración.
3. Ajuste el control deslizante deseado:
   - Arrastre el control deslizante **Zoom** hacia la izquierda para disminuir el zoom o hacia la derecha para aumentarlo. El indicador a la derecha del control deslizante se actualiza inmediatamente, mostrando el valor actual como un multiplicador (por ejemplo, `1.7x`).
   - Arrastre el control deslizante **Window** hacia la izquierda para disminuir la ventana de tiempo o hacia la derecha para aumentarla. El indicador a la derecha del control deslizante se actualiza inmediatamente, mostrando el valor actual en milisegundos o segundos (por ejemplo, `1 s` o `240 ms`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente en `WaveApplet_ZoomPercent` o `WaveApplet_TimeWindowMs`. El estado expandido/contraído del cajón también se guarda automáticamente en `WaveApplet_DrawerExpanded`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Zoom | 170 (1.7x) | 100–600 (se muestra como 1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` |

El valor del control deslizante Zoom es un porcentaje entero. La visualización de la forma de onda lo divide por 100 para producir el multiplicador que se muestra en el indicador. Un valor de 100 significa sin zoom (1.0x); 600 es el zoom máximo (6.0x).

El control deslizante Window selecciona entre pasos discretos de ventana de tiempo. Las dos primeras muescas proporcionan detalle de subsegundo (240 ms y 480 ms), seguidas de incrementos de un segundo desde 1 segundo hasta 10 segundos. Cada muesca es una parada deliberada, no un rango continuo.

## El estado del cajón de configuración

El cajón de configuración (que contiene los controles View, Zoom, Window y FPS) recuerda si estaba abierto o cerrado la última vez que usó el applet. Cuando vuelva a abrir el applet Waveform, el cajón se restaurará a su estado anterior. Si siempre quiere el cajón abierto, déjelo abierto antes de cerrar el applet o reiniciar AetherSDR.

## Modo Lean

Cuando el modo Lean está activo, el applet Waveform se oculta de la vista y todos los datos de alcance de audio se descartan silenciosamente sin ningún procesamiento. Esto reduce el uso de la CPU al evitar la representación de la forma de onda en tiempo real que normalmente se ejecuta a la velocidad de FPS configurada.

Para alternar el modo Lean para el applet Waveform:

1. Abra el panel de apariencia o de gestión de applets (disponible desde el menú contextual o la barra de herramientas).
2. Localice la entrada del applet Waveform.
3. Haga clic en la alternancia de visibilidad para habilitar o deshabilitar el modo Lean.

Cuando el modo Lean está desactivado, el applet es visible y procesa el audio normalmente. Cuando el modo Lean está activado, el applet está oculto y se llama al método `setActive(false)`, que:
- Oculta el widget del applet de la interfaz de usuario.
- Descarta todos los datos de muestra de alcance entrantes sin agregarlos al búfer.
- Detiene el ciclo de repintado de software de 24 Hz.

Las señales upstream `AudioEngine::{tx,rx}PostChainScopeReady` aún se activan en cada callback de audio, pero el procesamiento de alcance se omite por completo.

## Consejos

- En niveles de zoom altos, las señales cercanas a la escala completa producirán indicaciones de recorte (énfasis en columnas rojas y un contador CLIP N en el encabezado). Si ve indicadores de recorte frecuentes después de aumentar el zoom, reduzca el valor hasta que la traza quepa dentro de la pantalla sin tocar los bordes.
- Los ajustes de zoom y ventana se aplican por igual a las rutas RX y TX. El tinte de dirección (frío para RX, cálido para TX) aún distingue qué ruta está activa independientemente del nivel de zoom.
- Para inspeccionar un transitorio con mayor zoom sin perderlo en tiempo real, primero pause la pantalla haciendo clic una vez en la forma de onda, luego ajuste el zoom mientras la captura está congelada.
- Use una ventana más corta (240 ms o 480 ms) para ver detalles finos en formas de onda rápidas. Use una ventana más larga (5 s a 10 s) para ver cambios de nivel general a lo largo del tiempo.
- El intervalo de discriminación de clics utilizado para distinguir un clic simple de un doble clic respeta el valor que estableció en Radio Setup → Interaction Settings. Los cambios en esa configuración surten efecto de inmediato sin reiniciar AetherSDR.
- En el modo Lean, el applet Waveform no utiliza recursos de CPU para la representación, lo que lo hace ideal para operadores que rara vez necesitan el alcance pero quieren tenerlo disponible bajo demanda.

## Solución de problemas

- **El cajón de configuración no es visible** — Haga doble clic en la visualización de la forma de onda para abrirlo. El cajón está debajo de la traza de la forma de onda.
- **El control deslizante Zoom vuelve a su lugar después de arrastrarlo** — Esto puede ocurrir si no llega audio y la pantalla muestra el marcador de posición sin audio. El valor del control deslizante aún se guarda; surte efecto tan pronto como se reanude el audio.
- **El zoom se restablece después de reiniciar AetherSDR** — Verifique que el valor se esté persistencia. Si la aplicación se cerró de forma anormal, es posible que el ajuste `WaveApplet_ZoomPercent` no se haya escrito. Establezca el control deslizante al valor deseado después de un inicio limpio.
- **El ajuste de la ventana cambió inesperadamente después de una actualización** — Si actualiza desde una versión anterior que usaba el ajuste `WaveApplet_TimeWindowSec` (1–20 s lineal), el valor se migra automáticamente al paso discreto más cercano en `WaveApplet_TimeWindowMs`. Verifique el ajuste y ajústelo si es necesario.
- **El mensaje de marcador de posición sin audio cambió** — Cuando no llega audio de RX, la pantalla ahora muestra "Enable PC Audio" en lugar de "no RX audio". Esto indica que debe habilitar el audio de PC en la configuración de la radio o en la configuración de audio. Para TX, el mensaje aún muestra "no TX audio".
- **El applet Waveform no aparece después de habilitarlo** — Si el modo Lean está habilitado para el applet, permanecerá oculto incluso cuando esté activado. Deshabilite el modo Lean en el panel de gestión de applets para que la visualización de la forma de onda vuelva a ser visible.

## Relacionado

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
