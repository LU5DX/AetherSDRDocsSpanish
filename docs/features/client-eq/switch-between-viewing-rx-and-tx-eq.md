# Cambiar entre la visualización del EQ de RX y TX

El ClientEqApplet muestra una ruta de EQ a la vez — ya sea la ruta de recepción o la ruta de transmisión. Esta página explica cómo cambiar qué ruta muestra el widget de curva.

## Antes de comenzar

- El subcontenedor CEQ debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP). Permanece oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN o el editor flotante.
- El panel de applets debe estar abierto (`View > Applet Panel`).

## Pasos

1. Localice el tile **CEQ** en el panel de applets.
2. Haga clic en la pestaña **RX** para mostrar la curva de EQ y el analizador de la ruta de recepción.
3. Haga clic en la pestaña **TX** para mostrar la curva de EQ y el analizador de la ruta de transmisión.

El widget de curva se reasigna inmediatamente a la ruta seleccionada. La respuesta de EQ sumada y la superposición del analizador FFT en tiempo real se actualizan para reflejar dicha ruta.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **RX** | Pestaña | Activado | Asigna el widget de curva a la instancia de EQ de RX. Mutuamente exclusivo con TX. | — |
| **TX** | Pestaña | Desactivado | Asigna el widget de curva a la instancia de EQ de TX. Mutuamente exclusivo con RX. | — |
| Área del analizador / curva | Indicador | — | 110 px de alto. Muestra la respuesta de EQ sumada para la ruta seleccionada superpuesta con un analizador FFT en tiempo real. Solo lectura. | — |

El estado habilitado y la configuración de bandas de cada ruta se conservan por separado: `ClientEqRxEnabled`, `ClientEqTxEnabled`, `ClientEqRxBands` y `ClientEqTxBands`.

## Consejos

- Cambiar de pestaña no afecta el procesamiento. Ambas rutas de EQ, RX y TX, continúan ejecutándose independientemente de cuál se esté mostrando.
- Para editar bandas es necesario abrir el editor flotante. Haga doble clic en la etapa de EQ dentro del widget CHAIN para abrirlo. El área de curva en el applet es solo de visualización.

## Relacionados

- [Descripción general del EQ paramétrico (cliente)](overview.md)
- [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Ver el espectro en tiempo real de la ruta seleccionada](see-the-live-spectrum-of-the-selected-path.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
