# Pausar y limpiar la visualización de la forma de onda

La visualización de la forma de onda puede congelarse para que pueda inspeccionar un transitorio en detalle, o limpiarse por completo para empezar de nuevo. Utilice estos gestos para controlar lo que muestra la pantalla sin afectar al flujo de audio en sí.

## Antes de empezar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

### Pausar y reanudar

1. Haga un solo clic en cualquier lugar de la pantalla de forma de onda.
   La pantalla se congela en la instantánea del búfer actual. Aparece una insignia **PAUSED** en el pie de página.
2. Vuelva a hacer clic una vez en la pantalla para reanudar la actualización en vivo. La insignia **PAUSED** desaparece.

### Limpiar el búfer

1. Haga doble clic en cualquier lugar de la pantalla de forma de onda.
   El panel de configuración se abre o se cierra. Para restablecer el búfer mediante programación, use el slot `WaveformWidget::clear()` o reconecte la fuente de audio.

## Función de cada control

| Interacción                | Comportamiento                                                                                                                                                                                     | Estado predeterminado                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| Un solo clic en la pantalla | Alterna entre vivo y pausado. Mientras está pausado, se muestra una instantánea del búfer y aparece una insignia **PAUSED** en el pie de página.                                                  | Vivo                                                                                                                             |
| Doble clic en la pantalla  | Abre o cierra el panel de configuración. No limpia el búfer.                                                                                                                                       | —                                                                                                                                |
| View                       | Selecciona el modo de visualización de la forma de onda: Scope (Gráfico = líneas de mínimo/máximo + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de bandas de frecuencia mediante el filtro Goertzel). | Se encuentra en el panel de configuración plegable debajo de la forma de onda. Se conserva como `Graph`, `Envelope`, `History` o `Bands`. |
| Zoom                       | Escala el eje de amplitud; los valores más altos estiran verticalmente las señales pequeñas, haciendo que los artefactos de recorte aparezcan antes.                                                 | Se encuentra en el panel de configuración. Valor predeterminado 170% (1.7x).                                                      |
| FPS                        | Controla la frecuencia con la que se redibuja la forma de onda; los valores más bajos reducen la carga de la CPU en sistemas lentos.                                                               | Se encuentra en el panel de configuración.                                                                                        |

## Consejos

- La pausa reconoce la dirección: la instantánea conserva el lado (RX o TX) que estaba activo en el momento en que hizo clic. El tinte de dirección y la etiqueta RX/TX en el encabezado permanecen visibles para que pueda saber qué ruta está inspeccionando.
- El doble clic abre o cierra el panel de configuración, no el búfer. Para limpiar el búfer, use el slot `WaveformWidget::clear()` o reconéctese para restablecerlo.
- La pantalla muestra una ventana de tiempo de 100 ms. Pausar es más útil cuando necesita medir un evento breve que, de otro modo, se desplazaría antes de que pueda examinarlo.
- A partir de v0.9.3, el applet Waveform ya no tiene un tamaño vertical fijo. Puede cambiar su tamaño verticalmente arrastrando el borde del panel del applet.

## Solución de problemas

- **El doble clic abre el panel de configuración en lugar de limpiar el búfer** — Este es el comportamiento previsto a partir de v0.9.2.1. El doble clic ahora abre o cierra el panel de configuración. Para restablecer el búfer de forma de onda, use el slot `WaveformWidget::clear()` o reconecte la fuente de audio.
- **Un solo clic no pausa** — Qt distingue entre clics simples y dobles utilizando el intervalo de doble clic del sistema. Haga clic una vez y espere; si la pantalla no se pausa, intente hacer clic más lentamente.
- **La insignia PAUSED no es visible** — La insignia aparece en el pie de página, a la derecha del indicador de escala de tiempo. Si el applet es muy estrecho, el texto del pie de página puede truncarse. Aumente el ancho del panel del applet o sáquelo con `View > Pop Out Applet Panel`.

## Relacionado

- [Waveform applet overview](overview.md)
- [Use the waveform display to monitor TX or RX audio](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
