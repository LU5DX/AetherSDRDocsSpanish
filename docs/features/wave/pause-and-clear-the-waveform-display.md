# Pausar y limpiar la pantalla de forma de onda

La pantalla de forma de onda puede congelarse para inspeccionar un transitorio en detalle, o borrarse para empezar de nuevo. Use estos gestos para controlar lo que muestra la pantalla sin afectar la transmisión de audio en sí.

## Antes de comenzar

- El applet Waveform debe ser visible. Si no lo es, haga clic en el botón WAVE en la barra lateral derecha para mostrarlo.

## Pasos

### Pausar y reanudar

1. Haga clic una sola vez en cualquier lugar de la pantalla de forma de onda.
   La pantalla se congela en la instantánea actual del búfer. Aparece una insignia **PAUSED** en el pie de página.
2. Haga clic una sola vez en la pantalla de nuevo para reanudar la actualización en vivo. La insignia **PAUSED** desaparece.

### Limpiar el búfer

1. Haga doble clic en cualquier lugar de la pantalla de forma de onda.
   El cajón de configuración se abre o cierra. Para restablecer el búfer mediante programación, use el slot `WaveformWidget::clear()` o reconecte la fuente de audio.

## Qué hace cada control

| Interacción             | Comportamiento                                                                                                                                                                                                                   | Estado predeterminado                                                                                                    |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Clic único en la pantalla | Alterna entre en vivo y pausado. Mientras está pausado, se muestra una instantánea del búfer y aparece una insignia **PAUSED** en el pie de página.                                                                                | En vivo                                                                                                                  |
| Doble clic en la pantalla | Alterna el cajón de configuración abierto o cerrado. No limpia el búfer.                                                                                                                                                         | —                                                                                                                        |
| View                    | Selecciona el modo de visualización de forma de onda: Scope (Graph = líneas mín/máx + RMS), Envelope (área rellena pico/RMS), History (barras de nivel horizontales), Bands (barras de banda de frecuencia vía filtro Goertzel). | Ubicado en el cajón de configuración contraíble debajo de la forma de onda. Persistido como `Graph`, `Envelope`, `History`, o `Bands`. |
| Zoom                    | Escala el eje de amplitud; valores más altos estiran señales pequeñas verticalmente, causando que los artefactos de recorte aparezcan antes.                                                                                       | Ubicado en el cajón de configuración. Predeterminado 170% (1,7x).                                                      |
| FPS                     | Controla la frecuencia con la que se repinta la forma de onda; valores menores reducen la carga de CPU en sistemas lentos.                                                                                                       | Ubicado en el cajón de configuración.                                                                                    |

## Sugerencias

- Pausar es sensible a la dirección: la instantánea preserva cualquier lado (RX o TX) que estuviera activo en el momento en que hizo clic. El matiz de dirección y la etiqueta RX/TX en el encabezado permanecen visibles para que pueda identificar qué ruta está inspeccionando.
- El doble clic alterna el cajón de configuración, no el búfer. Para limpiar el búfer, use el slot `WaveformWidget::clear()` o reconecte para restablecer.
- La pantalla muestra una ventana de tiempo de 100 ms. Pausar es más útil cuando necesita medir un evento breve que de otro modo se desplazaría antes de que pueda examinarlo.
- A partir de v0.9.3, el applet Waveform ya no tiene un tamaño vertical fijo. Puede cambiar el tamaño verticalmente arrastrando el borde del panel del applet.

## Solución de problemas

- **El doble clic abre el cajón de configuración en lugar de limpiar el búfer** — Este es el comportamiento previsto a partir de v0.9.2.1. El doble clic ahora alterna el cajón de configuración. Para restablecer el búfer de forma de onda, use el slot `WaveformWidget::clear()` o reconecte la fuente de audio.
- **El clic único no pausa** — Qt desambigua clics simples de dobles usando el intervalo de doble clic del sistema. Haga clic una vez y espere; si la pantalla no se pausa, intente hacer clic más lentamente.
- **La insignia PAUSED no es visible** — La insignia aparece en el pie de página, a la derecha de la lectura de escala de tiempo. Si el applet es muy estrecho, el texto del pie de página puede truncarse. Amplíe el panel del applet o extraiga con `View > Pop Out Applet Panel`.

## Relacionado

- [Descripción general del applet Waveform](overview.md)
- [Usar la pantalla de forma de onda para monitorear audio TX o RX](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
