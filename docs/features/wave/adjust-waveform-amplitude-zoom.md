# Ajustar el zoom de amplitud de la forma de onda y la ventana de tiempo

El control deslizante Zoom del applet de forma de onda escala el eje de amplitud de la visualización de la forma de onda. Aumentar el zoom estira verticalmente las señales débiles para que sean más fáciles de leer; reducirlo evita que los artefactos de recorte oculten la traza en señales fuertes. El control deslizante Window controla la ventana de tiempo que se muestra en la visualización de la forma de onda.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para mostrarlo.
- El cajón de ajustes debe estar abierto. Si solo se ve la traza de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón. El estado del cajón se conserva entre sesiones.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de ajustes si aún no está abierto.
2. Localice la fila Zoom o la fila Window en el cajón de ajustes.
3. Ajuste el control deslizante deseado:
   - Arrastre el control deslizante **Zoom** hacia la izquierda para reducir el zoom o hacia la derecha para aumentarlo. La lectura a la derecha del control se actualiza inmediatamente, mostrando el valor actual como un multiplicador (por ejemplo, `1.7x`).
   - Arrastre el control deslizante **Window** hacia la izquierda para reducir la ventana de tiempo o hacia la derecha para aumentarla. La lectura a la derecha del control se actualiza inmediatamente, mostrando el valor actual en milisegundos (por ejemplo, `200 ms`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente en `WaveApplet_ZoomPercent` o `WaveApplet_TimeWindowMs`. El estado expandido/contraído del cajón también se guarda automáticamente en `WaveApplet_DrawerExpanded`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido |
|---------|----------------------|--------------|
| Zoom    | 170 (1.7x)           | 100–600 (mostrado como 1.0x–6.0x) |
| Window  | 200 ms               | 10–500 ms (continuo)              |

El valor del control deslizante Zoom es un porcentaje entero. La visualización de la forma de onda lo divide por 100 para producir el multiplicador mostrado en la lectura. Un valor de 100 significa sin zoom (1.0x); 600 es el zoom máximo (6.0x).

El control deslizante Window es un rango continuo de 10 ms a 500 ms, lo que le da control total sobre la ventana de tiempo. Los valores más pequeños (alrededor de 10–50 ms) proporcionan detalles finos en formas de onda rápidas; los valores más grandes (hasta 500 ms) muestran más historial con resolución reducida.

## El estado del cajón de ajustes

El cajón de ajustes (que contiene los controles View, Zoom, Window y FPS) recuerda si estaba abierto o cerrado la última vez que usó el applet. Cuando vuelve a abrir el applet de forma de onda, el cajón restaura su estado anterior. Si desea que el cajón esté siempre abierto, déjelo abierto antes de cerrar el applet o reiniciar AetherSDR.

## Consejos

- Con niveles de zoom altos, las señales cercanas a la escala completa producirán indicadores de recorte (énfasis en columna rojo y un contador CLIP N en el encabezado). Si ve indicadores de recorte frecuentes después de aumentar el zoom, reduzca el valor hasta que la traza quepa dentro de la visualización sin tocar los bordes.
- Los ajustes de zoom y ventana se aplican por igual a las rutas RX y TX. El tinte de dirección (frío para RX, cálido para TX) sigue distinguiendo qué ruta está activa independientemente del nivel de zoom.
- Para inspeccionar un transitorio con mayor zoom sin perderlo en tiempo real, primero ponga en pausa la visualización haciendo un solo clic en la forma de onda, luego ajuste el zoom mientras la instantánea está congelada.
- Use una ventana más corta (alrededor de 50 ms) para ver detalles finos en formas de onda rápidas. Use una ventana más larga (hasta 500 ms) para ver cambios generales de nivel a lo largo del tiempo.
- El intervalo de discriminación de clics utilizado para distinguir un clic simple de un doble clic respeta el valor que establezca en Radio Setup → Interaction Settings. Los cambios en ese ajuste tienen efecto inmediato sin reiniciar AetherSDR.

## Solución de problemas

- **El cajón de ajustes no es visible** — Haga doble clic en la visualización de la forma de onda para alternar su apertura. El cajón está debajo de la traza de la forma de onda.
- **El control deslizante Zoom vuelve a su posición después de arrastrarlo** — Esto puede ocurrir si no llega audio y la visualización muestra el marcador de posición sin audio. El valor del control se guarda igualmente; tiene efecto en cuanto se reanuda el audio.
- **El zoom se restablece después de reiniciar AetherSDR** — Verifique que el valor se esté guardando. Si la aplicación se cerró de forma anormal, es posible que el ajuste `WaveApplet_ZoomPercent` no se haya escrito. Establezca el control deslizante al valor deseado después de un inicio limpio.
- **El ajuste de ventana cambió inesperadamente después de una actualización** — Si actualiza desde una versión anterior que usaba el ajuste `WaveApplet_TimeWindowSec` (lineal de 1 a 20 s), el valor se migra automáticamente al valor más cercano en `WaveApplet_TimeWindowMs`. Verifique el ajuste y modifíquelo si es necesario.
- **El mensaje del marcador de posición sin audio cambió** — Cuando no llega audio de RX, la visualización ahora muestra «Enable PC Audio» en lugar de «no RX audio». Esto indica que debe habilitar el audio de PC en los ajustes de radio o en la configuración de audio. Para TX, el mensaje sigue mostrando «no TX audio».

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio de TX o RX en la visualización de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Establecer la frecuencia de actualización de la forma de onda para reducir la carga de CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
