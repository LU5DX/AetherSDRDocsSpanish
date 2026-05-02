# Reproducir el audio PUDU capturado

Esta página explica cómo reproducir el audio que ya grabó con el monitor TX post-PUDU. Úselo para escuchar exactamente cómo suena su señal transmitida después de que la cadena TX DSP completa la ha procesado.

## Antes de comenzar

- Debe existir una grabación previa. El botón Play (▶) solo se habilita cuando existe una grabación.
- La grabación no debe estar activa en ese momento. El botón Play (▶) está deshabilitado mientras el botón Record (⏺) esté activado.
- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado como `PUDU` en la barra lateral derecha para mostrarlo.
- La cadena TX debe ser la vista activa. El botón Play (▶) está oculto en modo RX.

## Pasos

1. En la fila de encabezado de ClientChainApplet, confirme que el botón **TX** esté seleccionado. Si no lo está, haga clic en **TX**.
2. Haga clic en el botón **Play (▶)**.
   - El botón pulsa en verde mientras la reproducción está en curso.
3. Para detener la reproducción antes de que finalice, haga clic nuevamente en el botón **Play (▶)**.

## Qué hace cada control

| Control                                              | Comportamiento                                                                                                                                 | Notas                                                                                                                                                                                                                                                                  |
|------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Play (▶)**                                         | Inicia la reproducción del audio PUDU capturado; haga clic de nuevo para cancelar.                                                             | Oculto en modo RX. Se habilita solo cuando existe una grabación y la grabación no está activa. Pulsa en verde durante la reproducción.                                                                                                                                 |
| **Record (⏺)**                                       | Deshabilitado durante la reproducción.                                                                                                         | Se vuelve a habilitar automáticamente cuando la reproducción finaliza.                                                                                                                                                                                                 |
| Etapa de cadena RX (EQ / AGC-T / AGC-C / TUBE / PUDU) | Un clic alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las cinco etapas RX (EQ, AGC-T/Gate, AGC-C/Comp, Tube, PUDU) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distintivo `application/x-aethersdr-rx-chain-stage` evita arrastres accidentales entre las dos tiras. |

## Consejos

- El botón Play (▶) permanece habilitado mientras la reproducción está en curso, por lo que puede cancelarla en cualquier momento haciendo clic en él nuevamente.
- Si desea una nueva grabación antes de escuchar, haga clic en **Record (⏺)** para capturar hasta 30 segundos de audio TX post-PUDU. La reproducción comienza automáticamente cuando la grabación se detiene.
- El botón Play (▶) está oculto siempre que la pestaña **RX** esté activa. Vuelva a **TX** para acceder a él.

## Solución de problemas

- **Play (▶) aparece en gris** — Aún no existe ninguna grabación, o la grabación está en curso. Realice primero una grabación usando **Record (⏺)**, o espere a que finalice la grabación actual.
- **Play (▶) no es visible** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la vista de cadena TX.

## Relacionados

- [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
