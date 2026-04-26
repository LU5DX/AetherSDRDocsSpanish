# Ver el espectro en vivo de la ruta seleccionada

La superposición del analizador en el ClientEqApplet muestra una FFT en tiempo real del audio que pasa por la ruta vinculada actualmente (RX o TX), dibujada sobre la curva de respuesta de EQ sumada. Úsela para confirmar el aspecto real del audio tras la ecualización, sin necesidad de abrir el editor flotante.

## Antes de comenzar

- El ClientEqApplet (etiquetado "CEQ") debe estar visible. Permanece oculto hasta que la etapa de EQ se habilita mediante el widget CHAIN o el editor flotante. Consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md) si el applet no aparece.
- El audio debe estar fluyendo por la ruta seleccionada para que la superposición del analizador muestre algo distinto al estado inactivo.

## Pasos

1. Localice el subcontenedor "CEQ" dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. El área del analizador/curva se actualiza automáticamente — no se requiere ninguna acción para iniciarlo. La superposición de FFT en vivo aparece como un degradado cian relleno sobre la cuadrícula cuando hay audio presente en la ruta vinculada.
3. Para ver el espectro de la otra ruta, cambie la ruta vinculada seleccionando el mosaico de cadena correspondiente. Cada instancia del applet CEQ está fijada a RX o TX en el momento de su creación; no hay un selector RX/TX dentro del propio applet. Consulte [Cambiar entre ver el EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md).

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Área de analizador/curva | Indicador (solo visualización) | — | Muestra una superposición de analizador FFT en vivo (degradado cian relleno, 20 Hz–20 kHz, escala de −70 dB a 0 dB) y la respuesta de EQ sumada para la ruta vinculada. La edición se realiza en el ClientEqEditor flotante, no aquí. |
| Respuesta de EQ sumada | Indicador | Plana (sin bandas) | Muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas. Muestra "(no bands — add one in the editor)" cuando no existen bandas, o "(no EQ connected)" si el applet no tiene un EQ vinculado. |
| Superposición del analizador en vivo | Indicador | Inactivo | FFT en tiempo real del audio que pasa por la ruta vinculada, dibujada bajo la curva de EQ. Activa únicamente cuando hay audio fluyendo. |

Configuraciones persistentes que afectan lo que se muestra: `ClientEqRxEnabled`, `ClientEqTxEnabled`, `ClientEqRxBands`, `ClientEqTxBands`.

## Consejos

- La cuadrícula de frecuencias va de 20 Hz a 20 kHz en escala logarítmica. Las líneas de cuadrícula de dB aparecen en ±6 dB y ±12 dB, con una línea de referencia de 0 dB más brillante en el centro.
- La superposición del analizador se dibuja bajo la curva de EQ y los indicadores por banda, de modo que la respuesta sumada permanece legible incluso cuando hay señal presente.
- La FFT cubre solo hasta la frecuencia de Nyquist de la ruta de audio; no se dibuja contenido por encima de ese punto, por lo que un espacio en el extremo superior de la pantalla es normal.
- El applet mide 110 px de alto y es solo de visualización. Para agregar, eliminar o ajustar bandas, haga doble clic en la etapa de EQ en el widget CHAIN para abrir el editor flotante.

## Solución de problemas

- **La superposición del analizador no es visible** — Confirme que el audio esté fluyendo activamente por la ruta vinculada. Si la ruta está inactiva (sin audio de recepción ni transmisión activa), la FFT no tiene señal que mostrar y la superposición no aparecerá.
- **La pantalla muestra "(no EQ connected)"** — El applet no ha sido vinculado a una instancia del motor de audio. Asegúrese de que la etapa de EQ esté habilitada mediante el widget CHAIN para que el applet se inicialice correctamente.
- **La pantalla muestra "(no bands — add one in the editor)"** — No se han configurado bandas de EQ para esta ruta. Abra el editor flotante para agregar al menos una banda. Consulte [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md).
- **El subcontenedor CEQ no es visible** — El applet se oculta a sí mismo hasta que la etapa de EQ está habilitada. Consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).

## Relacionado

- [Cambiar entre ver el EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
- [Verificar que la curva sumada coincida con el objetivo previsto](verify-the-summed-curve-matches-your-mental-target.md)
- [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
