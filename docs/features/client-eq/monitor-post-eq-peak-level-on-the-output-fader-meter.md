# Monitorear el nivel de pico post-EQ en el medidor del Output Fader

El Output Fader en el editor de EQ flotante muestra un medidor de nivel de pico post-EQ en tiempo real detrás de su control deslizante, lo que permite ver cuánto margen dinámico queda después de aplicar la curva de EQ y el ajuste de ganancia maestra.

## Antes de comenzar

- El editor de EQ flotante debe estar abierto para la ruta que desea monitorear (TX o RX). El Output Fader no está disponible en el panel de applet acoplado.
- La etapa de EQ debe estar habilitada. Si la etapa está en bypass, el medidor sigue reflejando la señal que pasa a través de ella, pero la curva de EQ no tiene efecto.

## Pasos

1. Abra el editor flotante para la ruta que desea monitorear. Haga doble clic en la etapa de EQ correspondiente en el widget CHAIN — ya sea el lado TX o RX — para abrir el editor titulado "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice el Output Fader en el borde derecho del editor flotante. Es un fader vertical combinado con medidor de nivel.
3. Observe la barra de nivel detrás del control deslizante. La barra muestra el nivel de pico post-EQ suavizado en tiempo real mediante un degradado verde-ámbar-rojo, igual que el medidor de nivel Tube.
4. Transmita o reciba audio de manera normal. La barra de nivel se actualiza continuamente, reflejando el nivel de señal después de todas las bandas de EQ y el desplazamiento de ganancia maestra aplicados.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Output Fader (TX) | 0 dB | −36.0 a +12.0 dB | `ClientEqTxMasterGain` |
| Output Fader (RX) | 0 dB | −36.0 a +12.0 dB | `ClientEqRxMasterGain` |

El medidor de nivel detrás del control deslizante es únicamente un indicador. Muestra el pico post-EQ suavizado para la ruta vinculada a esta instancia del editor. No tiene un control independiente ni una clave persistida.

## Consejos

- Si el medidor alcanza de forma consistente los niveles ámbar o rojo, arrastre el control del Output Fader hacia abajo para reducir la ganancia post-EQ, o reduzca las ganancias de bandas individuales para bajar los niveles antes de la etapa maestra.
- Desplace la rueda del ratón sobre el Output Fader para realizar ajustes finos de 0.5 dB mientras observa el medidor.
- Haga doble clic en el Output Fader para restablecerlo a 0 dB sin modificar los ajustes de banda.

## Relacionados

- [Ajustar la ganancia de salida post-EQ con el Output Fader](adjust-post-eq-output-gain-with-the-output-fader.md)
- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquiera de los lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Congelar la traza de retención de pico del analizador para identificar resonancias durante el ajuste](freeze-the-analyzer-peak-hold-trace-to-spot-resonances-while-tuning.md)
- [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
