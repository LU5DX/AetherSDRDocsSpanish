# Grabar hasta 30 segundos de audio TX posterior a PUDU

Use el grabador de monitor integrado para capturar y reproducir inmediatamente cómo suena su audio transmitido después de haber pasado por la cadena DSP TX completa, incluyendo PUDU. Esto le permite ajustar la configuración de su cadena sin necesitar una segunda estación que le informe los resultados.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar abierto. Si no está visible, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha.
- La entrada de micrófono debe estar configurada en **PC** (no en una fuente de micrófono del panel frontal del radio).
- DAX debe estar desactivado. El tooltip del botón de grabación indica: "MIC must be set to PC and DAX off."
- La pestaña **TX** debe estar activa en el applet. Los controles de grabación están ocultos cuando se selecciona **RX**.

## Pasos

1. Haga clic en el botón de pestaña **TX** en la parte superior del applet Aetherial Audio Chain para asegurarse de que se muestra la cadena TX. El botón se vuelve ámbar al seleccionarlo.
2. Confirme que el botón de grabación (⏺) está habilitado. Solo se habilita cuando la entrada de micrófono está lista y la reproducción no está en curso. Si aparece atenuado y no se puede hacer clic, verifique que la fuente de micrófono esté configurada en PC y que DAX esté desactivado.
3. Haga clic en **⏺** para iniciar la grabación. El botón parpadea en rojo para indicar que la captura está activa. La grabación se detiene automáticamente después de 30 segundos, o puede detenerla antes.
4. Para detener la grabación antes de que transcurran los 30 segundos, haga clic en **⏺** nuevamente. La reproducción comienza automáticamente una vez que la grabación se detiene.
5. Para cancelar la reproducción antes de que finalice, haga clic en **▶** mientras parpadea en verde.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **⏺** (grabar) | Sin marcar | Captura hasta 30 s de audio TX posterior a PUDU. Haga clic nuevamente para detener; la reproducción comienza automáticamente. |
| **▶** (reproducir) | Sin marcar | Reproduce el audio capturado. Haga clic nuevamente para cancelar. |
| Etapa de cadena RX (EQ / AGC-T / AGC-C / TUBE / PUDU) | — | Un clic alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. Las cinco etapas RX (EQ, AGC-T/Gate, AGC-C/Comp, Tube, PUDU) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita que se produzcan sueltas accidentales entre las dos tiras. |

## Sugerencias

- El grabador captura el audio en el punto posterior a la etapa PUDU en la cadena TX. Para escuchar el efecto de una etapa específica, active o desactive su bypass, realice una grabación y compare la reproducción.
- No es necesario transmitir hacia un receptor: el monitor graba el audio directamente desde la salida DSP del lado del cliente.
- Si desea comparar configuraciones, detenga la grabación actual, ajuste una etapa, grabe nuevamente y reproduzca para comparar.

## Solución de problemas

- **El botón ⏺ está atenuado y no se puede hacer clic** — La entrada de micrófono no está configurada en PC, DAX está activado o la reproducción está en curso. Desactive DAX, configure la fuente de micrófono en PC y espere a que finalice cualquier reproducción activa.
- **Los botones ⏺ y ▶ no son visibles** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la cadena TX; ambos botones están ocultos en el modo RX.
- **La reproducción no comienza después de que la grabación se detiene** — No se capturó audio. Confirme que su entrada de micrófono está enviando audio a la PC durante la ventana de grabación.

## Relacionados

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
