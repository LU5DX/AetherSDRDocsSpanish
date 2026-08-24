# Ajuste la ganancia de salida posterior al EQ con el Output Fader

El Output Fader establece una ganancia maestra aplicada después de todas las bandas de EQ en la ruta de TX o RX. Úselo para compensar cambios de nivel generales introducidos por su curva de EQ sin tocar las ganancias de bandas individuales.

## Antes de comenzar

- El editor flotante (titulado "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX") debe estar abierto. El Output Fader no está presente en el mosaico de la applet acoplada.
- La etapa de EQ correspondiente debe estar habilitada. Consulte [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md) si la etapa está actualmente en bypass.

## Pasos

1. Abra el editor flotante para la ruta que desea ajustar. Haga doble clic en la etapa de EQ en el widget CHAIN en el lado de TX o RX.
2. Localice el Output Fader en el borde derecho de la ventana del editor. Es un fader vertical combinado con un medidor de nivel.
3. Arrastre el control del fader hacia arriba o hacia abajo para establecer la ganancia maestra posterior al EQ. El rango válido es de -36.0 a +12.0 dB.
4. Para hacer un ajuste fino, coloque el cursor sobre el fader y gire la rueda del ratón. Cada paso de la rueda mueve la ganancia en 0.5 dB.
5. Para devolver la ganancia al valor predeterminado, haga doble clic en el control del fader. Esto restablece el valor a 0 dB.
6. Para escribir un valor dB preciso, haga clic en la lectura numérica en la parte inferior del fader. La lectura cambia a un editor en línea que muestra el número desnudo. Escriba el valor deseado (por ejemplo, `-6.2` o `+3.5`) y luego presione Enter o haga clic en otro lugar para confirmar. Si presiona Escape, la edición se cancela y se restaura el valor anterior.

## Qué hace cada control

