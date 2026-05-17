# Aclarar u oscurecer la señal saturada con Tone

Utilice el control Tone para inclinar el carácter espectral de la señal saturada: los valores negativos la oscurecen y la vuelven más cálida, los valores positivos la aclaran y la hacen más presente. Tone funciona de forma independiente tanto en el lado TX (Aetherial Mic-PreAmp) como en el lado RX (Aetherial Dynamic Tube).

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible en el Applet Panel. Haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor flotante, o localice el subcontenedor directamente en el panel.

## Pasos

1. Localice la fila de cinco perillas en la parte inferior del applet Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX).
2. Encuentre la perilla etiquetada **Tone**: es la segunda perilla desde la izquierda, entre Drive y Bias.
3. Gire la perilla **Tone** hacia la izquierda (hacia −1.00) para oscurecer la señal saturada, o hacia la derecha (hacia +1.00) para aclararla.
4. Lea el valor actual en la etiqueta debajo de la perilla. La etiqueta muestra dos decimales (por ejemplo, `−0.50` o `0.75`).
5. Para restablecer Tone a su valor predeterminado, haga doble clic en la perilla **Tone**.
6. Para escribir un valor preciso directamente, haga clic en la visualización del valor debajo de la perilla Tone. Aparece un pequeño campo de entrada de texto. Escriba el valor deseado y presione **Enter** o haga clic en otro lugar para confirmar. El valor se limita automáticamente al rango válido. Presione **Escape** para cancelar la edición y revertir al valor anterior.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste persistida | Comportamiento |
|---|---|---|---|---|
| Tone (TX) | 0.00 | −1.0 a 1.0 | `ClientTubeTxTone` | Los valores negativos oscurecen, los positivos aclaran la señal saturada. |
| Tone (RX) | 0.00 | −1.0 a 1.0 | `ClientTubeRxTone` | Mismo comportamiento que Tone en TX, aplicado a la ruta de recepción. |

## Medidor de nivel de salida

El editor flotante (titulado **Aetherial Tube — TX** o **Aetherial Tube — RX**) incluye un medidor de nivel **OUT** en la columna del extremo derecho. Este medidor muestra el nivel pico posterior a la saturación y utiliza balística de ataque rápido / liberación lenta.

| Rango de nivel | Color del medidor |
|---|---|
| −60 a −12 dB | Verde |
| −12 a −6 dB | Lima |
| −6 a −3 dB | Ámbar |
| Por encima de −3 dB | Rojo |

El medidor solo es visible en el editor flotante. No aparece en el mosaico del applet acoplado en el Applet Panel.

## Atenuación por bypass

Cuando la etapa de tubo está en bypass, todo el mosaico del applet acoplado se renderiza con opacidad reducida (aproximadamente 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en el widget de la curva EQ cuando esa etapa está en bypass. La opacidad vuelve al valor completo tan pronto como se rehabilita la etapa. El editor flotante no se ve afectado por esta atenuación.

## Consejos

- Tone interactúa con Drive: un valor alto de Drive produce más armónicos de saturación, por lo que los ajustes de Tone se vuelven más audibles a medida que aumenta Drive. Ajuste Drive primero, luego use Tone para dar forma al resultado.
- Si tiene el editor flotante abierto junto con el applet, ambos reflejan el mismo valor. Los cambios realizados en uno se sincronizan con el otro en aproximadamente 33 ms.
- Un valor de Tone de 0.00 no modifica el equilibrio espectral de la señal saturada.
- Observe el medidor **OUT** en el editor flotante para detectar recorte posterior a la saturación. Si el medidor alcanza el rojo, reduzca la perilla **Output** o baje **Drive**.
- El editor de valor en línea admite el análisis numérico sensible a la configuración regional. Ingrese `12,5` en una configuración regional de coma decimal, o elimine unidades como `12.5 ms` y el editor analizará la parte numérica.

## Solución de problemas

- **La perilla Tone no tiene efecto audible** — la etapa de tubo puede estar en bypass. Confirme que la etapa esté activa en el widget CHAIN en el lado correspondiente. También verifique que Mix esté por encima del 0 %; una señal completamente seca (Mix al 0 %) atraviesa el modelo de tubo pero no mezcla ninguna salida procesada.
- **La posición de la perilla no coincide con lo esperado después de recargar** — el valor se guarda automáticamente cada vez que la perilla cambia. Si `ClientTubeTxTone` o `ClientTubeRxTone` falta o está corrupto en su archivo de configuración, el valor vuelve al valor predeterminado de 0.00.
- **El medidor OUT no es visible** — el medidor solo aparece en el editor flotante. Haga doble clic en la etapa TUBE en el widget CHAIN para abrirlo.
- **El mosaico del applet aparece atenuado** — la etapa de tubo está en bypass. Habilite la etapa en el widget CHAIN para restaurar la opacidad completa.
- **El editor en línea muestra un borde rojo y no acepta la entrada** — el editor solo aparece cuando hace clic en la visualización del valor. Si no ve el editor, asegúrese de hacer clic directamente en el texto del valor numérico debajo de la perilla, no en la perilla misma. El editor vuelve a una apariencia similar a una etiqueta cuando no está enfocado.

## Relacionados

- [Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX) overview](overview.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Shift Bias to tweak the even / odd harmonic balance](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Parallel-blend saturation with Mix](parallel-blend-saturation-with-mix.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Type exact values with the value popup editor](type-exact-values-with-the-value-popup-editor.md)
