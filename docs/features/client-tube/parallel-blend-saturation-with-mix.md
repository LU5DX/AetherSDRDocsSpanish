# Saturación en paralelo con Mix

El control Mix combina la señal seca (sin procesar) con la salida totalmente saturada del tubo. Reducir Mix desde el 100 % permite añadir color armónico mientras se conserva el carácter transitorio y la sensación dinámica de la señal original, una técnica denominada saturación en paralelo.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible dentro del contenedor padre Aetherial Audio (TXDSP).

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del applet: Drive, Tone, Bias, Output, Mix.
2. Busque el mando situado más a la derecha, etiquetado como **Mix**.
3. Gire **Mix** para ajustar el balance seco/húmedo. En **100 %** solo pasa la señal saturada. En **0 %** solo pasa la señal seca. Los valores intermedios combinan ambas proporcionalmente.
4. Observe la curva de transferencia y escuche el resultado. Un valor entre 30–60 % es típico para saturación en paralelo.
5. Si el nivel combinado es más fuerte o más suave que la señal seca, ajústelo con el mando **Output**. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistente |
|---|---|---|---|
| Mix (TX) | 100 % | 0 % a 100 % (almacenado como 0.0–1.0) | `ClientTubeTxDryWet` |
| Mix (RX) | 100 % | 0 % a 100 % (almacenado como 0.0–1.0) | `ClientTubeRxDryWet` |

Mix funciona como una combinación lineal seco/húmedo. La etiqueta del mando muestra el valor como porcentaje (ej. `50 %`).

## Monitoreo del nivel posterior a la saturación con el medidor Output

El editor flotante Aetherial Tube (titulado **Aetherial Tube — TX** o **Aetherial Tube — RX**) incluye un medidor de nivel **OUT** en el extremo derecho de la ventana del editor. El medidor muestra el nivel pico posterior a la saturación con balística de ataque rápido / liberación lenta y no es visible en el mosaico del applet acoplado.

| Color | Rango de nivel |
|---|---|
| Verde | −60 dB a −12 dB |
| Lima | −12 dB a −6 dB |
| Ámbar | −6 dB a −3 dB |
| Rojo | Por encima de −3 dB |

Use el medidor para verificar que la señal saturada no esté recortando antes de llegar al procesamiento posterior. Si el medidor está constantemente en ámbar o rojo, reduzca el mando **Drive** o ajuste el mando **Output**.

## Consejos

- Los ajustes de Mix realizados en el editor flotante Aetherial Tube se reflejan en el mando del applet en aproximadamente 33 ms, y viceversa. No es necesario reabrir el editor después de cambiar Mix en el applet.
- Mix se aplica después de la etapa de tubo pero antes de cualquier otro elemento en la cadena: ajuste primero Drive a su gusto, luego use Mix para reducir la intensidad sin perder la forma armónica que configuró.
- El medidor **OUT** solo está disponible en el editor flotante. Abra el editor haciendo doble clic en el mosaico del applet si necesita monitorear los niveles posteriores a la saturación mientras ajusta Mix.

## Relacionados

- [Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX) overview](overview.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
