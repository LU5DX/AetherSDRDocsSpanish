# Cambiar a una referencia externa de 10 MHz

Use esta página para cambiar la referencia de frecuencia del radio Flex desde su oscilador interno a una señal externa de 10 MHz conectada al conector REF IN del panel trasero. Una referencia externa mejora la exactitud y la estabilidad de frecuencia, lo cual es importante para trabajo en señales débiles, modos digitales y operación con estándares disciplinados por GPS o de rubidio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **RX** en Radio Setup no es accesible sin una conexión activa.
- Debe haber una señal estable de 10 MHz presente en la entrada de referencia externa del panel trasero del radio antes de cambiar la fuente.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Localice el cuadro combinado **10 MHz Reference Source:**.
4. Seleccione **External**.

El radio cambia a la referencia externa de inmediato. Para revertir, seleccione **Internal** en el mismo cuadro combinado.

## Qué hace cada control

| Control | Tipo | Valores válidos | Comportamiento |
|---|---|---|---|
| **10 MHz Reference Source:** | Cuadro combinado | `Internal` \| `External` | Selecciona si el radio utiliza como reloj su oscilador interno o una señal externa de 10 MHz en la entrada del panel trasero. |

## Consejos

- Si también está corrigiendo un desplazamiento de frecuencia, ajuste **Freq Offset (ppb):** en la misma pestaña **RX** después de cambiar a la referencia externa. Consulte [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md) para ese procedimiento.
- Volver a **Internal** mientras la referencia externa sigue conectada es seguro; el radio utilizará su oscilador interno e ignorará la señal del panel trasero.

## Solución de problemas

- **La visualización de frecuencia salta o se vuelve inestable después de seleccionar External** — La señal externa de 10 MHz está ausente, es demasiado débil o está fuera de especificación. Verifique que la señal esté presente y dentro del nivel de entrada requerido por el radio antes de seleccionar External. Vuelva a **Internal** para restaurar la operación normal.

## Relacionado

- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
