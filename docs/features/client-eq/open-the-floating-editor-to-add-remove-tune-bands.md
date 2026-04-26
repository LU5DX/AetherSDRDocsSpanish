# Abrir el editor flotante para agregar / eliminar / ajustar bandas

El ClientEqEditor flotante es donde se agregan, eliminan y ajustan las bandas de ecualización para las rutas de RX y TX. El applet compacto del panel muestra el resultado; la edición siempre ocurre en esta ventana separada.

## Antes de comenzar

- El applet CEQ debe estar visible en el panel de applets. Permanece oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN.
- Ubique el tile de la etapa EQ en el widget CHAIN correspondiente a la ruta que desea editar (RX o TX).

## Pasos

1. Encuentre la etapa EQ en el widget CHAIN para la ruta que desea configurar (cadena RX para recepción, cadena TX para transmisión).
2. Haga doble clic en la etapa EQ dentro del widget CHAIN.
3. Se abre la ventana flotante ClientEqEditor. Agregue, elimine o ajuste bandas allí.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de ajuste |
|---|---|---|---|---|
| RX | Pestaña | Activada | Vincula el widget de curva a la instancia de EQ de RX. | — |
| TX | Pestaña | Desactivada | Vincula el widget de curva a la instancia de EQ de TX. | — |
| Área de analizador / curva | Indicador | — | Muestra la respuesta de EQ sumada y una superposición de FFT en tiempo real para la ruta seleccionada. Solo lectura; la edición requiere el editor flotante. | — |
| Estado habilitado de RX | — | — | Indica si la etapa EQ de RX está activa. | `ClientEqRxEnabled` |
| Estado habilitado de TX | — | — | Indica si la etapa EQ de TX está activa. | `ClientEqTxEnabled` |
| Configuración de bandas de RX | — | — | Parámetros de banda almacenados para la ruta de RX. | `ClientEqRxBands` |
| Configuración de bandas de TX | — | — | Parámetros de banda almacenados para la ruta de TX. | `ClientEqTxBands` |

## Consejos

- El área de curva tiene 110 px de alto y muestra un rango vertical de ±18 dB. Si se eliminan todas las bandas, el applet muestra "(no bands — add one in the editor)" como recordatorio de que el editor flotante es el único lugar para agregar bandas.
- Cada ruta tiene su propio tile de applet. Haga doble clic en la etapa EQ de la cadena RX para editar las bandas de RX; haga doble clic en la de la cadena TX para editar las bandas de TX. No existe un selector interno de RX/TX dentro del propio applet.
- También puede hacer clic derecho en la barra de título del subcontenedor CEQ para ver opciones que permiten flotar, extraer u ocultar el tile del applet.

## Temas relacionados

- [Descripción general del EQ paramétrico (cliente)](overview.md)
- [Omitir la etapa EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Alternar entre la visualización del EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
