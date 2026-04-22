# Ver el espectro en vivo de la ruta seleccionada

El área de analizador / curva del applet ClientEq muestra una FFT en tiempo real del audio que pasa por la ruta de RX o TX seleccionada, superpuesta con la respuesta de EQ sumada. Use esto para observar cómo el EQ está afectando el audio en vivo sin abrir el editor flotante.

## Antes de comenzar

- El applet CEQ debe estar visible. Permanece oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN o el editor flotante. Consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md) si el applet no se muestra.
- El audio debe estar fluyendo a través de la ruta que desea observar para que la superposición de FFT en vivo esté activa y no inactiva.

## Pasos

1. Localice el subcontenedor CEQ dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Haga clic en la pestaña **RX** para ver la ruta de recepción, o haga clic en la pestaña **TX** para ver la ruta de transmisión.
3. Observe el área de analizador / curva. La superposición de FFT en vivo aparece como un degradado relleno detrás de la curva de respuesta de EQ sumada. El eje horizontal va de 20 Hz a 20 kHz en escala logarítmica. El eje vertical abarca ±18 dB; la superposición de FFT escala desde −70 dB en la parte inferior hasta 0 dB en la parte superior.
4. Observe cómo la superposición se actualiza en tiempo real mientras el audio pasa por la ruta seleccionada.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **RX** | Pestaña | Activado | Vincula el área de analizador / curva al EQ de la ruta de recepción. Mutuamente exclusivo con TX. | — |
| **TX** | Pestaña | Desactivado | Vincula el área de analizador / curva al EQ de la ruta de transmisión. Mutuamente exclusivo con RX. | — |
| Área de analizador / curva | Indicador | — | 110 px de alto. Muestra la cuadrícula de frecuencia, la respuesta de EQ sumada para la ruta seleccionada y la superposición de FFT en vivo. Solo lectura. | — |

## Consejos

- El área de analizador / curva es solo de lectura. Para agregar, eliminar o ajustar bandas, abra el editor flotante haciendo doble clic en la etapa de EQ en el widget CHAIN.
- Haga clic derecho en la barra de título del subcontenedor CEQ para flotar o desprender el applet si desea tener el analizador visible junto a otras ventanas.
- La curva de respuesta de EQ sumada se dibuja encima de la superposición de FFT, de modo que puede comparar directamente la forma del EQ con el espectro en vivo.

## Relacionado

- [Cambiar entre la vista de EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Verificar que la curva sumada coincide con el objetivo esperado](verify-the-summed-curve-matches-your-mental-target.md)
- [Abrir el editor flotante para agregar / eliminar / ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
