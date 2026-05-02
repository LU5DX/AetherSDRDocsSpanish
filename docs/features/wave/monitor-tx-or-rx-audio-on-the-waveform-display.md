# Monitorear audio TX o RX en la pantalla de forma de onda

El applet Waveform muestra una vista en tiempo real del dominio temporal de la ruta de audio TX o RX activa. Úselo para detectar saturación (clipping), interrupciones y problemas de nivel de audio sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio — el applet muestra el audio del motor de audio local.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja WAVE en la fila superior de botones de bandeja de la barra lateral derecha.
2. Haga clic en WAVE para mostrar el applet Waveform. Haga clic nuevamente para ocultarlo.
3. Observe la pantalla de forma de onda. La traza tiene un tono frío al monitorear audio RX y un tono cálido al monitorear audio TX — no es necesario leer ninguna etiqueta.
4. Revise el indicador del encabezado para conocer la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel de pico en dBFS.
5. Si no ha llegado audio en un segundo, la pantalla muestra un marcador de posición "no RX audio" o "no TX audio" en lugar de una traza vacía.
6. Para abrir el cajón de configuración, haga doble clic en cualquier parte de la pantalla de forma de onda. Haga doble clic nuevamente para cerrarlo.
7. En el cajón de configuración, use el cuadro combinado View para elegir una visualización: **Scope**, **Envelope**, **History** o **Bands**. El valor predeterminado es **Scope**.
8. Use el control deslizante Zoom para escalar el eje de amplitud. El valor predeterminado es 1.7x (rango 1.0x–6.0x). Arrastre hacia la derecha para ampliar señales pequeñas; con valores de zoom altos, los artefactos de saturación aparecen antes.
9. Use el control deslizante FPS para establecer la frecuencia de actualización de la pantalla (rango 5–30 Hz, valor predeterminado 24). Los valores más bajos reducen la carga del CPU.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| View | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra la forma de onda mín/máx y líneas RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de bandas de frecuencia. |
| Zoom | 1.7x (170) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala el eje de amplitud verticalmente. |
| FPS | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de actualización de la pantalla. |
| Clic en la pantalla | En vivo | En vivo / Pausado | — | Alterna la pausa. Un indicador PAUSED aparece en el pie de página mientras la pantalla está congelada. |
| Doble clic en la pantalla | — | — | — | Abre o cierra el cajón de configuración. |

## Consejos

- Cuando ocurre saturación, las columnas afectadas se resaltan y aparece un contador CLIP N en el encabezado. Reduzca el nivel de la señal de audio o disminuya el valor de Zoom para que la señal vuelva a estar dentro del rango.
- Haga clic una vez en la forma de onda para congelar una instantánea cuando detecte un transitorio. Haga clic nuevamente para reanudar la vista en vivo.
- El cajón de configuración se abre en estado expandido cada vez que inicia AetherSDR.

## Solución de problemas

- **La pantalla muestra "no RX audio" o "no TX audio"** — No han llegado muestras al osciloscopio en el último segundo. Verifique que el audio esté fluyendo por la ruta correspondiente y que el dispositivo de audio correcto esté seleccionado en `Settings > Radio Setup...`.
- **El botón de bandeja WAVE no aparece** — Es posible que el panel de applets esté oculto. Actívelo mediante `View > Applet Panel`. Si el panel está visible pero WAVE no aparece, use `View > Reset Applet Order` para restaurar la disposición predeterminada de applets.

## Temas relacionados

- [Descripción general de Waveform](overview.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Cambiar el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Establecer la tasa de actualización de la forma de onda para reducir la carga del CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
