# Monitorizar audio de TX o RX en la pantalla de forma de onda

El applet de forma de onda (Waveform) muestra una vista en vivo en el dominio del tiempo de la ruta de audio activa de TX o RX. Úselo para detectar recortes, cortes y problemas de nivel de audio sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio: el applet muestra el audio del motor de audio local.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de la bandeja WAVE en la fila superior de botones de la barra lateral derecha.
2. Haga clic en WAVE para mostrar el applet de forma de onda. Vuelva a hacer clic para ocultarlo.
3. Observe la pantalla de forma de onda. La traza se tiñe de tono frío al monitorizar audio de RX y de tono cálido al monitorizar audio de TX — no es necesario leer etiquetas.
4. Verifique la lectura del encabezado para ver la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel pico en dBFS.
5. Si no ha llegado audio en un segundo, la pantalla muestra un marcador de posición "no RX audio" o "no TX audio" en lugar de una traza vacía.
6. Para abrir el cajón de ajustes, haga doble clic en cualquier lugar de la pantalla de forma de onda. Vuelva a hacer doble clic para cerrarlo.
7. En el cajón de ajustes, use el cuadro combinado View para elegir una visualización: **Scope**, **Envelope**, **History** o **Bands**. El valor predeterminado es **Scope**.
8. Use el control deslizante Zoom para escalar el eje de amplitud. El valor predeterminado es 1,7x (rango 1,0x–6,0x). Arrastre hacia la derecha para ampliar señales pequeñas; con valores de zoom altos, los artefactos de recorte aparecen antes.
9. Use el control deslizante FPS para establecer la frecuencia con la que se actualiza la pantalla (rango 5–30 Hz, predeterminado 24). Los valores más bajos reducen la carga de la CPU.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| View | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra la forma de onda mín/máx y líneas RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de bandas de frecuencia. |
| Zoom | 1,7x (170) | 1,0x–6,0x (100–600) | `WaveApplet_ZoomPercent` | Escala verticalmente el eje de amplitud. |
| FPS | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de repintado. |
| Clic en la pantalla | En vivo | En vivo / Pausado | — | Alterna la pausa. Aparece una etiqueta PAUSED en el pie de página mientras la pantalla está congelada. |
| Doble clic en la pantalla | — | — | — | Abre o cierra el cajón de ajustes. |

## Consejos

- Cuando se produce recorte, las columnas afectadas se resaltan y aparece un contador CLIP N en el encabezado. Reduzca el nivel de excitación de audio o disminuya el valor de Zoom para que la señal vuelva al rango.
- Haga clic una vez en la forma de onda para congelar una instantánea cuando note un transitorio. Vuelva a hacer clic para reanudar la vista en vivo.
- El cajón de ajustes se abre en el estado expandido cada vez que inicia AetherSDR.

## Solución de problemas

- **La pantalla muestra "no RX audio" o "no TX audio"** — No han llegado muestras de alcance en el último segundo. Verifique que el audio fluya a través de la ruta correspondiente y que el dispositivo de audio correcto esté seleccionado en `Settings > Radio Setup...`.
- **Falta el botón de la bandeja WAVE** — El panel de applets puede estar oculto. Actívelo mediante `View > Applet Panel`. Si el panel está visible pero WAVE no aparece, use `View > Reset Applet Order` para restaurar la disposición de applets predeterminada.

## Relacionados

- [Waveform overview](overview.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
