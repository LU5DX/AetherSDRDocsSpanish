# Cambiar a una referencia externa de 10 MHz

Esta página explica cómo seleccionar una fuente de referencia externa de 10 MHz en el FLEX-8600, lo que sincroniza la base de tiempo del radio con un oscilador externo de alta estabilidad o un GPSDO, en lugar de la referencia interna.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Radio Setup requiere una conexión activa al radio.
- Debe haber una señal de referencia estable de 10 MHz presente en la entrada de referencia externa del radio antes de cambiar la fuente.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Localice el cuadro combinado **10 MHz Reference Source:**.
4. Seleccione **External** en el cuadro combinado.

El radio aplica el cambio de inmediato. Para volver al oscilador interno, seleccione **Internal**.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Valores válidos |
|---|---|---|---|
| **10 MHz Reference Source:** | Selecciona si el radio se sincroniza con su oscilador interno o con una señal en la entrada de referencia externa de 10 MHz. | Internal | Internal, External |

## Consejos

- Si también está corrigiendo un error de frecuencia medido, ajuste **Freq Offset (ppb):** en la misma pestaña **RX** antes o después de cambiar la fuente de referencia.

## Solución de problemas

- **El radio no se sincroniza con la referencia externa** — Verifique que la señal externa esté presente, a 10 MHz y dentro de la especificación de nivel de entrada del radio antes de seleccionar **External**. Si la referencia desaparece después de cambiar, el radio perderá la sincronía; regrese el cuadro combinado a **Internal** hasta que la señal sea restaurada.

## Temas relacionados

- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Descripción general de Radio Setup](overview.md)
