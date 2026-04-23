# Omitir todas las etapas de TX a la vez

Use el botón BYPASS para silenciar instantáneamente toda la cadena DSP de TX — EQ, Compressor, Gate, De-Ess, Tube, PUDU y Reverb — y restaurarlas todas con un solo clic cuando haya terminado.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha para mostrarlo.
- El modo TX debe estar activo. BYPASS no tiene efecto en modo RX.

## Pasos

1. Confirme que el botón **TX** en la parte superior izquierda de la tira de cadena PooDoo Audio está marcado. Si en cambio está marcado **RX**, haga clic en **TX**.
2. Haga clic en **BYPASS**. El botón cambia a su estado marcado (borde y relleno ámbar saturado). Cada etapa actualmente habilitada queda registrada en una instantánea y se deshabilita.
3. Para restaurar, haga clic en **BYPASS** nuevamente. Las etapas que estaban habilitadas antes del bypass se vuelven a habilitar.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| TX | Botón de alternancia | Marcado | Muestra la cadena DSP de TX interactiva. Necesario para que BYPASS tenga efecto. | — |
| RX | Botón de alternancia | No marcado | Cambia al marcador de posición de la cadena RX. BYPASS no realiza ninguna acción en este modo. | — |
| BYPASS | Botón de alternancia | No marcado | Marcado: registra en una instantánea las etapas actualmente habilitadas y las deshabilita todas. No marcado: vuelve a habilitar solo las etapas que estaban activas antes. | `ClientCompTxChainStages` |

La tira de cadena y la visibilidad de su contenedor se guardan de forma persistente bajo `Applet_TXDSP`.

## Consejos

- Si activa o desactiva manualmente etapas individuales mientras BYPASS está marcado, esos cambios se rastrean de forma separada de la instantánea. Al desmarcar BYPASS, solo se restauran las etapas que estaban habilitadas en el momento en que marcó BYPASS; los cambios manuales realizados durante el bypass se conservan.
- BYPASS se aplica únicamente a la cadena TX. Hacer clic en él mientras **RX** está seleccionado no tiene ningún efecto.

## Solución de problemas

- **BYPASS está marcado pero el audio sigue pasando por una etapa** — Es posible que una etapa haya sido activada manualmente después de que se activó BYPASS. Esa etapa queda fuera de la instantánea. Haga clic en la etapa una vez para omitirla individualmente, o desmarque y vuelva a marcar BYPASS para tomar una nueva instantánea.
- **El botón BYPASS está presente pero hacer clic en él no tiene efecto** — El botón **RX** está seleccionado. Haga clic primero en **TX**; BYPASS solo opera sobre la cadena TX.

## Relacionado

- [Descripción general de la cadena PooDoo Audio](overview.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Alternar entre la vista de la cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
