# Omitir la etapa de EQ de la cadena

Esta página explica cómo omitir el EQ paramétrico del lado del cliente para la ruta de audio TX o RX. Al omitirlo, se elimina el EQ de la cadena de señal sin borrar la configuración de bandas.

## Antes de comenzar

- AetherSDR debe estar abierto. No se requiere conexión a una radio para omitir el EQ.
- La etapa de EQ ya debe estar presente en el widget CHAIN para la ruta que desea omitir (TX o RX).

## Pasos

1. Localice el widget CHAIN para la ruta que desea omitir: ya sea la cadena TX o la cadena RX.
2. Haga clic una vez en la etapa de EQ en el widget CHAIN para esa ruta.

La etapa de EQ queda omitida para esa ruta. El ajuste `ClientEqTxEnabled` o `ClientEqRxEnabled` se actualiza de inmediato y se conserva entre reinicios.

Para volver a activar el EQ, haga clic una vez más en la etapa de EQ en el widget CHAIN.

## Qué hace cada control

| Control | Ruta | Clave persistida | Comportamiento |
|---|---|---|---|
| Etapa de EQ (cadena TX) | TX | `ClientEqTxEnabled` | Un clic activa o desactiva la omisión del EQ de TX. Omitido = EQ eliminado de la cadena de señal; las bandas y los ajustes se conservan. |
| Etapa de EQ (cadena RX) | RX | `ClientEqRxEnabled` | Un clic activa o desactiva la omisión del EQ de RX. Omitido = EQ eliminado de la cadena de señal; las bandas y los ajustes se conservan. |

Los datos de banda se almacenan por separado en `ClientEqTxBands` y `ClientEqRxBands` y no se ven afectados por la omisión.

## Consejos

- El estado de omisión es por ruta. Omitir el EQ de TX no afecta el EQ de RX, y viceversa.
- Los mosaicos de los applets "Aetherial TX EQ" y "Aetherial RX EQ" se ocultan cuando su etapa de EQ correspondiente no está habilitada. Si un mosaico desaparece después de omitir, este es el comportamiento esperado.
- El editor flotante ("Aetherial Parametric EQ — TX" o "— RX") aún puede abrirse con doble clic en la etapa del widget CHAIN aunque esté omitido, por lo que puede continuar editando bandas sin volver a activar el EQ.

## Relacionados

- [Descripción general del Aetherial Parametric EQ (TX / RX)](overview.md)
- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en ambas rutas](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspeccionar la curva del EQ de TX y el espectro en tiempo real](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva del EQ de RX y el espectro en tiempo real](inspect-the-rx-eq-curve-and-live-spectrum.md)
