# Omitir la etapa de EQ en la cadena

Use esta página para omitir el EQ paramétrico del lado del cliente en la ruta TX o RX sin eliminar su configuración de bandas. Omitir es útil para comparaciones A/B o para deshabilitar temporalmente el EQ mientras mantiene su curva intacta.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa de EQ que desea omitir ya debe estar habilitada y presente en el widget CHAIN; si no aparece ninguna etapa de EQ (TX ni RX) en la cadena, consulte [Descripción general del EQ paramétrico Aetherial (TX / RX)](overview.md).

## Pasos

1. Ubique el widget CHAIN para la ruta que desea omitir: TX o RX.
2. Haga clic una sola vez en el mosaico de la etapa de EQ en el widget CHAIN para esa ruta.

   Al hacer clic en la etapa de EQ se activa o desactiva el modo de omisión en esa ruta. Cuando la omisión está activa, la etapa queda excluida de la cadena de procesamiento. Su configuración de bandas (`ClientEqTxBands` o `ClientEqRxBands`) se conserva y la etapa puede volver a habilitarse haciendo clic de nuevo.

3. Repita el procedimiento para la otra ruta si es necesario: los estados de omisión de TX y RX son independientes.

## Qué hace cada control

| Control | Ruta | Ajuste persistido | Efecto al omitir |
|---|---|---|---|
| Mosaico de etapa de EQ (TX) en el widget CHAIN | TX | `ClientEqTxEnabled` | Elimina el EQ de TX de la cadena de audio; las bandas de TX se conservan. |
| Mosaico de etapa de EQ (RX) en el widget CHAIN | RX | `ClientEqRxEnabled` | Elimina el EQ de RX de la cadena de audio; las bandas de RX se conservan. |

## Consejos

- Los sub-applets "Aetherial TX EQ" y "Aetherial RX EQ" se ocultan cuando la etapa de EQ correspondiente está deshabilitada. Si el applet desaparece después de activar la omisión, este comportamiento es el esperado.
- La configuración de bandas almacenada en `ClientEqTxBands` y `ClientEqRxBands` no se ve afectada al activar o desactivar la omisión. Al volver a habilitar la etapa, su curva se restaura exactamente.
- Para comparar su curva de EQ con una respuesta plana, haga clic rápidamente en el mosaico de la etapa para activar y desactivar la omisión.

## Relacionados

- [Descripción general del EQ paramétrico Aetherial (TX / RX)](overview.md)
- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquiera de los lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspeccionar la curva de EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
