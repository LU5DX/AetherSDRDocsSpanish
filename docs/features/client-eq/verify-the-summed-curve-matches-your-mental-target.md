# Verifique que la curva sumada coincide con su objetivo

El área del analizador / curva en el applet ClientEq muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas para una ruta, junto con un FFT en vivo del audio que la atraviesa. Use esta vista para confirmar que lo que ha construido en el editor produce la forma que tenía prevista.

## Antes de comenzar

- La etapa de EQ debe estar habilitada. El applet permanece oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN o el editor flotante.
- Al menos una banda debe estar configurada para la ruta correspondiente. El área de curva muestra "(no bands — add one in the editor)" cuando no existe ninguna banda.
- Abra primero el editor flotante si aún necesita agregar o ajustar bandas. Consulte [Abrir el editor flotante para agregar / eliminar / ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md).

## Pasos

1. Localice el subcontenedor CEQ dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Observe el área del analizador / curva. La curva de respuesta EQ sumada se dibuja sobre la superposición del analizador FFT en vivo.
3. Compruebe que la curva sube y baja en las frecuencias esperadas. El rango vertical es de ±18 dB. Las líneas de cuadrícula aparecen en ±6 dB y ±12 dB; la línea de referencia de 0 dB se dibuja ligeramente más brillante. Las líneas de cuadrícula de frecuencia están etiquetadas a lo largo de la parte inferior en 20, 50, 100, 200, 500, 1k, 2k, 5k, 10k y 20k Hz.
4. Si está verificando la ruta RX, confirme que la instancia RX está vinculada. Si está verificando la ruta TX, confirme que la instancia TX está vinculada. Cada tile CEQ está vinculado a una sola ruta al momento de su creación: los tiles RX muestran únicamente la respuesta RX; los tiles TX muestran únicamente la respuesta TX. Consulte [Alternar entre la visualización del EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md) si necesita ver la otra ruta.
5. Compare la forma de la curva sumada con su objetivo. Si la forma es incorrecta, regrese al editor flotante para ajustar los parámetros de las bandas.
6. Mientras el audio atraviesa la ruta, observe la superposición del analizador en vivo (la región rellena con gradiente cian). Confirme que el espectro post-EQ coincide con la conformación de la curva sumada.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|---|
| Área del analizador / curva | Indicador | Muestra la cuadrícula, la respuesta EQ sumada para la ruta vinculada y una superposición del analizador FFT en vivo. Solo lectura; 110 px de alto. | — | — |
| Respuesta EQ sumada | Estado del indicador | Respuesta en frecuencia acumulada de todas las bandas habilitadas. Muestra "flat" cuando ninguna banda aporta realce o corte; "shaped" cuando las bandas están activas. | flat | `ClientEqRxBands` / `ClientEqTxBands` |
| Superposición del analizador en vivo | Estado del indicador | FFT en tiempo real del audio que atraviesa la ruta vinculada. "idle" cuando no hay audio presente; "running" cuando fluye audio. | idle | — |

## Sugerencias

- Si el área de curva muestra "(no EQ connected)", el applet no ha sido vinculado a un motor de audio. Asegúrese de que la radio esté conectada y de que la etapa de EQ esté habilitada.
- La curva sumada se dibuja usando una referencia de prototipo analógico a lo largo del lienzo completo de 20 Hz–20 kHz, por lo que representa la respuesta ideal que los filtros digitales aproximan. Las pequeñas desviaciones entre la curva y el audio medido son normales cerca de la frecuencia de Nyquist.
- El FFT en vivo refleja el audio posterior al EQ. Si la forma del FFT no sigue la curva sumada, compruebe que la etapa de EQ no esté puenteada en la cadena. Consulte [Puentear la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).

## Solución de problemas

- **El área de curva muestra "(no bands — add one in the editor)"** — No se han agregado bandas para la ruta vinculada. Abra el editor flotante y agregue al menos una banda.
- **El área de curva muestra "(no EQ connected)"** — El applet no está vinculado al motor de audio. Verifique que la radio esté conectada y que la etapa de EQ esté habilitada mediante el widget CHAIN.
- **La superposición del analizador en vivo está ausente o vacía** — No hay audio atravesando la ruta, o el FFT aún no ha recibido datos. Transmita o reciba una señal y la superposición se completará.
- **La curva sumada aparece plana a pesar de que las bandas están configuradas** — Es posible que la etapa de EQ esté puenteada. Compruebe el widget CHAIN y confirme que `ClientEqRxEnabled` o `ClientEqTxEnabled` esté activo para la ruta correspondiente.

## Temas relacionados

- [Abrir el editor flotante para agregar / eliminar / ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Ver el espectro en vivo de la ruta seleccionada](see-the-live-spectrum-of-the-selected-path.md)
- [Alternar entre la visualización del EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Puentear la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
