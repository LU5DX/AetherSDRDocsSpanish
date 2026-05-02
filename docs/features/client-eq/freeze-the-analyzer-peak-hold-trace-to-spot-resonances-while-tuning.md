# Congelar la traza de pico máximo del analizador para identificar resonancias durante el ajuste

La traza de pico máximo marca el nivel de energía más alto observado en cada frecuencia desde el último reinicio. Congelarla detiene el decaimiento normal de ~10 dB/seg para que la traza permanezca estacionaria mientras ajusta bandas de EQ o bordes de la banda de paso — lo que facilita identificar resonancias y picos excesivos.

## Antes de comenzar

- Abra el editor flotante para el lado TX o RX del EQ. El botón `Peak Hold` se encuentra únicamente en la barra de encabezado del editor — no está disponible en el mosaico del applet acoplado. Consulte [Abrir el editor sin marcos para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).
- Asegúrese de que el audio esté pasando a través de la cadena del EQ para que el analizador FFT en vivo esté activo y la traza de pico máximo esté acumulando datos.

## Pasos

1. Abra el editor flotante del lado que desea inspeccionar (TX o RX) haciendo doble clic en la etapa de EQ en el widget CHAIN.
2. Deje correr el audio durante algunos segundos para que la traza de pico máximo se acumule en todo el rango de frecuencias.
3. Haga clic en `Peak Hold` en la barra de encabezado del editor. El botón se torna ámbar para confirmar que está activado.
4. Ajuste sus bandas de EQ, cortes de filtro u otras configuraciones mientras observa la traza congelada. La traza permanece estacionaria independientemente del nivel de señal actual.
5. Haga clic en `Peak Hold` nuevamente para desactivarlo. La traza reanuda el decaimiento normal (~10 dB/seg).

## Qué hace cada control

| Control | Ubicación | Predeterminado | Comportamiento | Clave persistida |
|---|---|---|---|---|
| `Peak Hold` | Barra de encabezado del editor | Desactivado | Cuando está activado, congela la traza de pico máximo por bin en el nivel más alto observado en cada frecuencia. No ocurre decaimiento hasta que se desactiva. Fondo ámbar cuando está activado. | — (no se persiste) |
| `Smoothing` | Barra de encabezado del editor | `Off (1/96)` | Promediado de potencia por fracción de octava aplicado únicamente a la visualización del analizador. Opciones: `Off (1/96)`, `1/24`, `1/12`, `1/6`, `1/3`. Menor fracción = más suavizado. No afecta los bins de la traza de pico máximo ni el cálculo del EQ. | `ClientEqSmoothingFraction` |

## Consejos

- La traza de pico máximo rastrea los bins de frecuencia sin procesar incluso cuando el suavizado de visualización (combo `Smoothing`) está configurado en un valor grueso como `1/3`. Si una resonancia aparece en la traza congelada pero se ve redondeada con un suavizado grueso, cambie `Smoothing` a `Off (1/96)` para ver el detalle completo a nivel de bin.
- Para limpiar los datos de pico acumulados sin desactivar y reactivar `Peak Hold`, desactive y vuelva a activar inmediatamente el botón tras un momento de silencio o señal reducida.
- Las líneas guía de corte de filtro amarillas discontinuas permanecen desplazables mientras `Peak Hold` está activo. Esto le permite alinear los bordes de la banda de paso del radio directamente con las características visibles en la traza congelada.

## Solución de problemas

- **El botón `Peak Hold` no es visible** — El botón se encuentra únicamente en el editor flotante, no en el mosaico del applet acoplado `Aetherial TX EQ` o `Aetherial RX EQ`. Abra el editor flotante haciendo doble clic en la etapa de EQ en el widget CHAIN.
- **La traza decae inmediatamente después de hacer clic en `Peak Hold`** — Confirme que el botón muestra un fondo ámbar, lo cual indica que está activado. Un solo clic que se registre como doble clic puede desactivar el botón nuevamente. Haga clic una vez firmemente y verifique el estado ámbar.

## Relacionados

- [Abrir el editor sin marcos para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Suavizar la visualización del analizador para una lectura más fácil con el combo Smoothing](smooth-the-analyzer-display-for-easier-reading-with-the-smoothing-combo.md)
- [Arrastrar la línea guía de corte de filtro TX o RX para mover la banda de paso del radio](drag-the-tx-or-rx-filter-cutoff-guide-line-to-move-the-radio-passband.md)
- [Inspeccionar la curva de EQ TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
