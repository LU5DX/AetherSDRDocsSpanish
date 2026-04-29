# Pausar y limpiar la pantalla de forma de onda

La pantalla de forma de onda puede congelarse para inspeccionar un transitorio en detalle, o borrarse por completo para empezar desde cero. Use estos gestos para controlar lo que muestra la pantalla sin afectar la señal de audio en sí.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE del panel lateral derecho para mostrarlo.

## Pasos

### Pausar y reanudar

1. Haga clic una vez en cualquier parte de la pantalla de forma de onda.
   La pantalla se congela en el instantánea actual del búfer. Aparece un indicador **PAUSED** en el pie de página.
2. Haga clic una vez más en la pantalla para reanudar la actualización en tiempo real. El indicador **PAUSED** desaparece.

### Limpiar el búfer

1. Haga doble clic en cualquier parte de la pantalla de forma de onda.
   El cajón de configuración se abre o se cierra. Para restablecer el búfer mediante programación, use el slot `WaveformWidget::clear()` o vuelva a conectar la fuente de audio.

## Qué hace cada control

| Interacción | Comportamiento | Estado predeterminado |
|---|---|---|
| Clic simple en la pantalla | Alterna entre modo en vivo y pausado. Mientras está pausado, se muestra una instantánea del búfer y aparece un indicador **PAUSED** en el pie de página. | En vivo |
| Doble clic en la pantalla | Abre o cierra el cajón de configuración. No borra el búfer. | — |
| View | Selecciona el modo de visualización de la forma de onda: Scope (Graph = líneas mín/máx + RMS), Envelope (área rellena con pico/RMS), History (barras de nivel horizontales), Bands (barras de banda de frecuencia mediante filtro de Goertzel). | Ubicado en el cajón de configuración desplegable debajo de la forma de onda. Se guarda como `Graph`, `Envelope`, `History` o `Bands`. |
| Zoom | Escala el eje de amplitud; los valores más altos estiran verticalmente las señales pequeñas y hacen que los artefactos de recorte aparezcan antes. | Ubicado en el cajón de configuración. Valor predeterminado: 170% (1.7x). |
| FPS | Controla la frecuencia de actualización de la pantalla; los valores más bajos reducen la carga de CPU en sistemas lentos. | Ubicado en el cajón de configuración. |

## Consejos

- La pausa tiene en cuenta la dirección: la instantánea preserva el lado (RX o TX) que estaba activo en el momento en que hizo clic. El color indicador de dirección y la etiqueta RX/TX del encabezado permanecen visibles para que pueda identificar qué ruta está inspeccionando.
- El doble clic abre o cierra el cajón de configuración, no borra el búfer. Para limpiar el búfer, use el slot `WaveformWidget::clear()` o vuelva a conectar para restablecerlo.
- La pantalla muestra una ventana de tiempo de 100 ms. La pausa es más útil cuando necesita medir un evento breve que de otro modo desaparecería antes de que pueda examinarlo.

## Solución de problemas

- **El doble clic abre el cajón de configuración en lugar de limpiar el búfer** — Este es el comportamiento esperado a partir de la versión v0.9.2.1. El doble clic ahora abre o cierra el cajón de configuración. Para restablecer el búfer de forma de onda, use el slot `WaveformWidget::clear()` o vuelva a conectar la fuente de audio.
- **El clic simple no pausa la pantalla** — Qt distingue entre clic simple y doble clic usando el intervalo de doble clic del sistema. Haga clic una vez y espere; si la pantalla no se pausa, intente hacer clic más despacio.
- **El indicador PAUSED no es visible** — El indicador aparece en el pie de página, a la derecha de la escala de tiempo. Si el applet es muy estrecho, el texto del pie de página puede aparecer truncado. Amplíe el panel del applet o extráigalo con `View > Pop Out Applet Panel`.

## Temas relacionados

- [Descripción general del applet Waveform](overview.md)
- [Usar la pantalla de forma de onda para monitorear el audio TX o RX](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
