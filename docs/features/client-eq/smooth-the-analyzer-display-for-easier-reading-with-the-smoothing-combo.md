# Suavice la visualización del analizador para facilitar la lectura con el combo Smoothing

El combo Smoothing aplica promediado de potencia por octava fraccionaria a la traza en vivo del analizador FFT en el editor Aetherial Parametric EQ. Úselo para reducir el jitter de la traza y hacer que las tendencias generales de respuesta sean más fáciles de leer mientras ajusta. El ajuste afecta únicamente a la visualización — el cálculo del EQ no cambia.

## Antes de comenzar

- El editor flotante debe estar abierto. Haga doble clic en la etapa EQ del widget CHAIN (lado TX o RX) para abrirlo. El editor se titula "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
- El combo Smoothing se encuentra en la barra de encabezado del editor. No está disponible en el mosaico del applet acoplado.

## Pasos

1. Abra el editor flotante para la etapa EQ TX o RX haciendo doble clic en la etapa EQ correspondiente en el widget CHAIN.
2. Localice la etiqueta "Smoothing:" en la barra de encabezado del editor.
3. Haga clic en el cuadro combinado a la derecha de la etiqueta "Smoothing:".
4. Seleccione un nivel de suavizado de la lista:
   - `Off (1/96)` — sin suavizado efectivo (valor predeterminado)
   - `1/24` — suavizado leve
   - `1/12` — suavizado moderado
   - `1/6` — suavizado mayor
   - `1/3` — máximo suavizado
5. La traza del analizador se actualiza de inmediato.

## Qué hace cada control

| Control | Predeterminado | Valores válidos | Ajuste guardado |
|---|---|---|---|
| Smoothing | `Off (1/96)` | `Off (1/96)` / `1/24` / `1/12` / `1/6` / `1/3` | `ClientEqSmoothingFraction` |

**Smoothing** — Aplica promediado de potencia por octava fraccionaria a la traza del analizador. Los valores de fracción más bajos producen una traza más suave: `1/3` es el máximo suavizado; `Off (1/96)` es efectivamente sin suavizado. El ajuste se comparte entre los editores TX y RX — cambiarlo en un editor también afecta al otro. El cálculo del EQ y la traza de retención de pico no se ven afectados.

## Consejos

- La traza de retención de pico rastrea los bins sin procesar independientemente del ajuste de suavizado. Si desea ver simultáneamente la tendencia suavizada y los picos sin procesar, active Peak Hold mientras el suavizado está activo.
- El suavizado `1/6` o `1/3` es útil para comparar su curva de EQ con la forma general del relleno del analizador sin que el ruido a nivel de bin fino oscurezca la comparación.

## Solución de problemas

- **El combo Smoothing no es visible** — El combo solo está presente en el editor flotante, no en el mosaico del applet acoplado "Aetherial TX EQ" o "Aetherial RX EQ". Abra el editor haciendo doble clic en la etapa EQ en el widget CHAIN.
- **Cambiar el suavizado en el editor TX también cambia el editor RX** — Esto es esperado. `ClientEqSmoothingFraction` es una preferencia global única compartida entre ambos editores.

## Relacionado

- [Congele la traza de retención de pico del analizador para detectar resonancias durante el ajuste](freeze-the-analyzer-peak-hold-trace-to-spot-resonances-while-tuning.md)
- [Abra el editor sin marco para agregar, eliminar o ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspeccione la curva de EQ TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccione la curva de EQ RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
