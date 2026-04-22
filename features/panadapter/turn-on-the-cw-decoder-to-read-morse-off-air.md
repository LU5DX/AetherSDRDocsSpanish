# Activar el decodificador CW para leer Morse en el aire

El panel de decodificación CW aparece debajo del panadapter y muestra el código Morse entrante como texto en tiempo real. Úselo para copiar CW en el aire sin necesidad de escuchar ni transcribir manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel del decodificador CW requiere una conexión activa con el radio.
- El audio del PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio — la decodificación no funcionará sin entrada de audio.
- El slice vinculado a este panadapter debe estar configurado en modo CW en el radio.

## Pasos

1. Localice el panadapter correspondiente al slice que desea decodificar.
2. Haga clic derecho en el espectro o en el waterfall del panadapter para abrir el menú contextual del panadapter, luego seleccione la opción para mostrar el panel del decodificador CW. El panel de decodificación CW aparece debajo del espectro y muestra "CW" en la barra de encabezado junto con "(requires PC Audio)".
3. Sintonice el radio en la señal CW. La etiqueta de estadísticas CW se actualiza para mostrar el tono y la velocidad detectados en el formato `<hz> Hz  <wpm> WPM`.
4. Observe el área "CW decode text" para ver los caracteres decodificados. El texto aparece codificado por colores según la confianza: verde indica la mayor confianza, luego amarillo, luego naranja y finalmente rojo.
5. Ajuste el control deslizante Sens si es necesario. El valor predeterminado es 30 (rango 0–100). Muévalo hacia la derecha para rechazar decodificaciones de baja confianza; muévalo hacia la izquierda para mostrar más resultados. Su configuración se guarda como `CwDecoderSensitivity`.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango |
|---|---|---|---|
| Etiqueta de estadísticas CW | Muestra el tono y la velocidad detectados como `<hz> Hz  <wpm> WPM`. | — | — |
| Sens | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. Se guarda como `CwDecoderSensitivity`. | 30 | 0–100 |
| 🔒P (Lock Pitch) | Fija el tono del decodificador en la frecuencia sintonizada actualmente. | Off | Toggle |
| 🔒S (Lock Speed) | Fija la velocidad del decodificador en los WPM detectados actualmente. | Off | Toggle |
| Lo (pitch min) | Tono mínimo que busca el decodificador, en Hz. Limitado a ≤ Hi. | 500 Hz | 300–1200 Hz |
| Hi (pitch max) | Tono máximo que busca el decodificador, en Hz. Limitado a ≥ Lo. | 700 Hz | 300–1200 Hz |
| CW decode text | Pantalla continua de solo lectura con el texto decodificado, coloreado según la confianza. | — | — |
| CPY ALL | Copia el texto decodificado completo al portapapeles. | — | — |
| CPY VIS | Copia únicamente el texto visible actualmente en el área de desplazamiento al portapapeles. | — | — |
| CLR | Borra el búfer de decodificación CW. | — | — |
| ✕ (close CW) | Oculta el panel de decodificación CW. | — | — |

## Consejos

- El color del texto decodificado indica la confianza de la decodificación: verde significa costo < 0.15 (mayor confianza), amarillo < 0.35, naranja < 0.60, rojo ≥ 0.60.
- Si el tono de la señal se desplaza, deje 🔒P desactivado para que el decodificador pueda rastrearlo. Una vez que el tono sea estable, active 🔒P para reducir las activaciones falsas producidas por señales cercanas.
- Reduzca el rango de tono entre Lo y Hi para delimitar la señal que está copiando. Esto reduce la interferencia de otras señales dentro del pasabanda.
- Use CLR para borrar el texto acumulado antes de que comience una nueva transmisión o un contacto.

## Solución de problemas

- **No aparece texto en el panel de decodificación** — El decodificador CW requiere audio del PC. Verifique que el audio esté enrutado hacia AetherSDR. La etiqueta "(requires PC Audio)" en el encabezado del panel es un recordatorio permanente de este requisito.
- **El texto decodificado es mayormente rojo o ilegible** — Mueva el control deslizante Sens hacia 0 para aceptar más resultados, luego verifique que los límites de tono Lo y Hi encuadren el tono real de la señal. Compruebe que el modo del slice sea CW en el radio.
- **El decodificador sigue la señal incorrecta** — Active 🔒P para fijar el tono en la frecuencia de la señal objetivo. Reduzca el rango Lo–Hi para excluir los tonos de otras señales.

## Temas relacionados

- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
