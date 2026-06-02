# Ajustar la ganancia de salida posterior a la EQ con el Fader de Salida

El Fader de Salida establece una ganancia maestra aplicada después de todas las bandas de ecualización en la ruta TX o RX. Úselo para compensar cambios de nivel general introducidos por su curva de EQ sin modificar las ganancias de bandas individuales.

## Antes de comenzar

- El editor flotante (titulado "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX") debe estar abierto. El Fader de Salida no está presente en el mosaico acoplado del applet.
- La etapa de EQ correspondiente debe estar habilitada. Consulte [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md) si la etapa está actualmente desviada.

## Pasos

1. Abra el editor flotante para la ruta que desea ajustar. Haga doble clic en la etapa de EQ en el widget CHAIN del lado TX o RX.
2. Localice el Fader de Salida en el borde derecho de la ventana del editor. Es un fader vertical combinado con un medidor de nivel.
3. Arrastre el control del fader hacia arriba o hacia abajo para establecer la ganancia maestra posterior a la EQ. El rango válido es de -36.0 a +12.0 dB.
4. Para realizar un ajuste fino, coloque el cursor sobre el fader y gire la rueda del ratón. Cada paso de la rueda mueve la ganancia en 0.5 dB.
5. Para devolver la ganancia al valor predeterminado, haga doble clic en el control del fader. Esto restablece el valor a 0 dB.
6. Para escribir un valor de dB preciso, haga clic en el indicador numérico en la parte inferior del fader. El indicador cambia a un editor en línea que muestra solo el número. Escriba el valor deseado (por ejemplo, `-6.2` o `+3.5`) y luego presione Enter o haga clic en otro lugar para confirmar. Si presiona Escape, la edición se cancela y se restaura el valor anterior.

## Función de cada control

