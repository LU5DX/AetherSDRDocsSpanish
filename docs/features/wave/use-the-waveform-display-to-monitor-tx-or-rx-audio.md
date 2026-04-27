# Usar la pantalla de forma de onda para supervisar el audio TX o RX

El applet Waveform muestra una vista de osciloscopio en el dominio del tiempo del camino de audio TX o RX activo. Úselo para detectar saturación (clipping), interrupciones y problemas de nivel de audio de un vistazo, sin interrumpir la operación.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE del panel lateral derecho para mostrarlo.
- El audio debe estar fluyendo a través de AetherSDR (transmitiendo o recibiendo) para que la pantalla muestre una traza.

## Pasos

1. Ubique el applet Waveform en el panel de applets del panel lateral derecho. Aparece por defecto después del botón EQ.
2. Observe el tinte de dirección: un tinte frío indica que la pantalla muestra audio RX; un tinte cálido indica audio TX. La dirección también aparece en la lectura del encabezado (por ejemplo, `RX  RMS -24.3 dBFS  PK -18.1 dBFS`).
3. Observe la traza en busca de saturación. Las columnas de píxeles que contienen muestras saturadas se resaltan en rojo y aparece un contador `CLIP` en la esquina superior derecha de la pantalla.
4. Verifique la lectura del encabezado para los niveles RMS y de pico en dBFS.
5. Verifique el pie de página para conocer la frecuencia de muestreo actual, la ventana de tiempo de 100 ms y la escala de milisegundos por división.
6. Si no ha llegado audio recientemente, la pantalla muestra un marcador "No audio" en lugar de una traza.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---|---|---|---|
| Pantalla Waveform | Representa la envolvente mínima/máxima por columna de píxeles con curvas de envolvente de pico y RMS. La ventana de tiempo está fija en 100 ms. | En vivo | Muestra RX o TX según la dirección activa. |
| Clic en la pantalla | Activa o desactiva la pausa. La pantalla se congela en una instantánea del búfer hasta que se hace clic de nuevo. | En vivo | Aparece un distintivo `PAUSED` en el pie de página mientras está en pausa. |
| Doble clic en la pantalla | Borra el búfer circular de la dirección activa (RX o TX). Restablece la pantalla a vacío. | — | No afecta el búfer de la otra dirección. |
| Tinte de dirección | Tinte frío = audio RX. Tinte cálido = audio TX. | — | Cambia automáticamente cuando la radio alterna entre transmisión y recepción. |
| Resaltado de saturación | Las columnas que contienen muestras en 0.98 de escala completa o por encima se dibujan en rojo. Aparece un recuento `CLIP N` en el encabezado. | Sin saturación | No se requiere ninguna acción; el resaltado aparece automáticamente. |
| Distintivo PAUSED | Se muestra en el pie de página cuando la pantalla está congelada. | No mostrado (en vivo) | Haga clic en la pantalla una vez para reanudar. |
| Marcador de sin audio | Reemplaza la traza cuando no han llegado muestras durante más de 1 segundo. | — | Desaparece en cuanto el audio se reanuda. |

## Consejos

- La lectura del encabezado siempre indica la fuente (`RX` o `TX`), por lo que no es necesario depender únicamente del tinte al trabajar en condiciones de poca luz.
- La información emergente (tooltip) de la pantalla dice "Click to pause/resume waveform capture" como recordatorio rápido del comportamiento al hacer clic.
- No se requiere una conexión de radio para que el applet Waveform se abra, pero los datos de audio en vivo requieren un camino de audio activo.

## Resolución de problemas

- **La pantalla muestra el mensaje "No audio"** — No han llegado muestras al osciloscopio en el último segundo. Confirme que el audio está enrutado correctamente y que la radio está recibiendo o transmitiendo activamente.
- **La traza está congelada y no se actualiza** — La pantalla está en pausa. Haga clic en la pantalla una vez para reanudar. El distintivo `PAUSED` en el pie de página confirma este estado.
- **El botón WAVE no está visible** — Abra `View > Applet Panel` para confirmar que el panel de applets está visible, o use `View > Reset Applet Order` para restaurar la disposición de applets predeterminada.

## Relacionados

- [Descripción general del applet Waveform](overview.md)
- [Pausar y borrar la pantalla de forma de onda](pause-and-clear-the-waveform-display.md)
