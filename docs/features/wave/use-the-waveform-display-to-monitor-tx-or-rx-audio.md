# Use the waveform display to monitor TX or RX audio

El applet Waveform muestra una vista de osciloscopio en el dominio del tiempo de la ruta de audio TX o RX activa. Úselo para detectar recortes, interrupciones y problemas de nivel de audio de un vistazo sin interrumpir la operación.

## Before you start

- El applet Waveform debe estar visible. Si no es así, haga clic en el botón WAVE en la barra lateral derecha para mostrarlo.
- El audio debe fluir a través de AetherSDR (transmitiendo o recibiendo) para que la pantalla muestre un trazo.

## Steps

1. Localice el applet Waveform en el panel de applets de la barra lateral derecha. Aparece por defecto después del botón EQ.
2. Observe el matiz de dirección: un matiz frío significa que la pantalla muestra audio RX; un matiz cálido significa audio TX. La dirección también aparece en la lectura del encabezado (por ejemplo, `RX  RMS -24.3 dBFS  PK -18.1 dBFS`).
3. Observe el trazo para detectar recortes. Las columnas de píxeles que contienen muestras recortadas se resaltan en rojo, y un contador `CLIP` aparece en la esquina superior derecha de la pantalla.
4. Compruebe la lectura del encabezado para los niveles RMS y pico en dBFS.
5. Compruebe el pie de página para la velocidad de muestreo actual, la ventana de tiempo de 100 ms y la escala de milisegundos por división.
6. Si no ha llegado audio recientemente, la pantalla muestra un marcador de posición "No audio" en lugar de un trazo.

## What each control does

| Control                 | Behavior                                                                                                                                                                                         | Default                                                                                                                  |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Waveform display        | Renders the min/max envelope per pixel column with peak and RMS envelope curves. Time window is fixed at 100 ms.                                                                                 | Live                                                                                                                     |
| Click on display        | Toggles pause. The display freezes on a snapshot of the buffer until clicked again.                                                                                                              | Live                                                                                                                     |
| Double-click on display | Toggles the settings drawer open or closed.                                                                                                                                                      | —                                                                                                                        |
| Direction tint          | Cool tint = RX audio. Warm tint = TX audio.                                                                                                                                                      | —                                                                                                                        |
| Clipping highlight      | Columns containing samples at or above 0.98 full scale are drawn in red. A `CLIP N` count appears in the header.                                                                                 | No clipping                                                                                                              |
| PAUSED badge            | Shown in the footer when the display is frozen.                                                                                                                                                  | Not shown (live)                                                                                                         |
| No-audio placeholder    | Replaces the trace when no samples have arrived for more than 1 second.                                                                                                                          | —                                                                                                                        |
| View                    | Selects the waveform visualization mode: Scope (Graph = min/max + RMS lines), Envelope (peak/RMS filled area), History (horizontal level bars), Bands (frequency band bars via Goertzel filter). | Scope. Located in the collapsible settings drawer below the waveform. Persisted as `Graph`, `Envelope`, `History`, or `Bands`. |
| Zoom                    | Scales the amplitude axis; higher values stretch small signals vertically, causing clipping artifacts to appear sooner. Range: 1.0x–6.0x.                                                        | 1.7x (170%). Located in the settings drawer.                                                                             |
| FPS                     | Controls how often the waveform repaints; lower values reduce CPU load on slow systems. Range: 5–30 Hz.                                                                                          | 24 Hz. Located in the settings drawer.                                                                                   |

## Tips

- La lectura del encabezado siempre etiqueta la fuente (`RX` o `TX`) para que no tenga que depender únicamente del matiz cuando trabaja en condiciones de poca luz.
- Haga doble clic en la pantalla para abrir el cajón de configuración y ajuste el modo de vista, el nivel de zoom o la velocidad de fotogramas sin salir del applet.
- El applet Waveform se redimensiona verticalmente con su contenedor. Puede arrastrar el divisor del panel del applet para dar al waveform más o menos espacio vertical.
- No se requiere una conexión de radio para que se abra el applet Waveform, pero los datos de audio en vivo requieren una ruta de audio activa.

## Troubleshooting

- **Display shows "No audio" message** — No scope samples have arrived in the last 1 second. Confirm audio is routed correctly and the radio is actively receiving or transmitting.
- **Trace is frozen and not updating** — The display is paused. Click the display once to resume. The `PAUSED` badge in the footer confirms this state.
- **WAVE tray button is not visible** — Open `View > Applet Panel` to confirm the applet panel is shown, or use `View > Reset Applet Order` to restore the default applet layout.

## Related

- [Waveform applet overview](overview.md)
- [Pause and clear the waveform display](pause-and-clear-the-waveform-display.md)
