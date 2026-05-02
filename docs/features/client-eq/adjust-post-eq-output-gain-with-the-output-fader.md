# Ajustar la ganancia de salida post-EQ con el Output Fader

El Output Fader establece una ganancia maestra aplicada después de todas las bandas de EQ, tanto en la ruta TX como en la RX. Úselo para compensar los cambios de nivel general introducidos por su curva de EQ sin modificar las ganancias individuales de cada banda.

## Antes de comenzar

- El editor flotante (titulado "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX") debe estar abierto. El Output Fader no está disponible en el applet acoplado.
- La etapa de EQ correspondiente debe estar habilitada. Consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md) si la etapa está desactivada actualmente.

## Pasos

1. Abra el editor flotante para la ruta que desea ajustar. Haga doble clic en la etapa de EQ en el widget CHAIN del lado TX o RX.
2. Localice el Output Fader en el borde derecho de la ventana del editor. Es un fader vertical combinado con medidor de nivel.
3. Arrastre el control del fader hacia arriba o hacia abajo para establecer la ganancia maestra post-EQ. El rango válido es de -36.0 a +12.0 dB.
4. Para realizar un ajuste fino, coloque el cursor sobre el fader y desplace la rueda del ratón. Cada paso de desplazamiento mueve la ganancia 0.5 dB.
5. Para restablecer la ganancia al valor predeterminado, haga doble clic en el control del fader. Esto restablece el valor a 0 dB.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Output Fader (ruta TX) | 0 dB | -36.0 a +12.0 dB | `ClientEqTxMasterGain` |
| Output Fader (ruta RX) | 0 dB | -36.0 a +12.0 dB | `ClientEqRxMasterGain` |

La barra de nivel detrás del control del fader muestra el nivel de pico post-EQ suavizado en tiempo real, usando el mismo gradiente verde-ámbar-rojo que el medidor de nivel Tube. Es solo un indicador visual; no responde al arrastre.

## Consejos

- Use la barra de nivel en vivo del Output Fader para confirmar que sus cambios de EQ no han llevado la salida al rojo antes de transmitir o enrutar el audio más adelante.
- Los Output Faders de TX y RX son independientes. Ajustar una ruta no afecta a la otra.
- El valor de ganancia se guarda de inmediato. Si cierra y vuelve a abrir el editor, el fader regresa a la última posición guardada.

## Resolución de problemas

- **El Output Fader no es visible** — El fader solo está presente en el editor flotante, no en el applet acoplado "Aetherial TX EQ" o "Aetherial RX EQ". Abra el editor flotante haciendo doble clic en la etapa de EQ en el widget CHAIN.
- **El doble clic no restablece el fader** — Asegúrese de hacer doble clic directamente sobre el control del fader, no sobre la barra de nivel detrás de él.

## Relacionados

- [Monitorear el nivel de pico post-EQ en el medidor del Output Fader](monitor-post-eq-peak-level-on-the-output-fader-meter.md)
- [Abrir el editor sin marco para agregar, quitar o ajustar bandas en cualquier ruta](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Descripción general del Aetherial Parametric EQ (TX / RX)](overview.md)
