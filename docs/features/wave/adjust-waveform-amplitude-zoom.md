# Ajustar el zoom de la amplitud de la forma de onda

El deslizador Zoom del applet Waveform escala el eje de amplitud de la visualización de la forma de onda. Aumentar el zoom estira las señales pequeñas verticalmente para que sean más fáciles de leer; reducirlo evita que los artefactos de recorte oculten la traza en señales fuertes.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El cajón de ajustes debe estar abierto. Si solo se ve la traza de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de ajustes si aún no está abierto.
2. Localice la fila Zoom en el cajón de ajustes.
3. Arrastre el deslizador Zoom hacia la izquierda para reducir el zoom o hacia la derecha para aumentarlo. La lectura a la derecha del deslizador se actualiza inmediatamente, mostrando el valor actual como un multiplicador (por ejemplo, `1.7x`).
4. Suelte el deslizador. El nuevo valor se guarda automáticamente en `WaveApplet_ZoomPercent`.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|
| Zoom | 170 (1.7x) | 100–600 (se muestra como 1.0x–6.0x) | `WaveApplet_ZoomPercent` |

El valor del deslizador es un porcentaje entero. La visualización de la forma de onda lo divide entre 100 para producir el multiplicador que se muestra en la lectura. Un valor de 100 significa sin zoom (1.0x); 600 es el zoom máximo (6.0x).

## Consejos

- Con niveles altos de zoom, las señales cercanas a la escala completa producirán indicaciones de recorte (énfasis en columnas rojas y un contador CLIP N en el encabezado). Si ve indicadores de recorte frecuentes después de aumentar el zoom, reduzca el valor hasta que la traza quepa dentro de la visualización sin tocar los bordes.
- El ajuste de zoom se aplica por igual a las rutas de RX y TX. El matiz de dirección (frío para RX, cálido para TX) aún distingue qué ruta está activa independientemente del nivel de zoom.
- Para inspeccionar un transitorio con mayor zoom sin perderlo en tiempo real, primero pause la visualización haciendo un solo clic en la forma de onda, luego ajuste el zoom mientras la instantánea está congelada.

## Solución de problemas

- **El cajón de ajustes no es visible** — Haga doble clic en la visualización de la forma de onda para alternar su apertura. El cajón está debajo de la traza de la forma de onda.
- **El deslizador Zoom retrocede después de arrastrarlo** — Esto puede ocurrir si no llega audio y la visualización muestra el marcador de posición de ausencia de audio. El valor del deslizador aún se guarda; surte efecto tan pronto como se reanuda el audio.
- **El zoom se restablece después de reiniciar AetherSDR** — Verifique que el valor se esté guardando. Si la aplicación se cerró de forma anormal, es posible que el ajuste `WaveApplet_ZoomPercent` no se haya escrito. Ajuste el deslizador al valor deseado después de un inicio limpio.

## Relacionados

- [Descripción general de Waveform](overview.md)
- [Monitorizar audio de TX o RX en la visualización de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Ajustar la frecuencia de actualización de la forma de onda para reducir la carga de la CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
