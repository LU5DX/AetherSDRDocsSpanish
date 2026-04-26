# Omitir la etapa de EQ de la cadena

Elimine el EQ paramétrico del lado del cliente de la cadena de procesamiento de audio sin borrar la configuración de bandas. Use esto cuando desee comparar audio procesado y sin procesar, o deshabilitar temporalmente el EQ sin perder su configuración.

## Antes de comenzar

- El ClientEqApplet (etiquetado "CEQ") debe ser visible en el panel de applets. Permanece oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN o el editor flotante.
- Abra el editor flotante de EQ haciendo doble clic en la etapa de EQ en el widget CHAIN. El control de omisión se encuentra en ese editor, no en el mosaico compacto del applet CEQ.

## Pasos

1. Haga doble clic en la etapa de EQ en el widget CHAIN para abrir el editor flotante de EQ.
2. En el editor flotante, localice el interruptor de habilitación para la ruta que desea omitir: RX o TX.
3. Haga clic en el interruptor para deshabilitar el EQ en esa ruta.

El mosaico del applet CEQ refleja el cambio: `ClientEqRxEnabled` o `ClientEqTxEnabled` se establece en false para la ruta afectada, y el EQ se elimina de la cadena de señal. La configuración de bandas almacenada en `ClientEqRxBands` y `ClientEqTxBands` se conserva.

## Qué hace cada control

| Control | Ruta | Clave persistida | Predeterminado | Comportamiento |
|---|---|---|---|---|
| Interruptor de habilitación RX | Recepción | `ClientEqRxEnabled` | — | Inserta u omite el EQ en la cadena de audio RX. Las bandas se conservan al omitir. |
| Interruptor de habilitación TX | Transmisión | `ClientEqTxEnabled` | — | Inserta u omite el EQ en la cadena de audio TX. Las bandas se conservan al omitir. |
| `ClientEqRxBands` | Recepción | `ClientEqRxBands` | — | Configuración de bandas persistida para la ruta RX. No se ve afectada por la omisión. |
| `ClientEqTxBands` | Transmisión | `ClientEqTxBands` | — | Configuración de bandas persistida para la ruta TX. No se ve afectada por la omisión. |

## Consejos

- Omitir una ruta no afecta a la otra. Puede omitir el EQ de RX mientras mantiene activo el EQ de TX, o viceversa.
- La curva de respuesta de EQ sumada en el mosaico del applet CEQ muestra el estado actual de la ruta seleccionada. Cuando se omite, la curva refleja que el EQ está inactivo.

## Solución de problemas

- **El mosaico del applet CEQ no es visible** — El mosaico permanece oculto hasta que la etapa de EQ se habilite desde el widget CHAIN o el editor flotante. Habilite la etapa primero y luego omítala si es necesario.
- **Hacer doble clic en el widget CHAIN no abre el editor flotante** — Confirme que está haciendo doble clic directamente sobre el bloque de la etapa de EQ dentro del widget CHAIN, no sobre el contenedor que lo rodea.

## Relacionados

- [Descripción general del EQ paramétrico (cliente)](overview.md)
- [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Alternar entre la vista de EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
