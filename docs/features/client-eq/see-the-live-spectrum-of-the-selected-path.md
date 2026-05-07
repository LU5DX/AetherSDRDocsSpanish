# Ver el espectro en vivo de la ruta seleccionada

La superposición del analizador en el ClientEqApplet muestra una FFT en tiempo real del audio que pasa por la ruta actualmente vinculada (RX o TX), dibujada sobre la curva de respuesta del ecualizador sumada. Úselo para confirmar cómo se ve realmente el audio después de la ecualización, sin necesidad de abrir el editor flotante.

## Antes de comenzar

- El ClientEqApplet (etiquetado como "CEQ") debe estar visible. Está oculto hasta que la etapa de ecualización se habilite a través del widget CHAIN o del editor flotante. Consulte [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md) si el applet no se muestra.
- Debe haber audio fluyendo a través de la ruta seleccionada para que la superposición del analizador muestre algo diferente al estado inactivo.

## Pasos

1. Localice el subcontenedor "CEQ" dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. El área del analizador / curva se actualiza automáticamente — no se requiere ninguna acción para iniciarla. La superposición FFT en vivo aparece como un relleno de degradado cian sobre la cuadrícula siempre que haya audio presente en la ruta vinculada.
3. Para ver el espectro de la otra ruta, cambie la ruta vinculada seleccionando el mosaico de cadena correspondiente. Cada instancia del applet CEQ está fijada a RX o TX en el momento de la construcción; no hay un selector RX / TX dentro del applet. Consulte [Switch between viewing RX and TX EQ](switch-between-viewing-rx-and-tx-eq.md).

## Función de cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Área del analizador / curva | Indicador (solo visualización) | — | Muestra una superposición del analizador FFT en vivo (degradado cian relleno, 20 Hz–20 kHz, escala de −70 dB a 0 dB) y la respuesta del ecualizador sumada para la ruta vinculada. La edición se realiza en el ClientEqEditor flotante, no aquí. |
| Respuesta del ecualizador sumada | Indicador | Plana (sin bandas) | Muestra la respuesta de frecuencia acumulativa de todas las bandas habilitadas. Muestra "(no bands — add one in the editor)" cuando no existen bandas, o "(no EQ connected)" si el applet no tiene un ecualizador vinculado. |
| Superposición del analizador en vivo | Indicador | Inactivo | FFT en tiempo real del audio que pasa por la ruta vinculada, dibujada debajo de la curva del ecualizador. Activa solo cuando hay audio fluyendo. |

Configuraciones persistentes que afectan lo que se muestra: `ClientEqRxEnabled`, `ClientEqTxEnabled`, `ClientEqRxBands`, `ClientEqTxBands`.

## Consejos

- La cuadrícula de frecuencia va de 20 Hz a 20 kHz en una escala logarítmica. Las líneas de cuadrícula de dB aparecen a ±6 dB y ±12 dB, con una línea de referencia de 0 dB más brillante en el centro.
- La superposición del analizador se dibuja debajo de la curva del ecualizador y de los indicadores por banda, por lo que la respuesta sumada sigue siendo legible incluso cuando hay señal presente.
- La FFT solo cubre hasta la frecuencia de Nyquist de la ruta de audio; no se dibuja contenido por encima de ese punto, por lo que un espacio en el extremo superior de la pantalla es normal.
- El applet tiene 110 px de alto y es solo de visualización. Para agregar, eliminar o ajustar bandas, haga doble clic en la etapa de ecualización en el widget CHAIN para abrir el editor flotante.

## Solución de problemas

- **La superposición del analizador no es visible** — Confirme que el audio esté fluyendo activamente a través de la ruta vinculada. Si la ruta está inactiva (sin audio de recepción o sin transmisión activa), la FFT no tiene señal para mostrar y la superposición no aparecerá.
- **La pantalla muestra "(no EQ connected)"** — El applet no se ha vinculado a una instancia del motor de audio. Asegúrese de que la etapa de ecualización esté habilitada a través del widget CHAIN para que el applet se inicialice correctamente.
- **La pantalla muestra "(no bands — add one in the editor)"** — No se han configurado bandas de ecualización para esta ruta. Abra el editor flotante para agregar al menos una banda. Consulte [Open the floating editor to add / remove / tune bands](open-the-floating-editor-to-add-remove-tune-bands.md).
- **El subcontenedor CEQ no es visible** — El applet se oculta hasta que la etapa de ecualización esté habilitada. Consulte [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md).

## Relacionados

- [Switch between viewing RX and TX EQ](switch-between-viewing-rx-and-tx-eq.md)
- [Verify the summed curve matches your mental target](verify-the-summed-curve-matches-your-mental-target.md)
- [Open the floating editor to add / remove / tune bands](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Bypass the EQ stage from the chain](bypass-the-eq-stage-from-the-chain.md)
