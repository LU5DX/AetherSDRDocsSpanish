# Use la visualización de forma de onda para monitorear audio de TX o RX

El applet de forma de onda muestra una vista de osciloscopio en el dominio del tiempo de la ruta de audio activa de TX o RX. Úselo para detectar recorte, caídas y problemas de nivel de audio de un vistazo sin interrumpir la operación.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para mostrarlo.
- El audio debe estar fluyendo a través de AetherSDR (transmitiendo o recibiendo) para que la visualización muestre una traza.

## Pasos

1. Localice el applet de forma de onda en el panel de applets de la barra lateral derecha. Aparece por defecto después del botón EQ.
2. Observe el tinte de dirección: un tinte frío indica que la visualización está mostrando audio de RX; un tinte cálido indica audio de TX. La dirección también aparece en el indicador del encabezado (por ejemplo, `RX  RMS -24.3 dBFS  PK -18.1 dBFS`).
3. Observe la traza en busca de recorte. Las columnas de píxeles que contienen muestras recortadas se resaltan en rojo, y un contador `CLIP` aparece en la esquina superior derecha de la visualización.
4. Verifique el indicador del encabezado para los niveles RMS y pico en dBFS.
5. Verifique el pie de página para la tasa de muestreo actual, la ventana de tiempo de 100 ms y la escala de milisegundos por división.
6. Si no ha llegado audio recientemente, la visualización muestra un marcador de posición "No audio" en lugar de una traza.

## Qué hace cada control

| Control                      | Comportamiento                                                                                                                                                                                                                      | Predeterminado                                                                                                             |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Visualización de forma de onda | Renderiza el sobre mínimo/máximo por columna de píxel con curvas de sobre pico y RMS. La ventana de tiempo es fija en 100 ms.                                                                                                       | En vivo                                                                                                                    |
| Clic en la visualización     | Alterna la pausa. La pantalla se congela en una instantánea del búfer hasta que se hace clic de nuevo.                                                                                                                              | En vivo                                                                                                                    |
| Doble clic en la visualización | Alterna la apertura o cierre del cajón de configuración.                                                                                                                                                                           | —                                                                                                                          |
| Tinte de dirección           | Tinte frío = audio RX. Tinte cálido = audio TX.                                                                                                                                                                                     | —                                                                                                                          |
| Resaltado de recorte         | Las columnas que contienen muestras en o por encima de 0.98 de escala completa se dibujan en rojo. Aparece un conteo `CLIP N` en el encabezado.                                                                                     | Sin recorte                                                                                                                |
| Insignia PAUSED              | Se muestra en el pie de página cuando la visualización está congelada.                                                                                                                                                              | No se muestra (en vivo)                                                                                                    |
| Marcador de posición sin audio | Reemplaza la traza cuando no han llegado muestras durante más de 1 segundo.                                                                                                                                                        | —                                                                                                                          |
| Vista                        | Selecciona el modo de visualización de forma de onda: Scope (Gráfico = líneas mín/máx + RMS), Envelope (área rellena pico/RMS), History (barras de nivel horizontales), Bands (barras de banda de frecuencia mediante filtro Goertzel). | Scope. Ubicado en el cajón de configuración plegable debajo de la forma de onda. Persistido como `Graph`, `Envelope`, `History` o `Bands`. |
| Zoom                         | Escala el eje de amplitud; valores más altos estiran las señales pequeñas verticalmente, lo que hace que los artefactos de recorte aparezcan antes. Rango: 1.0x–6.0x.                                                               | 1.7x (170%). Ubicado en el cajón de configuración.                                                                         |
| FPS                          | Controla la frecuencia con la que se vuelve a dibujar la forma de onda; valores más bajos reducen la carga de la CPU en sistemas lentos. Rango: 5–30 Hz.                                                                            | 24 Hz. Ubicado en el cajón de configuración.                                                                               |

## Consejos

- El indicador del encabezado siempre etiqueta la fuente (`RX` o `TX`), por lo que no es necesario confiar únicamente en el tinte cuando se trabaja en condiciones de poca luz.
- Haga doble clic en la visualización para abrir el cajón de configuración y ajustar el modo de vista, el nivel de zoom o la velocidad de fotogramas sin salir del applet.
- El applet de forma de onda se redimensiona verticalmente con su contenedor. Puede arrastrar el divisor del panel de applets para darle a la forma de onda más o menos espacio vertical.
- No se requiere una conexión de radio para que se abra el applet de forma de onda, pero los datos de audio en vivo requieren una ruta de audio activa.

## Solución de problemas

- **La visualización muestra el mensaje "No audio"** — No han llegado muestras de alcance en el último segundo. Confirme que el audio esté enrutado correctamente y que la radio esté recibiendo o transmitiendo activamente.
- **La traza está congelada y no se actualiza** — La visualización está en pausa. Haga clic en la visualización una vez para reanudarla. La insignia `PAUSED` en el pie de página confirma este estado.
- **El botón de bandeja WAVE no está visible** — Abra `View > Applet Panel` para confirmar que el panel de applets esté visible, o use `View > Reset Applet Order` para restaurar la disposición predeterminada de applets.

## Relacionado

- [Descripción general del applet de forma de onda](overview.md)
- [Pausar y limpiar la visualización de forma de onda](pause-and-clear-the-waveform-display.md)
