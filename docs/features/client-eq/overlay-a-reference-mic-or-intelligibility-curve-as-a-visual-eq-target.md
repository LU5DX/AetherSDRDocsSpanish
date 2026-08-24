# Superponer un micrófono de referencia o una curva de inteligibilidad como objetivo visual de EQ

Esta página le muestra cómo visualizar una curva de respuesta en frecuencia de referencia—como el objetivo de inteligibilidad AT&T de 1959 o la respuesta de un micrófono SSB famoso—en el lienzo de EQ mientras sintoniza bandas. La curva es solo una guía visual; no afecta el cálculo del EQ.

## Antes de comenzar

- Abra el editor Aetherial Parametric EQ haciendo doble clic en la etapa EQ en el widget CHAIN (lado TX o RX).
- La ventana del editor se titula "Aetherial Parametric EQ — TX" o "— RX", según el lado que haya abierto.

## Pasos

1. En la franja de encabezado del editor flotante, localice el cuadro combinado **Ref:**.
2. Haga clic en el cuadro combinado **Ref:** y seleccione una de las siguientes opciones:
   - **Off** (predeterminado) — sin curva de referencia
   - **AT&T 1959** — objetivo de inteligibilidad de Bell Labs, +5 dB a 2.5 kHz
   - **Heil DX** — refuerzo de presencia agresivo para concursos SSB
   - **Astatic D-104** — micrófono clásico tipo chupete, pico agudo a 3 kHz
   - **Shure 444** — micrófono de escritorio estilo radiodifusión, refuerzo más suave
   - **Heil HC-5** — elemento dinámico SSB moderno
3. La curva seleccionada aparece como una línea delgada de color ámbar en el lienzo de EQ.
4. Ajuste sus bandas de EQ para que coincidan con la curva de referencia, o úsela como forma aproximada para su respuesta objetivo.
5. Para eliminar la superposición, seleccione **Off** en el cuadro combinado **Ref:**.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de ajuste persistida | Comportamiento |
|---|---|---|---|---|
| Cuadro combinado **Ref:** | Off | Off \| AT&T 1959 \| Heil DX \| Astatic D-104 \| Shure 444 \| Heil HC-5 | `ClientEqReferenceCurve` | Superpone una curva objetivo de referencia en el lienzo de EQ como una línea delgada de color ámbar. Compartido entre los editores RX y TX. |
| Cuadro combinado **Smoothing:** | Off (1/96) | Off (1/96) \| 1/24 \| 1/12 \| 1/6 \| 1/3 | `ClientEqSmoothingFraction` | Aplica promediado de potencia por fracción de octava a la traza del analizador para su visualización. No afecta el cálculo del EQ. Compartido entre los editores RX y TX. |

## Consejos

- La curva de referencia es solo de visualización—nunca cambia la ruta de audio, así que siéntase libre de experimentar con diferentes preajustes.
- La selección persiste de forma global; elegir una curva en el editor TX también afecta la visualización del editor RX.
- Combine la curva de referencia con **Peak Hold** para comparar la forma de sus bandas contra una vista sostenida del audio que realmente atraviesa el sistema.

## Relacionado

- [Inspeccione la curva de EQ TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccione la curva de EQ RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Suavice la visualización del analizador para una lectura más fácil con el cuadro combinado Smoothing](smooth-the-analyzer-display-for-easier-reading-with-the-smoothing-combo.md)
- [Verifique que la curva sumada coincida con su objetivo mental](verify-the-summed-curve-matches-your-mental-target.md)