| Control                             | Predeterminado                                                                                                                                                                                                                                                                                                                                                                         | Rango válido                                                                                                                                                                                                                      |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fader de Salida (ruta TX)           | 0 dB                                                                                                                                                                                                                                                                                                                                                                                   | -36.0 a +12.0 dB                                                                                                                                                                                                                  |
| Fader de Salida (ruta RX)           | 0 dB                                                                                                                                                                                                                                                                                                                                                                                   | -36.0 a +12.0 dB                                                                                                                                                                                                                  |
| Suavizado                           | Desactivado (1/96). Aplica promediado de potencia en fracciones de octava a la traza del analizador para visualización — no afecta los cálculos de EQ. Fracción menor = traza más suave (1/3 es el más suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX.                                                                                          | Desactivado (1/96) \| 1/24 \| 1/12 \| 1/6 \| 1/3                                                                                                                                                                                                                                                |
| Retención de pico                   | Botón de alternancia, sin marcar. Cuando está marcado, la traza de retención de pico por bin en el analizador deja de decaer — el nivel más alto observado de cada frecuencia se mantiene hasta que el botón se desactive. Fondo ámbar cuando está marcado.                                                                                                                               | Ubicado en la franja del encabezado del editor (solo editor flotante).                                                                                                                                                            |
| Familia de filtros                  | Butterworth. Selecciona las matemáticas de la cascada HP/LP. Butterworth = banda de paso máximamente plana; Chebyshev = pendiente más pronunciada con 1 dB de ondulación en la banda de paso; Bessel = fase lineal / pendiente más suave; Elíptico = transición más abrupta con ondulación en ambas bandas. Se aplica solo a los tipos de filtro HP y LP; las bandas de pico y estante usan su propia topología fija de segundo orden independientemente. | Butterworth \| Chebyshev \| Bessel \| Elíptico                                                                                                                                                                                                                                                   |
| Restablecer                         | Botón pulsador. Restablece todas las bandas a la plantilla predeterminada de 10 bandas (ClientEq::defaultBand), restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Se guarda inmediatamente. Información sobre herramientas: 'Reset all bands to default values'.                                                                             | Ubicado en la franja del encabezado del editor (solo editor flotante).                                                                                                                                                            |
| Fila de iconos de tipo de filtro    | Una fila de 8 iconos dibujados personalizados (uno por espacio de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana de pico, rampa de estante, pendiente HP/LP) en el color de la paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro para esa banda; al hacer clic también se selecciona la banda, resaltando su control en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está desviada. Implementado por ClientEqIconRow.                                                                                   |
| Fila de texto de parámetros         | Una fila de 8 columnas de texto (una por espacio de banda) debajo del lienzo que muestra los valores de Frecuencia, Ganancia y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Haga clic en una columna para seleccionar esa banda. Las etiquetas están alineadas en la parte inferior dentro de cada columna y el fondo de la fila es transparente para que no oculte la tira de plan de bandas en el lienzo superior. | Ubicado solo en el editor flotante. Implementado por ClientEqParamRow. Confirmado mediante menú contextual o tecla Enter.                                                                                                         |
| Líneas guía de corte de filtro (TX/RX) | Líneas amarillas discontinuas verticales superpuestas en el lienzo en los límites de filtro de corte bajo/alto TX actuales de la radio (mosaico TX) o en los bordes de la banda de paso RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real. | Arrastrar las guías de corte TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 para un borde a fin de suprimir esa guía.          |
| Editor de valor del Fader de Salida | Muestra el valor de ganancia actual en dB. Haga clic para activar la edición en línea. Escriba un valor numérico (por ejemplo, `-6.2` o `+3.5`) y presione Enter para confirmar. Presione Escape para cancelar la edición. Los valores fuera del rango válido se limitan.                                                                                                               | -36.0 a +12.0 dB                                                                                                                                                                                                                  |

La barra de nivel detrás del control del fader muestra el nivel pico posterior a la EQ suavizado en tiempo real, utilizando el mismo gradiente verde-ámbar-rojo que el medidor de nivel del Tubo. Esto es solo un indicador visual; no responde al arrastre.

## Superposición de curva de referencia

Se puede superponer una curva de referencia en el lienzo de EQ para proporcionar un objetivo visual al dar forma a su EQ paramétrica. La superposición se dibuja como una curva ámbar semitransparente detrás de sus curvas de banda de EQ.

### Preajustes de referencia disponibles

| Preajuste       | Fuente                                                                                                                              |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------|
| AT&T 1959       | AT&T 1959 "respuesta de frecuencia de transmisión óptima para voz" — objetivo canónico de pico de presencia de Bell Labs. Pico +5 dB a 2.5 kHz. |
| Heil DX         | Recomendación publicada de Bob Heil para máxima potencia de habla en acumulaciones. Pico más agudo de +6 dB a 2.7 kHz.              |
| Astatic D-104   | Respuesta clásica del micrófono de cristal "lollipop" para AM/SSB. Pico de presencia extremo alrededor de 3 kHz.                    |
| Shure 444       | Micrófono de escritorio clásico de estilo transmisión. Respuesta más amplia con realce de presencia más suave.                      |
| Heil HC-5       | Forma objetivo para micrófono dinámico de SSB moderno. El realce de presencia medio alcanza un pico ~3 kHz a +5 dB.                 |

### Para seleccionar una curva de referencia

1. Abra el editor flotante para la ruta que desea ajustar.
2. Localice el selector **Reference curve** en la franja del encabezado del editor.
3. Haga clic en el selector y elija un preajuste de la lista. La curva aparece inmediatamente en el lienzo.
4. Para eliminar la curva de referencia, seleccione **Off** en el mismo selector.

El ID de la curva de referencia se conserva por separado para cada ruta (`ClientEqTxReferenceCurve` / `ClientEqRxReferenceCurve`).

## Consejos

- Use la barra de nivel en vivo del Fader de Salida para confirmar que sus cambios de EQ no han llevado la salida a la zona roja antes de transmitir o enrutar el audio más adelante.
- Los Faders de Salida TX y RX son independientes. Ajustar una ruta no afecta a la otra.
- El valor de ganancia se guarda inmediatamente. Si cierra y vuelve a abrir el editor, el fader vuelve a la última posición guardada.
- Haga clic derecho en una columna de parámetros en la fila de texto de parámetros para editar los valores de esa banda numéricamente. Presione Enter para confirmar la edición; la configuración de EQ se guarda inmediatamente.

## Solución de problemas

- **El Fader de Salida no es visible** — El fader solo está presente en el editor flotante, no en el mosaico acoplado del applet "Aetherial TX EQ" o "Aetherial RX EQ". Abra el editor flotante haciendo doble clic en la etapa de EQ en el widget CHAIN.
- **El doble clic no restablece el fader** — Asegúrese de hacer doble clic directamente en el control del fader, no en el área de la barra de nivel detrás de él.
- **La edición en línea del valor no acepta mi entrada** — El editor acepta números decimales con un signo opcional al inicio. Si su configuración regional usa una coma como separador decimal, el editor aceptará comas. Los valores fuera del rango válido (-36 a +12 dB) se limitan al valor válido más cercano.
- **La fila de texto de parámetros se superpone con la tira de plan de bandas** — Esto podría indicar una versión anterior del software. La versión 0.9.7 corrige un problema de diseño donde el fondo de la columna de parámetros podía sangrar hacia arriba sobre la tira de plan de bandas del lienzo. Actualice a v0.9.7 o posterior para resolverlo.

## Relacionados

- [Monitor post-EQ peak level on the Output Fader meter](monitor-post-eq-peak-level-on-the-output-fader-meter.md)
- [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md)
- [Aetherial Parametric EQ (TX / RX) overview](overview.md)
