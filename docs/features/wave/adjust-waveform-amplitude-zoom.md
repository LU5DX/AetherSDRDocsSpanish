# Ajustar el zoom de amplitud de la forma de onda

El control deslizante Zoom del applet Waveform escala el eje de amplitud de la pantalla de forma de onda. Aumentar el zoom estira verticalmente las señales débiles para facilitar su lectura; disminuirlo evita que los artefactos de recorte oscurezcan la traza en señales de nivel alto.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para mostrarlo.
- El panel de configuración debe estar abierto. Si solo es visible la traza de la forma de onda sin controles debajo, haga doble clic en la pantalla de forma de onda para abrir el panel.

## Pasos

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración si aún no está abierto.
2. Localice la fila Zoom en el panel de configuración.
3. Arrastre el control deslizante Zoom hacia la izquierda para disminuir el zoom o hacia la derecha para aumentarlo. El indicador a la derecha del control se actualiza de inmediato y muestra el valor actual como un multiplicador (por ejemplo, `1.7x`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente en `WaveApplet_ZoomPercent`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Zoom | 170 (1.7x) | 100–600 (mostrado como 1.0x–6.0x) | `WaveApplet_ZoomPercent` |

El valor del control deslizante es un porcentaje entero. La pantalla de forma de onda lo divide entre 100 para producir el multiplicador que se muestra en el indicador. Un valor de 100 significa sin zoom (1.0x); 600 es el zoom máximo (6.0x).

## Consejos

- Con niveles de zoom altos, las señales cercanas a la escala máxima producirán indicadores de recorte (énfasis en columna roja y un contador CLIP N en el encabezado). Si aparecen indicadores de recorte frecuentes tras aumentar el zoom, reduzca el valor hasta que la traza quepa dentro de la pantalla sin alcanzar los bordes.
- La configuración de zoom se aplica por igual a las rutas RX y TX. El tinte de dirección (frío para RX, cálido para TX) sigue distinguiendo qué ruta está activa independientemente del nivel de zoom.
- Para inspeccionar un transitorio a mayor zoom sin perderlo en tiempo real, pause primero la pantalla haciendo un solo clic en la forma de onda y luego ajuste el zoom mientras la instantánea está congelada.

## Solución de problemas

- **El panel de configuración no es visible** — Haga doble clic en la pantalla de forma de onda para alternarlo entre abierto y cerrado. El panel se encuentra debajo de la traza de la forma de onda.
- **El control deslizante Zoom regresa a su posición anterior al arrastrarlo** — Esto puede ocurrir si no llega audio y la pantalla muestra el marcador de posición de ausencia de audio. El valor del control deslizante se guarda de todas formas; surte efecto en cuanto se reanuda el audio.
- **El zoom se restablece al reiniciar AetherSDR** — Verifique que el valor se esté persistiendo. Si la aplicación se cerró de forma anormal, es posible que la configuración `WaveApplet_ZoomPercent` no se haya escrito. Establezca el control deslizante en el valor deseado tras un inicio limpio.

## Relacionados

- [Descripción general de Waveform](overview.md)
- [Monitorear audio TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Establecer la tasa de actualización de la forma de onda para reducir la carga de CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
