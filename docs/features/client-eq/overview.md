# Descripción general del EQ paramétrico (cliente)

La función de EQ paramétrico (cliente) proporciona un ecualizador paramétrico del lado del cliente para las rutas de audio de recepción y transmisión. Úselo para moldear la respuesta en frecuencia del audio que pasa por AetherSDR sin modificar la cadena DSP propia del radio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar el EQ, pero se necesita una ruta de audio activa para que la superposición del analizador muestre señal.
- El applet de EQ está oculto de forma predeterminada. Habilite la etapa de EQ desde el widget CHAIN o el editor flotante para hacer visible el applet.

## Cómo funciona

AetherSDR ejecuta una instancia de EQ para la ruta de recepción y otra para la ruta de transmisión. Cada instancia es independiente: tiene su propio conjunto de bandas, su propio estado habilitado/omitido y su propia configuración persistida.

El subcontenedor **CEQ** se encuentra dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets. Muestra un área compacta de curva y analizador (110 px de alto) para la ruta a la que está vinculado. Hay una ficha de applet por ruta: la ficha vinculada a RX muestra el EQ de RX; la ficha vinculada a TX muestra el EQ de TX. Ninguna ficha contiene un selector de ruta interno; la pestaña del widget de cadena determina qué lado se está editando.

La edición de bandas — agregar, eliminar y ajustar — ocurre en la ventana flotante **ClientEqEditor**, no en la ficha del applet. Ábrala haciendo doble clic en la etapa de EQ en el widget CHAIN. La ficha del applet es una vista de solo lectura: muestra el estado actual de la ruta, pero no acepta clics para mover o editar bandas.

El área de curva renderiza dos capas simultáneamente:

- **Respuesta de EQ sumada** — la respuesta en frecuencia acumulada de todas las bandas habilitadas para la ruta vinculada. Cuando no hay bandas configuradas, el área muestra "(no bands — add one in the editor)". Cuando no hay EQ conectado, muestra "(no EQ connected)".
- **Superposición del analizador FFT en vivo** — una FFT en tiempo real del audio que pasa por la ruta vinculada, dibujada como un degradado cian relleno. La escala vertical va de −70 dB en la parte inferior a 0 dB en la parte superior. La escala horizontal es logarítmica de 20 Hz a 20 kHz.

La cuadrícula de frecuencias dibuja líneas verticales en 20, 50, 100, 200, 500, 1k, 2k, 5k, 10k y 20k Hz. Las líneas de referencia de dB horizontales aparecen en ±6 dB y ±12 dB, con una línea más brillante en 0 dB.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| Pestaña RX | Pestaña | Activada | Vincula el widget de curva a la instancia de EQ de RX. Mutuamente exclusiva con TX. | — |
| Pestaña TX | Pestaña | Desactivada | Vincula el widget de curva a la instancia de EQ de TX. Mutuamente exclusiva con RX. | — |
| Área de analizador / curva | Indicador (solo lectura) | — | Muestra la respuesta de EQ sumada y la superposición del analizador FFT en vivo para la ruta seleccionada. La edición se realiza en el ClientEqEditor flotante. | — |
| `ClientEqRxEnabled` | Configuración persistida | — | Almacena el estado habilitado/omitido del EQ de RX. | `ClientEqRxEnabled` |
| `ClientEqTxEnabled` | Configuración persistida | — | Almacena el estado habilitado/omitido del EQ de TX. | `ClientEqTxEnabled` |
| `ClientEqRxBands` | Configuración persistida | — | Almacena la configuración de bandas del EQ de RX. | `ClientEqRxBands` |
| `ClientEqTxBands` | Configuración persistida | — | Almacena la configuración de bandas del EQ de TX. | `ClientEqTxBands` |

## Consejos

- Haga clic derecho en la barra de título del subcontenedor **CEQ** para flotar, desprender u ocultar la ficha del applet si necesita más espacio en pantalla.
- La respuesta de EQ sumada se calcula a partir de funciones de transferencia de prototipo analógico en el rango completo de 20 Hz a 20 kHz. La curva es una referencia ideal; la ruta de audio utiliza los biquads digitales equivalentes.
- Los colores de las bandas siguen una paleta fija (gris, ámbar, amarillo, verde, verde azulado, azul, púrpura, gris). Con más de 8 bandas, los colores se repiten cíclicamente en lugar de reiniciarse desde el gris.

## Relacionados

- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Abrir el editor flotante para agregar, eliminar y ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Ver el espectro en vivo de la ruta seleccionada](see-the-live-spectrum-of-the-selected-path.md)
- [Cambiar entre la visualización del EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