| Control                             | Predeterminado                                                                                                                                                                                                                                                                                                                                                                         | Rango válido                                                                                                                                                                                                                               |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Output Fader (ruta TX)              | 0 dB                                                                                                                                                                                                                                                                                                                                                                            | -36.0 a +12.0 dB                                                                                                                                                                                                                         |
| Output Fader (ruta RX)              | 0 dB                                                                                                                                                                                                                                                                                                                                                                            | -36.0 a +12.0 dB                                                                                                                                                                                                                         |
| Smoothing                           | Off (1/96). Aplica promediado de potencia de fracción de octava a la traza del analizador para visualización — no afecta el cálculo de EQ. Fracción más baja = más suavizado (1/3 es el más suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores de TX y RX.                                                                                                                                                 | Off (1/96)                                                                                                                                                                                                                                |
| Peak Hold                           | Botón de conmutación, desmarcado. Cuando está marcado, la traza de retención de pico por bin en el analizador deja de decaer — el nivel más alto observado de cada frecuencia se mantiene hasta que el botón se desmarca. Fondo ámbar cuando está marcado.                                                                                                                                                           | Ubicado en la franja de encabezado del editor (solo editor flotante).                                                                                                                                                                                |
| Filter family                       | Butterworth. Selecciona la matemática de cascada HP/LP. Butterworth = banda de paso máximamente plana; Chebyshev = caída más pronunciada con ondulación de banda de paso de 1 dB; Bessel = fase lineal / caída más suave; Elliptic = transición más pronunciada con ondulación en ambas bandas. Aplica solo a tipos de filtro HP y LP; las bandas de pico y estante usan su propia topología fija de segundo orden independientemente.            | Butterworth                                                                                                                                                                                                                               |
| Reset                               | Botón pulsador. Restablece todas las bandas a la plantilla predeterminada de 10 bandas (ClientEq::defaultBand), restaura el número predeterminado de bandas y restablece la familia de filtros a Butterworth. Guarda inmediatamente. Información sobre herramientas: 'Reset all bands to default values'.                                                                                                                                           | Ubicado en la franja de encabezado del editor (solo editor flotante).                                                                                                                                                                                |
| Fila de iconos de tipo de filtro    | Una fila de 8 iconos dibujados personalizados (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma actual del filtro (campana de pico, rampa de estante, pendiente HP/LP) en el color de paleta de su banda. Haga clic en un icono para alternar los tipos de filtro para esa banda; el clic también selecciona la banda, resaltando su control en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está en bypass. Implementado por ClientEqIconRow.                                                                                                                 |
| Fila de texto de parámetros         | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores Freq, Gain y Q de cada banda. Los valores se actualizan en vivo durante los arrastres del lienzo. Hacer clic en una columna selecciona esa banda. Las etiquetas están alineadas en la parte inferior de cada columna y el fondo de la fila es transparente para no oscurecer la franja de plan de bandas en el lienzo superior.                                      | Ubicado solo en el editor flotante. Implementado por ClientEqParamRow. Confirmado mediante menú de clic derecho o tecla Enter.                                                                                                                        |
| Líneas guía de corte de filtro (TX / RX) | Líneas verticales amarillas discontinuas superpuestas en el lienzo en los cortes de filtro bajo/alto actuales de TX (mosaico TX) o los bordes de banda de paso de RX (mosaico RX) de la radio. Pasar el cursor cerca de una línea cambia el cursor a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real.                                                                  | Arrastrar las guías de corte de TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías de RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía.                      |
| Editor de valor del Output Fader    | Muestra el valor actual de ganancia en dB. Haga clic para activar la edición en línea. Escriba un valor numérico (por ejemplo, `-6.2` o `+3.5`) y presione Enter para confirmar. Presione Escape para cancelar la edición. Los valores fuera del rango válido se limitan.                                                                                                                                              | -36.0 a +12.0 dB                                                                                                                                                                                                                         |
| Ref (superposición de curva de referencia) | Superpone una de varias curvas de respuesta de frecuencia objetivo en el lienzo de EQ como una línea ámbar delgada, como guía visual mientras ajusta las bandas. Incluye el objetivo de inteligibilidad de AT&T 1959 Bell Labs más respuestas digitalizadas de micrófonos SSB famosos (Astatic D-104, Shure 444, Heil HC-5) y un preajuste DX agresivo de Bob-Heil.                                                   | Solo visualización — la superposición no afecta el cálculo de EQ. Persistido globalmente (preferencia de usuario única compartida entre editores de RX y TX). Ubicado en la franja de encabezado del editor flotante y el panel de EQ de la franja de canal, no en el mosaico de la applet acoplada. |

La barra de nivel detrás del control del fader muestra el nivel de pico posterior al EQ suavizado en tiempo real, usando el mismo gradiente verde-ámbar-rojo que el medidor de nivel del Tube. Es solo un indicador de visualización; no responde al arrastre.

## Superposición de curva de referencia

Se puede superponer una curva de referencia en el lienzo de EQ para proporcionar un objetivo visual al dar forma a su EQ paramétrico. La superposición se dibuja como una curva ámbar semitransparente detrás de las curvas de sus bandas de EQ.

### Preajustes de referencia disponibles

| Preset          | Fuente                                                                                                                                 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| AT&T 1959       | Respuesta de frecuencia de transmisión "óptima para el habla" de AT&T 1959 — objetivo canónico de pico de presencia de Bell Labs. Pico de +5 dB a 2.5 kHz.      |
| Heil DX         | Recomendación publicada de Bob Heil para máxima potencia de habla en pile-ups. Pico más pronunciado de +6 dB a 2.7 kHz.                                                             |
| Astatic D-104   | Respuesta clásica de micrófono de cristal "lollipop" AM/SSB. Pico de presencia extremo alrededor de 3 kHz.                                             |
| Shure 444       | Micrófono de escritorio clásico estilo radiodifusión. Respuesta más amplia con refuerzo de presencia más suave.                                                        |
| Heil HC-5       | Forma objetivo de micrófono SSB dinámico moderno. El refuerzo de presencia media alcanza su pico ~3 kHz a +5 dB.                                                        |

### Para seleccionar una curva de referencia

1. Abra el editor flotante para la ruta que desea ajustar.
2. Localice el selector **Reference curve** en la franja de encabezado del editor.
3. Haga clic en el selector y elija un preajuste de la lista. La curva aparece inmediatamente en el lienzo.
4. Para eliminar la curva de referencia, seleccione **Off** en el mismo selector.

El ID de la curva de referencia se persiste por separado por ruta (`ClientEqTxReferenceCurve` / `ClientEqRxReferenceCurve`).

## Consejos

- Use la barra de nivel en vivo del Output Fader para confirmar que sus cambios de EQ no han empujado la salida al rojo antes de transmitir o enrutar audio más adelante.
- Los Output Faders de TX y RX son independientes. Ajustar una ruta no afecta la otra.
- El valor de ganancia se persiste inmediatamente. Si cierra y vuelve a abrir el editor, el fader regresa a la última posición guardada.
- Haga clic derecho en una columna de parámetros en la fila de texto de parámetros para editar numéricamente los valores de esa banda. Presione Enter para confirmar la edición; la configuración de EQ se guarda inmediatamente.
- La visualización del analizador usa caché para mantener la representación receptiva. Para tamaños de lienzo muy grandes (por ejemplo, dimensiones de lienzo que excedan aproximadamente 32 MB de datos de píxeles a la relación de píxeles de su pantalla), la caché se omite y el lienzo se dibuja directamente, lo que preserva la fidelidad. Esto es automático y no requiere acción.

## Solución de problemas

- **El Output Fader no es visible** — El fader solo está presente en el editor flotante, no en el mosaico de la applet acoplada "Aetherial TX EQ" o "Aetherial RX EQ". Abra el editor flotante haciendo doble clic en la etapa de EQ en el widget CHAIN.
- **El doble clic no restablece el fader** — Asegúrese de hacer doble clic directamente en el control del fader, no en el área de la barra de nivel detrás de él.
- **La edición de valor en línea no acepta mi entrada** — El editor acepta números decimales con un prefijo de signo opcional. Si su configuración regional usa coma como separador decimal, el editor aceptará comas. Los valores fuera del rango válido (-36 a +12 dB) se limitan al valor válido más cercano.
- **La fila de texto de parámetros se superpone a la franja de plan de bandas** — Esto podría indicar una versión anterior del software. La versión 0.9.7 corrige un problema de diseño donde el fondo de la columna de parámetros podía sangrar hacia arriba sobre la franja de plan de bandas del lienzo. Actualice a v0.9.7 o posterior para resolverlo.

## Relacionado

- [Monitor post-EQ peak level on the Output Fader meter](monitor-post-eq-peak-level-on-the-output-fader-meter.md)
- [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md)
- [Aetherial Parametric EQ (TX / RX) overview](overview.md)
