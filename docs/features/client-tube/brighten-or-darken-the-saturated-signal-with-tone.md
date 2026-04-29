# Aclarar u oscurecer la señal saturada con Tone

Use el control **Tone** para inclinar el carácter espectral de la señal saturada: los valores negativos la hacen más oscura y cálida, mientras que los valores positivos la hacen más brillante y presente. Tone actúa de forma independiente en el lado TX (Aetherial Mic-PreAmp) y en el lado RX (Aetherial Dynamic Tube).

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible en el Applet Panel. Haga doble clic en la etapa TUBE del widget CHAIN para abrir el editor flotante, o localice el subcontenedor directamente en el panel.

## Pasos

1. Localice la fila de cinco controles en la parte inferior del applet Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX).
2. Encuentre el control etiquetado como **Tone** — es el segundo desde la izquierda, entre Drive y Bias.
3. Gire el control **Tone** hacia la izquierda (hacia −1.00) para oscurecer la señal saturada, o hacia la derecha (hacia +1.00) para aclararla.
4. Lea el valor actual en la etiqueta que aparece debajo del control. La etiqueta muestra dos decimales (p. ej., `−0.50` o `0.75`).
5. Para restablecer Tone a su valor predeterminado, haga doble clic en el control **Tone**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste guardado | Comportamiento |
|---|---|---|---|---|
| Tone (TX) | 0.00 | −1.0 a 1.0 | `ClientTubeTxTone` | Los valores negativos oscurecen y los positivos aclaran la señal saturada. |
| Tone (RX) | 0.00 | −1.0 a 1.0 | `ClientTubeRxTone` | Mismo comportamiento que Tone en TX, aplicado a la cadena de recepción. |

## Medidor de nivel de salida

El editor flotante (titulado **Aetherial Tube — TX** o **Aetherial Tube — RX**) incluye un medidor de nivel **OUT** en la columna del extremo derecho. Este medidor muestra el nivel de pico posterior a la saturación y utiliza una dinámica de ataque rápido / liberación lenta.

| Rango de nivel | Color del medidor |
|---|---|
| −60 a −12 dB | Verde |
| −12 a −6 dB | Lima |
| −6 a −3 dB | Ámbar |
| Por encima de −3 dB | Rojo |

El medidor solo es visible en el editor flotante. No aparece en el mosaico del applet acoplado en el Applet Panel.

## Consejos

- Tone interactúa con Drive: un valor alto de Drive produce más armónicos de saturación, por lo que los ajustes de Tone se vuelven más audibles a medida que Drive aumenta. Ajuste Drive primero y luego use Tone para dar forma al resultado.
- Si tiene el editor flotante abierto junto al applet, ambos reflejan el mismo valor. Los cambios realizados en uno se sincronizan con el otro en aproximadamente 33 ms.
- Un valor de Tone de 0.00 deja sin cambios el balance espectral de la señal saturada.
- Observe el medidor **OUT** en el editor flotante para detectar recorte posterior a la saturación. Si el medidor alcanza el rojo, reduzca el control **Output** o disminuya **Drive**.

## Solución de problemas

- **El control Tone no produce ningún efecto audible** — la etapa de tubo puede estar omitida. Confirme que la etapa está activa en el widget CHAIN del lado correspondiente. Verifique también que Mix esté por encima del 0 %; una señal completamente seca (Mix al 0 %) pasa por el modelo de tubo, pero no mezcla ninguna salida con efecto.
- **La posición del control no coincide con lo esperado al recargar** — el valor se guarda automáticamente cada vez que se modifica el control. Si `ClientTubeTxTone` o `ClientTubeRxTone` no existe o está dañado en su archivo de ajustes, el valor vuelve al predeterminado de 0.00.
- **El medidor OUT no es visible** — el medidor solo aparece en el editor flotante. Haga doble clic en la etapa TUBE en el widget CHAIN para abrirlo.

## Relacionado

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplazar Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Mezclar la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
