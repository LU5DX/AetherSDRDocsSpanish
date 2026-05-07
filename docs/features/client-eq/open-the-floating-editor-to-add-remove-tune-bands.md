# Abra el editor flotante para añadir, eliminar o sintonizar bandas

El ClientEqEditor flotante es donde usted añade, elimina y sintoniza bandas de ecualización para las rutas RX y TX. El applet compacto en el panel muestra el resultado; la edición siempre ocurre en esta ventana separada.

## Antes de comenzar

- El applet CEQ debe estar visible en el panel de applets. Está oculto hasta que la etapa EQ se habilite a través del widget CHAIN.
- Localice el mosaico de la etapa EQ en el widget CHAIN para la ruta que desea editar (RX o TX).

## Pasos

1. Encuentre la etapa EQ en el widget CHAIN para la ruta que desea moldear (cadena RX para recepción, cadena TX para transmisión).
2. Haga doble clic en la etapa EQ en el widget CHAIN.
3. Se abre la ventana flotante ClientEqEditor. Añada, elimine o sintonice bandas allí.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Clave de ajuste |
|---|---|---|---|---|
| RX | Pestaña | Marcado | Vincula el widget de curva a la instancia EQ de RX. | — |
| TX | Pestaña | Sin marcar | Vincula el widget de curva a la instancia EQ de TX. | — |
| Área de analizador/curva | Indicador | — | Muestra la respuesta EQ sumada y una superposición FFT en vivo para la ruta seleccionada. Solo visualización; la edición requiere el editor flotante. | — |
| Estado habilitado de RX | — | — | Indica si la etapa EQ de RX está activa. | `ClientEqRxEnabled` |
| Estado habilitado de TX | — | — | Indica si la etapa EQ de TX está activa. | `ClientEqTxEnabled` |
| Configuración de bandas de RX | — | — | Parámetros de banda almacenados para la ruta RX. | `ClientEqRxBands` |
| Configuración de bandas de TX | — | — | Parámetros de banda almacenados para la ruta TX. | `ClientEqTxBands` |

## Consejos

- El área de curva tiene 110 px de alto y muestra un rango vertical de ±18 dB. Si se eliminan todas las bandas, el applet muestra "(sin bandas — añada una en el editor)" como recordatorio de que el editor flotante es el único lugar para añadir bandas.
- Cada ruta tiene su propio mosaico de applet. Haga doble clic en la etapa EQ de la cadena RX para editar bandas RX; haga doble clic en la de la cadena TX para editar bandas TX. No hay un selector interno RX/TX dentro del propio applet.
- También puede hacer clic derecho en la barra de título del subcontenedor CEQ para ver opciones de flotar, desacoplar u ocultar el mosaico del applet.

## Relacionado

- [Descripción general del EQ paramétrico (Cliente)](overview.md)
- [Omita la etapa EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Cambie entre la visualización de EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Verifique que la curva sumada coincida con su objetivo mental](verify-the-summed-curve-matches-your-mental-target.md)
