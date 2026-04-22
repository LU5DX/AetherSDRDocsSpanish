# Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es estable

Una vez que el decodificador CW ha enganchado una señal y produce una copia limpia, puede congelar el tono, la velocidad o ambos para que el decodificador deje de buscar y se mantenga en el objetivo.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y activo. Consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- La etiqueta de estadísticas CW debe mostrar una lectura estable — por ejemplo, `600 Hz  20 WPM` — antes de bloquear.
- El audio de la PC debe estar enrutado hacia AetherSDR; sin él, el decodificador no produce ninguna salida sobre la cual bloquear.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que las lecturas de Hz y WPM se estabilicen.
2. Para congelar el tono, haga clic en 🔒P en el panel de decodificación CW. El botón se resalta cuando está activo.
3. Para congelar la velocidad, haga clic en 🔒S. El botón se resalta cuando está activo.
4. Para desbloquear, haga clic en el mismo botón nuevamente. El resaltado desaparece y el decodificador reanuda el seguimiento.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Etiqueta de estadísticas CW | Muestra el tono y la velocidad detectados actualmente como `<hz> Hz  <wpm> WPM`. | — | — | — |
| 🔒P (Lock Pitch) | Bloquea el tono del decodificador en la frecuencia mostrada en la etiqueta de estadísticas CW. Presione nuevamente para desbloquear. | Off | On / Off | — |
| 🔒S (Lock Speed) | Bloquea la velocidad del decodificador en el WPM mostrado en la etiqueta de estadísticas CW. Presione nuevamente para desbloquear. | Off | On / Off | — |
| Lo (tono mínimo) | Establece el tono mínimo que el decodificador busca antes de que se establezca un bloqueo. Limitado a ≤ Hi. | 500 Hz | 300–1200 Hz | — |
| Hi (tono máximo) | Establece el tono máximo que el decodificador busca antes de que se establezca un bloqueo. Limitado a ≥ Lo. | 700 Hz | 300–1200 Hz | — |
| Sens | Filtra las decodificaciones de baja confianza. Valores más altos son más estrictos. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- Acerque Lo y Hi al tono real de la señal antes de bloquear. Si la señal está en 600 Hz, fijar Lo en 550 y Hi en 650 le da al decodificador menos margen para desviarse antes de hacer clic en 🔒P.
- Puede bloquear el tono y la velocidad de forma independiente. Bloquear solo la velocidad es útil en una red donde varias estaciones transmiten a la misma velocidad pero en frecuencias ligeramente diferentes.
- Si la copia se deteriora después de bloquear, es posible que el operador haya cambiado el tono o la velocidad. Desbloquee, deje que el decodificador vuelva a rastrear y bloquee nuevamente.

## Solución de problemas

- **La etiqueta de estadísticas CW no muestra ninguna lectura** — El decodificador no ha detectado una señal. Verifique que el audio de la PC esté enrutado correctamente y que la señal esté dentro del rango de tonos Lo–Hi.
- **🔒P o 🔒S no tiene ningún efecto visible en el texto** — La etiqueta de estadísticas no estaba estable en el momento del bloqueo. Desbloquee, espere a que la lectura se estabilice y bloquee nuevamente.
- **La calidad del texto decodificado cae inmediatamente después de bloquear la velocidad** — La lectura de WPM en el momento del bloqueo aún estaba convergiendo. Desbloquee y espere una lectura más estable antes de bloquear nuevamente.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
