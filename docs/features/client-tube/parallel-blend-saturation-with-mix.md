# Saturación en paralelo con Mix

El control **Mix** mezcla la señal seca (sin procesar) con la salida de tubo completamente saturada. Al reducir Mix por debajo del 100 % es posible añadir riqueza armónica conservando parte del carácter transitorio de la señal original — una técnica denominada saturación en paralelo.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- Abra el applet que contiene el control Mix: **Aetherial Mic-PreAmp** (lado TX) o **Aetherial Dynamic Tube** (lado RX), ubicado dentro del contenedor principal Aetherial Audio (TXDSP).

## Pasos

1. Localice el control **Mix** — el más a la derecha en la fila de cinco controles, etiquetado como **Mix**.
2. Gire **Mix** para establecer el balance seco/húmedo. La etiqueta muestra el valor actual como porcentaje (por ejemplo, `75 %`).
   - `100 %` — señal completamente saturada, sin mezcla seca (valor predeterminado).
   - `0 %` — solo señal seca; la saturación del tubo es inaudible.
   - Los valores entre `0 %` y `100 %` mezclan la señal seca y la húmeda proporcionalmente.
3. Ajuste **Drive**, **Bias** y **Tone** en la ruta húmeda según sea necesario. La curva de transferencia y la bola de entrada en vivo se actualizan para reflejar la señal saturada independientemente de la posición de Mix.
4. Use **Output** para compensar cualquier cambio de nivel global introducido por la mezcla. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).

La configuración se guarda automáticamente cada vez que mueve el control.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Configuración persistente (TX / RX) |
|---------|---------------|--------------|--------------------------------------|
| Mix | `100 %` | `0 %` a `100 %` (almacenado como 0.0 a 1.0) | `ClientTubeTxDryWet` / `ClientTubeRxDryWet` |

## Consejos

- Comience con **Mix** en `100 %`, ajuste **Drive** y **Bias** hasta obtener el tono deseado y luego reduzca Mix hasta que el resultado encaje cómodamente en el audio — esto es más sencillo que intentar ajustar todos los controles simultáneamente.
- Dado que las señales seca y húmeda se suman, ajustes elevados de **Drive** con valores bajos de Mix pueden producir contenido armónico audible sin saturar la fuente.
- Las etapas de tubo TX y RX tienen configuraciones de Mix completamente independientes. Ajustar un lado no afecta al otro.

## Relacionado

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez TX o modelado de tono RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
