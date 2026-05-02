# Saturación de mezcla en paralelo con Mix

El control Mix mezcla la señal seca (sin procesar) con la salida de tubo completamente saturada. Al reducir Mix desde el 100 % puede agregar color armónico mientras preserva el carácter transitorio y la sensación dinámica de la señal original — una técnica denominada saturación en paralelo.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible dentro del contenedor principal Aetherial Audio (TXDSP).

## Pasos

1. Localice la fila de cinco controles en la parte inferior del applet — Drive, Tone, Bias, Output, Mix.
2. Encuentre el control más a la derecha, etiquetado como **Mix**.
3. Gire **Mix** para establecer el balance seco/húmedo. Al **100 %** solo pasa la señal saturada. Al **0 %** solo pasa la señal seca. Los valores intermedios mezclan ambas de forma proporcional.
4. Observe la curva de transferencia y escuche el resultado. Un valor de alrededor del 30–60 % es típico para la saturación en paralelo.
5. Si el nivel mezclado es más alto o más bajo que la señal seca, ajústelo con el control **Output**. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---|---|---|---|
| Mix (TX) | 100 % | 0 % a 100 % (almacenado como 0.0–1.0) | `ClientTubeTxDryWet` |
| Mix (RX) | 100 % | 0 % a 100 % (almacenado como 0.0–1.0) | `ClientTubeRxDryWet` |

Mix opera como una mezcla lineal seco/húmedo. La etiqueta del control muestra el valor como porcentaje (p. ej., `50 %`).

## Monitoreo del nivel posterior a la saturación con el medidor Output

El editor flotante Aetherial Tube (titulado **Aetherial Tube — TX** o **Aetherial Tube — RX**) incluye un medidor de nivel **OUT** en el extremo derecho de la ventana del editor. El medidor muestra el nivel de pico posterior a la saturación con balística de ataque rápido / liberación lenta y no es visible en el panel de applet acoplado.

| Color | Rango de nivel |
|---|---|
| Verde | −60 dB a −12 dB |
| Lima | −12 dB a −6 dB |
| Ámbar | −6 dB a −3 dB |
| Rojo | Por encima de −3 dB |

Use el medidor para verificar que la señal saturada no esté recortando antes de llegar al procesamiento posterior. Si el medidor permanece constantemente en ámbar o rojo, reduzca el control **Drive** o ajuste el control **Output**.

## Consejos

- Los ajustes de Mix realizados en el editor flotante Aetherial Tube se reflejan en el control del applet en aproximadamente 33 ms, y viceversa. No es necesario volver a abrir el editor después de cambiar Mix en el applet.
- Mix se aplica después de la etapa de tubo pero antes de nada más en la cadena — ajuste Drive primero a su gusto, luego use Mix para reducir la intensidad sin perder la forma armónica que configuró.
- El medidor **OUT** solo está disponible en el editor flotante. Abra el editor haciendo doble clic en el panel del applet si necesita monitorear los niveles posteriores a la saturación mientras ajusta Mix.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ajustar Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
