# Omitir todas las etapas de RX a la vez

Use el control BYPASS para silenciar toda la cadena DSP de RX con un solo clic — útil para una verificación rápida A/B de lo que el procesamiento del lado del cliente está haciendo con el audio entrante.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrar el contenedor.
- La cadena RX debe ser la vista activa. Si actualmente se muestra TX, debe cambiar a RX primero.

## Pasos

1. Haga clic en RX en la fila de encabezado del applet. La tira de la cadena RX se vuelve visible y muestra las etapas EQ, GATE, COMP, TUBE y PUDU entre los mosaicos de estado RADIO y SPEAK.
2. Haga clic en BYPASS. El botón se resalta en ámbar y todas las etapas de RX actualmente habilitadas se deshabilitan a la vez. La instantánea de qué etapas estaban activas se guarda internamente.
3. Para restaurar la cadena, haga clic en BYPASS de nuevo. Solo las etapas que estaban habilitadas antes de aplicar el bypass se vuelven a habilitar.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| RX | Botón de alternancia | Sin marcar | Cambia el applet para mostrar y editar la cadena DSP de RX. Conserva la pestaña activa. | `PooDooAudioActiveTab` |
| TX | Botón de alternancia | Marcado | Cambia el applet para mostrar y editar la cadena DSP de TX. Conserva la pestaña activa. | `PooDooAudioActiveTab` |
| BYPASS | Botón de alternancia | Sin marcar | Marcado: toma una instantánea de las etapas de RX habilitadas y las deshabilita todas. Sin marcar: vuelve a habilitar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas. | None |
| Etapa de la cadena RX (EQ / GATE / COMP / TUBE / PUDU) | Controlador de arrastre | — | Un solo clic alterna el bypass de esa etapa individual; doble clic abre su editor sin marco; arrastrar reordena la cadena. | `ClientCompRxChainStages` |

## Consejos

- TX y RX mantienen instantáneas de bypass completamente separadas. Activar BYPASS en RX no tiene ningún efecto sobre la cadena TX, y viceversa.
- Si alterna una etapa individual manualmente mientras BYPASS está activo, ese cambio se conserva fuera de la instantánea y no se revertirá al desactivar el bypass.
- El estado visual marcado de BYPASS refleja el lado (TX o RX) que se muestra actualmente. Si cambia a TX mientras el bypass de RX está activo, se reflejará el estado de bypass de TX, no el de RX.

## Solución de problemas

- **BYPASS aparece marcado después de cambiar de RX a TX** — Cada lado tiene su propio estado de bypass. Lo que ve refleja la cadena activa. Vuelva a RX para ver o cambiar el estado de bypass de RX.
- **Las etapas permanecen deshabilitadas después de hacer clic en BYPASS por segunda vez** — Una etapa alternada manualmente mientras BYPASS estaba activo queda fuera de la instantánea y no se restaurará automáticamente. Haga clic en cada etapa afectada individualmente para volver a habilitarla.

## Relacionado

- [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
