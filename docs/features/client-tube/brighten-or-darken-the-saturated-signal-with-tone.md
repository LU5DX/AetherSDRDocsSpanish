# Aclarar u oscurecer la señal saturada con Tone

Use el mando **Tone** para inclinar el carácter espectral de la señal saturada: los valores negativos la oscurecen y la hacen más cálida, los valores positivos la aclaran y la hacen más presente. **Tone** funciona de forma independiente tanto en el lado de TX (Aetherial Mic-PreAmp) como en el de RX (Aetherial Dynamic Tube).

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible en el Applet Panel. Haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor flotante, o localice el subcontenedor directamente en el panel.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del applet Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX).
2. Encuentre el mando etiquetado **Tone** — es el segundo mando desde la izquierda, entre Drive y Bias.
3. Gire el mando **Tone** hacia la izquierda (hacia −1.00) para oscurecer la señal saturada, o hacia la derecha (hacia +1.00) para aclararla.
4. Lea el valor actual en la etiqueta debajo del mando. La etiqueta muestra dos decimales (por ejemplo, `−0.50` o `0.75`).
5. Para restablecer Tone a su valor predeterminado, haga doble clic en el mando **Tone**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistente | Comportamiento |
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

Cuando la etapa de tubo está en bypass, todo el mosaico del applet acoplado se muestra con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en el widget de la curva EQ cuando esa etapa está en bypass. La opacidad vuelve al completo tan pronto como la etapa se reactiva. El editor flotante no se ve afectado por esta atenuación.

## Consejos

- **Tone** interactúa con Drive: un valor alto de Drive produce más armónicos de saturación, por lo que los ajustes de Tone se vuelven más audibles a medida que Drive aumenta. Ajuste Drive primero, luego use Tone para dar forma al resultado.
- Si tiene el editor flotante abierto junto al applet, ambos reflejan el mismo valor. Los cambios realizados en uno se sincronizan con el otro en aproximadamente 33 ms.
- Un valor de Tone de 0.00 deja sin cambios el balance espectral de la señal saturada.
- Observe el medidor **OUT** en el editor flotante para detectar recorte posterior a la saturación. Si el medidor llega al rojo, reduzca el mando **Output** o baje **Drive**.

## Solución de problemas

- **El mando Tone no tiene efecto audible** — la etapa de tubo puede estar en bypass. Confirme que la etapa esté activa en el widget CHAIN del lado correspondiente. También verifique que Mix esté por encima del 0 %; una señal completamente seca (Mix al 0 %) pasa a través del modelo de tubo pero no mezcla nada de la salida procesada.
- **La posición del mando no coincide con lo que espera después de recargar** — el valor se guarda automáticamente cada vez que el mando cambia. Si `ClientTubeTxTone` o `ClientTubeRxTone` faltan o están dañados en su archivo de configuración, el valor vuelve al valor predeterminado de 0.00.
- **El medidor OUT no es visible** — el medidor solo aparece en el editor flotante. Haga doble clic en la etapa TUBE en el widget CHAIN para abrirlo.
- **El mosaico del applet aparece atenuado** — la etapa de tubo está en bypass. Active la etapa en el widget CHAIN para restaurar la opacidad completa.

## Relacionados

- [Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX) overview](overview.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Shift Bias to tweak the even / odd harmonic balance](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Parallel-blend saturation with Mix](parallel-blend-saturation-with-mix.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
