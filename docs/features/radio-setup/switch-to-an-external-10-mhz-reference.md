# Cambiar a una referencia externa de 10 MHz

Esta página explica cómo seleccionar un reloj de referencia externo de 10 MHz en un FLEX-8600 conectado. Use una referencia externa cuando disponga de un oscilador disciplinado por GPS u otra fuente de precisión de 10 MHz y desee que la radio se sincronice con ella en lugar de con su oscilador interno.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Radio Setup requiere una conexión de radio activa.
- La señal de referencia externa de 10 MHz debe estar conectada al puerto REF IN del panel trasero del FLEX-8600 antes de cambiar la fuente.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Localice el cuadro combinado `10 MHz Reference Source:`.
4. Seleccione `External` en el cuadro combinado. Para volver al oscilador interno, seleccione `Internal`.

## Qué hace cada control

| Control | Tipo | Rango válido | Comportamiento |
|---|---|---|---|
| `10 MHz Reference Source:` | Cuadro combinado | `Internal` \| `External` | Indica a la radio qué fuente de 10 MHz debe usar para sincronizar sus relojes ADC. `Internal` utiliza el oscilador integrado de la radio. `External` se sincroniza con la señal presente en el conector REF IN del panel trasero. |

## Consejos

- La pestaña `RX` también contiene el control numérico `Cal Frequency (MHz):` y el control numérico `Freq Offset (ppb):` utilizados para la calibración del GPSDO. Si usa un oscilador disciplinado por GPS como referencia externa, consulte [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md) para conocer el procedimiento de calibración.

## Solución de problemas

- **La frecuencia de la radio parece inestable o desplazada tras cambiar a External** — Es posible que la señal REF IN esté ausente, tenga un nivel demasiado bajo o no sea exactamente de 10 MHz. Verifique que la fuente externa esté en funcionamiento y correctamente conectada antes de seleccionar `External`. Vuelva a `Internal` mientras realiza el diagnóstico.

## Relacionado

- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
