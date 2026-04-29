# Abrir el editor flotante para agregar / eliminar / ajustar bandas

El ClientEqEditor flotante es donde se agregan, eliminan y ajustan las bandas de EQ para las rutas de RX y TX. El applet compacto en el panel muestra el resultado; la edición siempre ocurre en esta ventana separada.

## Antes de comenzar

- El applet CEQ debe estar visible en el panel de applets. Permanece oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN.
- Localice el mosaico de la etapa de EQ en el widget CHAIN para la ruta que desea editar (RX o TX).

## Pasos

1. Encuentre la etapa de EQ en el widget CHAIN para la ruta que desea configurar (cadena RX para recepción, cadena TX para transmisión).
2. Haga doble clic en la etapa de EQ en el widget CHAIN.
3. Se abre la ventana flotante ClientEqEditor. Agregue, elimine o ajuste bandas allí.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| RX | Pestaña | Seleccionada | Vincula el widget de curva a la instancia de EQ de RX. | — |
| TX | Pestaña | No seleccionada | Vincula el widget de curva a la instancia de EQ de TX. | — |
| Área del analizador / curva | Indicador | — | Muestra la respuesta de EQ sumada y una superposición FFT en tiempo real para la ruta seleccionada. Solo lectura; la edición requiere el editor flotante. | — |
| Estado habilitado de RX | — | — | Indica si la etapa de EQ de RX está activa. | `ClientEqRxEnabled` |
| Estado habilitado de TX | — | — | Indica si la etapa de EQ de TX está activa. | `ClientEqTxEnabled` |
| Configuración de bandas de RX | — | — | Parámetros de banda almacenados para la ruta de RX. | `ClientEqRxBands` |
| Configuración de bandas de TX | — | — | Parámetros de banda almacenados para la ruta de TX. | `ClientEqTxBands` |

## Consejos

- El área de curva tiene 110 px de alto y muestra un rango vertical de ±18 dB. Si se eliminan todas las bandas, el applet muestra "(no bands — add one in the editor)" como recordatorio de que el editor flotante es el único lugar para agregar bandas.
- Cada ruta tiene su propio mosaico de applet. Haga doble clic en la etapa de EQ en la cadena de RX para editar las bandas de RX; haga doble clic en la de la cadena de TX para editar las bandas de TX. No existe un selector interno de RX/TX dentro del propio applet.
- También puede hacer clic derecho en la barra de título del subcontenedor CEQ para acceder a opciones que permiten flotar, extraer u ocultar el mosaico del applet.

## Relacionados

- [Descripción general del EQ paramétrico (cliente)](overview.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Alternar entre la visualización del EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
