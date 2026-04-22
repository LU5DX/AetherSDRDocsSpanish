# Verificar que la curva resultante coincida con el objetivo previsto

Use el área de analizador/curva del ClientEqApplet para confirmar que el efecto combinado de todas sus bandas de EQ produce la respuesta en frecuencia que tenía en mente, tanto para la ruta RX como para la ruta TX.

## Antes de comenzar

- El applet CEQ debe estar visible. Permanece oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN o el editor flotante.
- Al menos una banda debe estar configurada en el editor flotante para que la respuesta de EQ resultante no sea plana.

## Pasos

1. Localice el subcontenedor CEQ dentro del contenedor padre PooDoo Audio (TXDSP) en el panel de applets.
2. Haga clic en la pestaña **RX** para inspeccionar el EQ de la ruta de recepción, o haga clic en la pestaña **TX** para inspeccionar el EQ de la ruta de transmisión.
3. Observe el área de analizador/curva — la pantalla de 110 px de alto que ocupa la parte inferior del applet.
4. Lea la línea de respuesta de EQ resultante. Muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas para la ruta seleccionada, trazada sobre una cuadrícula de frecuencia que abarca de 20 Hz a 20 kHz y un rango vertical de ±18 dB.
5. Compare la forma de la curva con el objetivo previsto. Las líneas de referencia horizontales de dB aparecen en 0, ±6 y ±12 dB como marcadores de referencia. Las líneas de frecuencia aparecen en 20, 50, 100, 200, 500, 1k, 2k, 5k, 10k y 20k Hz.
6. Si la curva no coincide con el objetivo, haga doble clic en la etapa de EQ en el widget CHAIN para abrir el editor flotante y ajustar las bandas. Vuelva al applet para verificar nuevamente después de cada cambio.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| RX | Pestaña | Activado | Vincula el área de analizador/curva al EQ de la ruta de recepción. | — |
| TX | Pestaña | Desactivado | Vincula el área de analizador/curva al EQ de la ruta de transmisión. | — |
| Área de analizador/curva | Indicador (solo lectura) | — | Muestra la respuesta de EQ resultante para la ruta seleccionada superpuesta con un analizador FFT en tiempo real. Eje de frecuencia: 20 Hz–20 kHz (logarítmico). Eje vertical: ±18 dB. | — |

Configuraciones guardadas que afectan lo que refleja la curva:

| Clave de configuración | Qué controla |
|---|---|
| `ClientEqRxEnabled` | Si la etapa de EQ de RX está activa |
| `ClientEqTxEnabled` | Si la etapa de EQ de TX está activa |
| `ClientEqRxBands` | Parámetros de banda guardados para la ruta RX |
| `ClientEqTxBands` | Parámetros de banda guardados para la ruta TX |

## Consejos

- El área de analizador/curva es de solo lectura. Toda la edición — agregar, eliminar y ajustar bandas — se realiza en el ClientEqEditor flotante, no en el applet.
- La superposición del analizador FFT en tiempo real muestra el audio que fluye realmente por la ruta seleccionada después del EQ. Si la superposición está inactiva, en ese momento no pasa audio por esa ruta.
- La línea de referencia de 0 dB se dibuja ligeramente más brillante que las demás líneas de cuadrícula de dB, lo que facilita identificar de un vistazo la simetría de realce y corte.
- Haga clic derecho en la barra de título del subcontenedor CEQ para flotar o extraer el applet si desea colocarlo junto al editor flotante.

## Solución de problemas

- **El área de analizador/curva no es visible** — El applet CEQ se oculta hasta que la etapa de EQ esté habilitada. Habilite la etapa de EQ desde el widget CHAIN o el editor flotante y, a continuación, compruebe que el panel de applets sea visible mediante `View > Applet Panel`.
- **La línea de respuesta resultante es plana** — No hay bandas habilitadas para la ruta seleccionada, o todas las bandas tienen una ganancia de 0 dB. Abra el editor flotante para confirmar que los ajustes de banda estén guardados en `ClientEqRxBands` o `ClientEqTxBands` para la ruta que está visualizando.
- **La curva muestra una forma, pero omitir la etapa de EQ suena idéntico** — Es posible que `ClientEqRxEnabled` o `ClientEqTxEnabled` estén desactivados. Verifique que la etapa de EQ no esté en bypass en el widget CHAIN.

## Relacionados

- [Descripción general del EQ paramétrico (cliente)](overview.md)
- [Abrir el editor flotante para agregar, eliminar y ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Alternar entre la visualización del EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Ver el espectro en tiempo real de la ruta seleccionada](see-the-live-spectrum-of-the-selected-path.md)
- [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
