# Verifique que la curva sumada coincide con su objetivo mental

Después de ajustar las bandas en el editor de EQ paramétrico, use los mosaicos del applet para confirmar que la curva de respuesta de EQ sumada refleja la forma general que tenía prevista, con la superposición del analizador en vivo mostrando cómo el audio real se alinea con ella.

## Antes de comenzar

- La etapa de EQ que desea verificar debe estar habilitada. Si el mosaico "Aetherial TX EQ" o "Aetherial RX EQ" está oculto, habilite la etapa de EQ correspondiente mediante el widget CHAIN primero.
- Las bandas ya deben estar configuradas. Si todavía no ha agregado ni ajustado bandas, consulte [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Pasos

1. Ubique el subcontenedor "Aetherial TX EQ" o "Aetherial RX EQ" dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Observe el área de la curva: la pantalla de 110 px de alto que muestra una cuadrícula, la respuesta de EQ sumada y la superposición del analizador FFT en vivo.
3. Trace la curva de respuesta de EQ sumada a lo largo del eje de frecuencia. Refleja la respuesta acumulada de todas las bandas habilitadas para esa ruta.
4. Compare la forma de la curva con su objetivo previsto. Los picos, los estantes (shelves) y los cortes paso-alto o paso-bajo aparecen como desviaciones respecto a una línea plana.
5. Observe la superposición del analizador en vivo mientras el audio pasa por la cadena. La superposición muestra el FFT en tiempo real del audio en esa ruta, lo que le permite confirmar que la respuesta modelada está afectando el espectro como se esperaba.
6. Si la curva no coincide con su objetivo, haga doble clic en la etapa de EQ en el widget CHAIN para reabrir el editor sin marco ("Aetherial Parametric EQ — TX" o "— RX") y ajuste las bandas allí.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| Área del analizador / curva | Muestra la cuadrícula, la respuesta de EQ sumada y la superposición del analizador FFT en vivo para la ruta fija del mosaico (TX o RX). | Solo lectura en el mosaico del applet. La edición requiere el editor flotante. |
| Respuesta de EQ sumada | La respuesta en frecuencia acumulada de todas las bandas habilitadas en esta ruta. Aparece plana cuando ninguna banda altera la respuesta; modelada cuando una o más bandas están activas. | Se conserva mediante `ClientEqTxBands` (TX) o `ClientEqRxBands` (RX). |
| Superposición del analizador en vivo | FFT en tiempo real del audio que pasa por esta ruta. Aparece inactiva cuando no hay audio presente, y en funcionamiento cuando el audio está activo. | Proporciona confirmación visual de que la curva está afectando la señal real. |

## Consejos

- El mosaico del applet es solo de lectura. No se realiza ninguna edición aquí. Todos los cambios de banda deben hacerse en el editor sin marco abierto desde el widget CHAIN.
- Hay un mosaico por lado. "Aetherial TX EQ" está fijo a la ruta TX; "Aetherial RX EQ" está fijo a la ruta RX. No comparten un selector.
- Si la curva aparece plana pero espera que tenga forma, verifique si la etapa de EQ está en derivación (bypass). Una etapa en derivación no aplica sus bandas a la ruta de audio aunque la pantalla de la curva pueda seguir mostrando la forma. Consulte [Poner en derivación la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).

## Solución de problemas

- **El mosaico del applet no es visible** — La etapa de EQ no está habilitada. Habilítela mediante el widget CHAIN o el editor flotante. El mosaico permanece oculto hasta que la etapa correspondiente esté activa.
- **La curva sumada está plana a pesar de tener bandas configuradas** — Es posible que todas las bandas tengan una ganancia de 0 dB, o que la etapa de EQ esté en derivación. Abra el editor sin marco para inspeccionar la configuración individual de cada banda, o verifique el estado de derivación en el widget CHAIN.
- **La superposición del analizador en vivo está inactiva** — No está pasando audio por esa ruta. Para RX, asegúrese de que el radio esté recibiendo y de que el enrutamiento de audio esté activo. Para TX, asegúrese de que se esté procesando una señal a través de la cadena TX DSP.

## Relacionados

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva de EQ TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Poner en derivación la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
