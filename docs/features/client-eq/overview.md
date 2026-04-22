# Descripción general del Parametric EQ (Client)

El applet Parametric EQ (Client) aplica un ecualizador paramétrico del lado del cliente a sus rutas de audio de recepción y transmisión de forma independiente. Úselo para dar forma al audio antes de que llegue a sus altavoces o a la cadena del micrófono, sin modificar el DSP propio del radio.

## Antes de comenzar

- El applet está alojado dentro del contenedor principal PooDoo Audio (TXDSP) como el subcontenedor "CEQ". Permanece oculto hasta que la etapa de EQ se habilita mediante el widget CHAIN o el editor flotante.
- No se requiere conexión con el radio para configurar el EQ.

## Cómo funciona

El applet presenta una vista compacta de una ruta de audio a la vez: ya sea RX o TX. Las pestañas **RX** y **TX** en la parte superior del applet seleccionan qué ruta se muestra. Cambiar de pestaña reasigna el área de curva a la instancia de EQ de esa ruta; no omite ni altera ninguna de las dos rutas.

El área principal del applet es la pantalla del analizador y de la curva. Tiene 110 píxeles de alto y muestra dos capas al mismo tiempo:

- **Respuesta de EQ sumada** — la respuesta en frecuencia combinada de todas las bandas habilitadas para la ruta seleccionada. La curva es plana cuando no hay bandas activas o todas están omitidas, y tiene forma cuando una o más bandas aportan ganancia o corte.
- **Superposición del analizador FFT en tiempo real** — un espectro en tiempo real del audio que fluye por la ruta seleccionada. Esta superposición está inactiva cuando no hay audio presente y en funcionamiento cuando el audio está activo.

El área de curva es solo de visualización. Para agregar, eliminar o ajustar bandas, abra el editor flotante haciendo doble clic en la etapa de EQ en el widget CHAIN.

La omisión (habilitar y deshabilitar la etapa de EQ por completo) se controla desde el widget CHAIN, no desde dentro del applet.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Ajuste persistido |
|---|---|---|---|---|
| **RX** | Pestaña | Seleccionado | Selecciona la ruta de recepción; vincula el área de curva a la instancia de EQ de RX. Mutuamente excluyente con TX. | — |
| **TX** | Pestaña | No seleccionado | Selecciona la ruta de transmisión; vincula el área de curva a la instancia de EQ de TX. Mutuamente excluyente con RX. | — |
| Área del analizador / curva | Indicador | — | Muestra la respuesta de EQ sumada y la superposición del analizador FFT en tiempo real para la ruta seleccionada. Solo de visualización. | — |
| Estado habilitado de RX | — | — | Indica si la etapa de EQ de RX está activa u omitida. Se controla mediante el widget CHAIN. | `ClientEqRxEnabled` |
| Estado habilitado de TX | — | — | Indica si la etapa de EQ de TX está activa u omitida. Se controla mediante el widget CHAIN. | `ClientEqTxEnabled` |
| Configuración de bandas de RX | — | — | Frecuencia, ganancia, Q y tipo para cada banda en la ruta de RX. Se edita en el editor flotante. | `ClientEqRxBands` |
| Configuración de bandas de TX | — | — | Frecuencia, ganancia, Q y tipo para cada banda en la ruta de TX. Se edita en el editor flotante. | `ClientEqTxBands` |

## Consejos

- El rango vertical del área de curva es ±18 dB. Las líneas de cuadrícula horizontales aparecen en ±6 dB y ±12 dB; la línea de referencia de 0 dB se dibuja ligeramente más brillante.
- Las líneas de cuadrícula de frecuencia se ubican en 20, 50, 100, 200, 500, 1k, 2k, 5k, 10k y 20k Hz.
- Las rutas de RX y TX son independientes. Cambiar la pestaña para revisar una ruta no afecta lo que hace la otra.
- Haga clic derecho en la barra de título del subcontenedor "CEQ" para flotar, extraer u ocultar el applet si necesita más espacio en pantalla.

## Relacionado

- [Cambiar entre la vista de EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Ver el espectro en tiempo real de la ruta seleccionada](see-the-live-spectrum-of-the-selected-path.md)
- [Verificar que la curva sumada coincida con su objetivo previsto](verify-the-summed-curve-matches-your-mental-target.md)
