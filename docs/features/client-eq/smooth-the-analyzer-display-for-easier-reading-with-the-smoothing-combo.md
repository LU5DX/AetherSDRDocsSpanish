# Suavizar la visualización del analizador para una lectura más fácil con el combo de suavizado

El combo de suavizado aplica un promediado de potencia de octava fraccional a la traza en vivo del analizador FFT en el editor de ecualización paramétrica Aetherial. Úselo para reducir la vibración de la traza y hacer que las tendencias amplias de respuesta sean más fáciles de leer mientras ajusta. La configuración afecta solo a la visualización — los cálculos del ecualizador no se modifican.

## Antes de comenzar

- El editor flotante debe estar abierto. Haga doble clic en la etapa EQ en el widget CHAIN (lado TX o RX) para abrirlo. El editor se titula "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
- El combo de suavizado se encuentra en la barra de encabezado del editor. No está disponible en el mosaico acoplado del applet.

## Pasos

1. Abra el editor flotante para la etapa EQ de TX o RX haciendo doble clic en la etapa EQ correspondiente en el widget CHAIN.
2. Localice la etiqueta "Smoothing:" en la barra de encabezado del editor.
3. Haga clic en el cuadro combinado a la derecha de la etiqueta "Smoothing:".
4. Seleccione un nivel de suavizado de la lista:
   - `Off (1/96)` — sin suavizado efectivo (predeterminado)
   - `1/24` — suavizado ligero
   - `1/12` — suavizado moderado
   - `1/6` — suavizado más intenso
   - `1/3` — el más suavizado
5. La traza del analizador se actualiza inmediatamente.

## Qué hace cada control

| Control                           | Predeterminado                                                                                                                                                                                                                                                                                                                                                               | Valores válidos                                                                                                                                                                                                     |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Smoothing                         | `Off (1/96)`                                                                                                                                                                                                                                                                                                                                                                 | `Off (1/96)` / `1/24` / `1/12` / `1/6` / `1/3`                                                                                                                                                                      |
| Fila de iconos de tipo de filtro  | Una fila de 8 iconos pintados personalizados (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma actual del filtro (campana de pico, rampa de estante, pendiente HP/LP) en el color de la paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro para esa banda; al hacer clic también se selecciona la banda, resaltando su control en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está desactivada. Implementado por ClientEqIconRow.                                                                 |
| Fila de texto de parámetros       | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores de Frecuencia, Ganancia y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. Las etiquetas están alineadas en la parte inferior de cada columna y el fondo de la fila es transparente para no ocultar la tira de bandas sobre la fila. | Ubicado solo en el editor flotante. Implementado por ClientEqParamRow.                                                                                                                                              |
| Líneas guía de corte del filtro (TX / RX) | Líneas verticales amarillas discontinuas superpuestas en el lienzo en los cortes de filtro bajo/alto actuales de la radio (mosaico TX) o en los bordes de la banda de paso de RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real. | Arrastrar las guías de corte TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía. |

**Smoothing** — Aplica un promediado de potencia de octava fraccional a la traza del analizador. Los valores de fracción más bajos producen una traza más suave: `1/3` es el más suavizado; `Off (1/96)` no está suavizado de forma efectiva. La configuración se comparte entre los editores TX y RX — cambiarla en un editor también afecta al otro. Los cálculos del ecualizador y la traza de retención de pico no se ven afectados.

## Consejos

- La traza de retención de pico rastrea los bins sin procesar independientemente de la configuración de suavizado. Si desea ver tanto la tendencia suavizada como los picos sin procesar simultáneamente, active Peak Hold mientras el suavizado está activo.
- El suavizado `1/6` o `1/3` es útil para comparar su curva de ecualización con la forma amplia del relleno del analizador sin que el ruido fino a nivel de bin obstruya la comparación.

## Solución de problemas

- **El combo de suavizado no es visible** — El combo solo está presente en el editor flotante, no en el mosaico acoplado del applet "Aetherial TX EQ" o "Aetherial RX EQ". Abra el editor haciendo doble clic en la etapa EQ en el widget CHAIN.
- **Cambiar el suavizado en el editor TX también cambia el editor RX** — Esto es esperado. `ClientEqSmoothingFraction` es una única preferencia global compartida entre ambos editores.
- **La fila de texto de parámetros se superpone con la tira de bandas** — Esto era un defecto de visualización en versiones anteriores a v0.9.7 donde el fondo oscuro de la fila de parámetros se filtraba hacia arriba sobre la tira de bandas del lienzo. Si ve esto, actualice a v0.9.7 o posterior.

## Relacionado

- [Freeze the analyzer peak-hold trace to spot resonances while tuning](freeze-the-analyzer-peak-hold-trace-to-spot-resonances-while-tuning.md)
- [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspect the TX EQ curve and live spectrum](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspect the RX EQ curve and live spectrum](inspect-the-rx-eq-curve-and-live-spectrum.md)
