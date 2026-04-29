# Uso del display de forma de onda para monitorear audio TX o RX

El applet Waveform muestra una vista de osciloscopio en el dominio del tiempo de la ruta de audio TX o RX activa. Úselo para detectar de un vistazo saturación de señal (clipping), interrupciones y problemas de nivel de audio sin interrumpir la operación.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE del panel lateral derecho para mostrarlo.
- El audio debe estar fluyendo a través de AetherSDR (transmitiendo o recibiendo) para que el display muestre una traza.

## Pasos

1. Localice el applet Waveform en el panel de applets del panel lateral derecho. Aparece de forma predeterminada después del botón EQ.
2. Observe el tinte de dirección: un tinte frío indica que el display muestra audio RX; un tinte cálido indica audio TX. La dirección también aparece en el encabezado (por ejemplo, `RX  RMS -24.3 dBFS  PK -18.1 dBFS`).
3. Observe la traza en busca de clipping. Las columnas de píxeles que contienen muestras saturadas se resaltan en rojo, y un contador `CLIP` aparece en la esquina superior derecha del display.
4. Verifique los niveles RMS y de pico en dBFS en el encabezado.
5. Verifique en el pie de página la frecuencia de muestreo actual, la ventana de tiempo de 100 ms y la escala de milisegundos por división.
6. Si no ha llegado audio recientemente, el display muestra un marcador de posición "No audio" en lugar de una traza.

## Qué hace cada control

| Control                    | Comportamiento                                                                                                                                                                                                          | Valor predeterminado                                                                                                                         |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Display de forma de onda   | Renderiza el envolvente mín./máx. por columna de píxeles con curvas de envolvente de pico y RMS. La ventana de tiempo está fija en 100 ms.                                                                              | En vivo                                                                                                                                      |
| Clic en el display         | Activa o desactiva la pausa. El display se congela en una instantánea del búfer hasta que se hace clic de nuevo.                                                                                                        | En vivo                                                                                                                                      |
| Doble clic en el display   | Abre o cierra el cajón de configuración.                                                                                                                                                                                | —                                                                                                                                            |
| Tinte de dirección         | Tinte frío = audio RX. Tinte cálido = audio TX.                                                                                                                                                                         | —                                                                                                                                            |
| Resaltado de clipping      | Las columnas que contienen muestras en 0.98 de escala completa o por encima se dibujan en rojo. Un conteo `CLIP N` aparece en el encabezado.                                                                            | Sin clipping                                                                                                                                 |
| Insignia PAUSED            | Se muestra en el pie de página cuando el display está congelado.                                                                                                                                                        | No se muestra (en vivo)                                                                                                                      |
| Marcador de posición sin audio | Reemplaza la traza cuando no han llegado muestras durante más de 1 segundo.                                                                                                                                         | —                                                                                                                                            |
| View                       | Selecciona el modo de visualización de la forma de onda: Scope (Graph = líneas mín./máx. + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de banda de frecuencia mediante filtro de Goertzel). | Scope. Se encuentra en el cajón de configuración desplegable debajo de la forma de onda. Se guarda como `Graph`, `Envelope`, `History` o `Bands`. |
| Zoom                       | Escala el eje de amplitud; los valores más altos estiran verticalmente las señales pequeñas, haciendo que los artefactos de clipping aparezcan antes. Rango: 1.0x–6.0x.                                                 | 1.7x (170%). Se encuentra en el cajón de configuración.                                                                                      |
| FPS                        | Controla con qué frecuencia se repinta la forma de onda; los valores más bajos reducen la carga de CPU en sistemas lentos. Rango: 5–30 Hz.                                                                              | 24 Hz. Se encuentra en el cajón de configuración.                                                                                            |

## Sugerencias

- El encabezado siempre indica la fuente (`RX` o `TX`), por lo que no es necesario depender únicamente del tinte al trabajar en condiciones de poca luz.
- Haga doble clic en el display para abrir el cajón de configuración y ajustar el modo de visualización, el nivel de zoom o la tasa de fotogramas sin salir del applet.
- No se requiere una conexión de radio para abrir el applet Waveform, pero los datos de audio en vivo requieren una ruta de audio activa.

## Solución de problemas

- **El display muestra el mensaje "No audio"** — No han llegado muestras del osciloscopio en el último segundo. Confirme que el audio está enrutado correctamente y que la radio está recibiendo o transmitiendo activamente.
- **La traza está congelada y no se actualiza** — El display está en pausa. Haga clic una vez en el display para reanudar. La insignia `PAUSED` en el pie de página confirma este estado.
- **El botón WAVE no está visible** — Abra `View > Applet Panel` para confirmar que el panel de applets está visible, o use `View > Reset Applet Order` para restaurar la disposición de applets predeterminada.

## Relacionado

- [Descripción general del applet Waveform](overview.md)
- [Pausar y limpiar el display de forma de onda](pause-and-clear-the-waveform-display.md)
