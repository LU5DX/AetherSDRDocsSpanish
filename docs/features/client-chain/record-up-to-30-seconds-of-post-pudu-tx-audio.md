# Grabar hasta 30 segundos de audio TX posterior al PUDU

Use la grabadora de monitor integrada para capturar su audio TX procesado después de que pase por la etapa PUDU, luego reprodúzcalo de inmediato para evaluar la configuración de su cadena de audio.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado como **PUDU** en la barra lateral derecha para mostrarlo.
- La cadena TX debe ser la vista activa. Haga clic en **TX** en el encabezado del applet si actualmente está seleccionado **RX**.
- La fuente de micrófono debe estar configurada en PC y DAX debe estar desactivado. El botón de grabación se deshabilita cuando estas condiciones no se cumplen.

## Pasos

1. Confirme que el botón **TX** en el encabezado de Aetherial Audio Chain esté marcado. Si no lo está, haga clic en **TX**.
2. Haga clic en el botón **⏺** (Record) en la fila del encabezado, a la derecha de los selectores **TX** / **RX**. El botón parpadea en rojo para indicar que la grabación está activa.
3. Hable frente a su micrófono. La grabación se detiene automáticamente después de 30 segundos, o haga clic en **⏺** nuevamente para detenerla antes.
4. Cuando la grabación se detiene, la reproducción comienza automáticamente. El botón **▶** (Play) parpadea en verde durante la reproducción.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---|---|---|---|
| **⏺** (Record) | Inicia la captura del audio TX posterior al PUDU; haga clic nuevamente para detener antes. La reproducción comienza automáticamente cuando finaliza la grabación. | Desmarcado | Parpadea en rojo durante la grabación. Deshabilitado cuando la fuente del micrófono no es PC, DAX está activado o la reproducción está en curso. Oculto cuando **RX** es la pestaña activa. |
| **▶** (Play) | Reproduce el audio capturado; haga clic nuevamente para cancelar la reproducción. | Desmarcado | Parpadea en verde durante la reproducción. Solo se habilita una vez que existe una grabación y la grabación no está activa. Oculto cuando **RX** es la pestaña activa. |

## Consejos

- El botón **⏺** permanece habilitado durante la grabación, por lo que puede hacer clic en él para detenerla antes de alcanzar el límite de 30 segundos.
- El botón **▶** permanece habilitado durante la reproducción, por lo que puede hacer clic en él para cancelarla en cualquier momento.
- Al cambiar al modo **RX** se ocultan los botones **⏺** y **▶**. Vuelva a **TX** para acceder a ellos nuevamente.

## Resolución de problemas

- **El botón ⏺ aparece en gris** — La fuente del micrófono no está configurada en PC, DAX está habilitado o la reproducción está en curso. Deshabilite DAX, configure la entrada del micrófono en PC y espere a que finalice la reproducción antes de grabar.
- **El botón ▶ aparece en gris** — Aún no existe ninguna grabación o la grabación está actualmente activa. Complete una grabación primero.
- **El botón ⏺ no es visible** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la cadena TX; los botones de grabar y reproducir solo aparecen en el modo TX.

## Relacionados

- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
