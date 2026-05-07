# Cambiar entre visualización de EQ de RX y TX

El ClientEqApplet muestra una ruta de EQ a la vez — ya sea la ruta de recepción o la ruta de transmisión. Esta página explica cómo cambiar qué ruta muestra el widget de curva.

## Antes de comenzar

- El subcontenedor CEQ debe estar visible dentro del contenedor padre PooDoo Audio (TXDSP). Está oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN o el editor flotante.
- El panel de applets debe estar abierto (`View > Applet Panel`).

## Pasos

1. Localice el mosaico **CEQ** en el panel de applets.
2. Haga clic en la pestaña **RX** para mostrar la curva de EQ y el analizador de la ruta de recepción.
3. Haga clic en la pestaña **TX** para mostrar la curva de EQ y el analizador de la ruta de transmisión.

El widget de curva se reenlaza inmediatamente a la ruta seleccionada. La respuesta de EQ sumada y la superposición del analizador FFT en vivo se actualizan para reflejar esa ruta.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **RX** | Pestaña | Marcada | Enlaza el widget de curva a la instancia de EQ de RX. Mutuamente excluyente con TX. | — |
| **TX** | Pestaña | Sin marcar | Enlaza el widget de curva a la instancia de EQ de TX. Mutuamente excluyente con RX. | — |
| Área de analizador/curva | Indicador | — | 110 px de altura. Muestra la respuesta de EQ sumada para la ruta seleccionada superpuesta con un analizador FFT en vivo. Solo visualización. | — |

El estado habilitado y la configuración de banda para cada ruta se guardan por separado: `ClientEqRxEnabled`, `ClientEqTxEnabled`, `ClientEqRxBands` y `ClientEqTxBands`.

## Consejos

- Cambiar de pestaña no afecta el procesamiento. Ambas rutas de EQ (RX y TX) continúan ejecutándose independientemente de cuál se muestre.
- La edición de bandas requiere abrir el editor flotante. Haga doble clic en la etapa de EQ en el widget CHAIN para abrirlo. El área de curva en el applet es solo de visualización.

## Relacionados

- [Visión general de EQ paramétrico (Cliente)](overview.md)
- [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Ver el espectro en vivo de la ruta seleccionada](see-the-live-spectrum-of-the-selected-path.md)
- [Verificar que la curva sumada coincida con su objetivo mental](verify-the-summed-curve-matches-your-mental-target.md)
