# Abrir el editor flotante para agregar / eliminar / ajustar bandas

La ventana flotante ClientEqEditor es donde se agregan, eliminan y ajustan las bandas de EQ individuales para las rutas de RX y TX. La vista compacta del applet es de solo lectura; toda la edición de bandas ocurre en esta ventana separada.

## Antes de comenzar

- El subcontenedor CEQ debe estar visible dentro del contenedor padre PooDoo Audio (TXDSP). Si está oculto, habilite la etapa de EQ a través del widget CHAIN primero.
- Localice el widget CHAIN para la ruta de audio que desea editar (RX o TX).

## Pasos

1. En el widget CHAIN, haga doble clic en la etapa de EQ para abrir la ventana flotante ClientEqEditor.

Esa es la única forma admitida de abrir el editor. El applet en sí no contiene un botón de edición; tanto la omisión (bypass) como la apertura del editor se gestionan desde el widget CHAIN.

## Qué hace cada control

| Control | Tipo | Predeterminado | Configuración persistida |
|---|---|---|---|
| RX | Pestaña | Activado | — |
| TX | Pestaña | Desactivado | — |
| Área del analizador / curva | Indicador (solo lectura) | — | — |
| Estado habilitado del EQ de RX | — | — | `ClientEqRxEnabled` |
| Estado habilitado del EQ de TX | — | — | `ClientEqTxEnabled` |
| Configuración de bandas de RX | — | — | `ClientEqRxBands` |
| Configuración de bandas de TX | — | — | `ClientEqTxBands` |

El área del analizador / curva tiene 110 px de alto y muestra la respuesta de EQ sumada para la ruta seleccionada, superpuesta con un analizador FFT en tiempo real. Es de solo lectura; utilice el editor flotante para todos los cambios de banda.

## Consejos

- El applet CEQ comienza oculto y solo se vuelve visible después de que la etapa de EQ se habilita a través del widget CHAIN o del editor flotante.
- La pestaña RX está seleccionada de forma predeterminada. Si desea editar la ruta de TX, haga clic en TX en el applet antes de abrir el editor para que el área de curva refleje la ruta correcta.
- Haga clic derecho en la barra de título del subcontenedor CEQ para ver opciones de flotar, extraer u ocultar el panel del applet.

## Solución de problemas

- **Hacer doble clic en la etapa de EQ en el widget CHAIN no hace nada** — El subcontenedor CEQ puede estar oculto. Verifique que la etapa de EQ esté habilitada en el widget CHAIN; el applet debe estar activo antes de que el editor pueda abrirse.
- **El applet CEQ no está visible** — Permanece oculto hasta que la etapa de EQ se activa. Habilite la etapa desde el widget CHAIN para que el subcontenedor CEQ aparezca.

## Relacionados

- [Descripción general del EQ paramétrico (cliente)](overview.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Cambiar entre la vista de EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Ver el espectro en tiempo real de la ruta seleccionada](see-the-live-spectrum-of-the-selected-path.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
