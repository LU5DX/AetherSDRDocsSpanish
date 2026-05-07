# Ajustar la ganancia de salida posterior a la ecualización con el Output Fader

El Output Fader establece una ganancia maestra que se aplica después de todas las bandas de ecualización en la ruta de TX o RX. Úselo para compensar los cambios de nivel general introducidos por su curva de ecualización sin tocar las ganancias de bandas individuales.

## Antes de comenzar

- El editor flotante (con el título "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX") debe estar abierto. El Output Fader no está presente en el mosaico acoplado del applet.
- La etapa de ecualización correspondiente debe estar habilitada. Consulte [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md) si la etapa está actualmente desviada.

## Pasos

1. Abra el editor flotante para la ruta que desea ajustar. Haga doble clic en la etapa de EQ en el widget CHAIN del lado TX o RX.
2. Localice el Output Fader en el borde derecho de la ventana del editor. Es un fader vertical combinado con un medidor de nivel.
3. Arrastre el control deslizante del fader hacia arriba o hacia abajo para establecer la ganancia maestra posterior a la EQ. El rango válido es de -36.0 a +12.0 dB.
4. Para realizar un ajuste fino, coloque el cursor sobre el fader y gire la rueda del ratón. Cada paso de la rueda mueve la ganancia en 0.5 dB.
5. Para devolver la ganancia al valor predeterminado, haga doble clic en el control deslizante del fader. Esto restablece el valor a 0 dB.

## Función de cada control

| Control                            | Valor predeterminado                                                                                                                                                                                                                                                                                                                                                             | Rango válido                                                                                                                                                                                                                       |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Output Fader (ruta TX)             | 0 dB                                                                                                                                                                                                                                                                                                                                                                            | -36.0 a +12.0 dB                                                                                                                                                                                                                  |
| Output Fader (ruta RX)             | 0 dB                                                                                                                                                                                                                                                                                                                                                                            | -36.0 a +12.0 dB                                                                                                                                                                                                                  |
| Smoothing                          | Aplica un promediado de potencia por fracciones de octava a la traza del analizador para su visualización; no afecta los cálculos de EQ. Fracción más baja = más suavizado (1/3 es el máximo suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX.                                                                                             | Tooltip: 'Suavizado por fracciones de octava aplicado a la traza del analizador. Fracción más baja = más suavizado (1/3 = máximo, 1/96 = desactivado). Afecta solo la visualización; los cálculos de EQ no cambian.' Ubicado en la barra superior del editor (solo editor flotante). |
| Fila de iconos de tipo de filtro   | Una fila de 8 iconos personalizados (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana pico, rampa de shelving, pendiente HP/LP) en el color de la paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro para esa banda; al hacer clic también se selecciona la banda, resaltando su control en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está desviada. Implementado por ClientEqIconRow.                                                                                    |
| Fila de texto de parámetros        | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores de Frecuencia, Ganancia y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. Las etiquetas están alineadas en la parte inferior de cada columna y el fondo de la fila es transparente para no ocultar la banda de planificación de frecuencias en el lienzo superior. | Ubicado solo en el editor flotante. Implementado por ClientEqParamRow.                                                                                                                                                            |
| Líneas guía de corte del filtro (TX / RX) | Líneas amarillas discontinuas verticales superpuestas en el lienzo en los límites de corte actuales de TX bajo/alto (mosaico TX) o los bordes de la banda pasante de RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte del filtro correspondiente de la radio en tiempo real. | Arrastrar las guías de corte de TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías de RX escribe en el SliceModel activo. Pase 0 para un borde con el fin de suprimir esa guía. |

La barra de nivel detrás del control deslizante del fader muestra el nivel pico posterior a la EQ suavizado en tiempo real, usando el mismo gradiente verde-ámbar-rojo que el medidor de nivel del tubo. Este es solo un indicador visual; no responde al arrastre.

## Consejos

- Use la barra de nivel en vivo del Output Fader para confirmar que sus cambios de EQ no han llevado la salida al rojo antes de transmitir o enrutar el audio más adelante.
- Los Output Faders de TX y RX son independientes. Ajustar una ruta no afecta a la otra.
- El valor de ganancia se guarda inmediatamente. Si cierra y vuelve a abrir el editor, el fader regresa a la última posición guardada.

## Solución de problemas

- **El Output Fader no es visible** — El fader solo está presente en el editor flotante, no en el mosaico acoplado del applet "Aetherial TX EQ" o "Aetherial RX EQ". Abra el editor flotante haciendo doble clic en la etapa de EQ en el widget CHAIN.
- **El doble clic no restablece el fader** — Asegúrese de hacer doble clic directamente sobre el control deslizante del fader, no sobre el área de la barra de nivel detrás de él.
- **La fila de texto de parámetros se superpone con la banda de planificación de frecuencias** — Esto podría indicar una versión anterior del software. La versión 0.9.7 corrige un problema de diseño donde el fondo de la columna de parámetros podía filtrarse hacia arriba sobre la banda de planificación de frecuencias del lienzo. Actualice a v0.9.7 o posterior para resolverlo.

## Relacionados

- [Monitor post-EQ peak level on the Output Fader meter](monitor-post-eq-peak-level-on-the-output-fader-meter.md)
- [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md)
- [Aetherial Parametric EQ (TX / RX) overview](overview.md)
