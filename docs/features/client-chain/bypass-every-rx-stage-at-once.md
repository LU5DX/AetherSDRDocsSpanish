# Omitir todas las etapas RX a la vez

Use el botón BYPASS para deshabilitar todas las etapas de la cadena RX en un solo clic, sin perder el registro de cuáles estaban activas. Al hacer clic en BYPASS nuevamente, se restauran únicamente las etapas que estaban habilitadas antes.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrar el contenedor.
- Debe estar viendo la cadena RX. El botón BYPASS actúa sobre el lado de la cadena que se muestra en ese momento.

## Pasos

1. En el encabezado del applet Aetherial Audio Chain, haga clic en **RX**. Las etapas de la cadena RX aparecen a continuación.
2. Haga clic en **BYPASS**. El botón cambia a su apariencia activada (borde y relleno de color ámbar). Todas las etapas de la cadena RX se deshabilitan de inmediato. AetherSDR guarda una instantánea de las etapas que estaban habilitadas en el momento en que hizo clic.
3. Para restaurar los estados anteriores de las etapas, haga clic en **BYPASS** nuevamente. Solo se vuelven a habilitar las etapas que estaban habilitadas antes del bypass.

## Qué hace cada control

| Control                                            | Tipo                                                                                                                                    | Valor predeterminado   |
|----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **RX**                                             | Botón de alternancia                                                                                                                           | Sin marcar |
| **BYPASS**                                         | Botón de alternancia                                                                                                                           | Sin marcar |
| Etapa de la cadena RX (EQ / AGC-T / AGC-C / TUBE / PUDU) | Un clic alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las cinco etapas RX (EQ, AGC-T/Gate, AGC-C/Comp, Tube, PUDU) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME exclusivo `application/x-aethersdr-rx-chain-stage` impide que haya sueltas accidentales entre las dos tiras. |

## Consejos

- TX y RX mantienen instantáneas de BYPASS separadas. Activar BYPASS en la cadena RX no afecta a la cadena TX, y viceversa.
- Si alterna manualmente una etapa individual mientras BYPASS está marcado, ese cambio se conserva fuera de la instantánea y no se revertirá al desmarcar BYPASS.
- El estado marcado de BYPASS que se muestra en el encabezado refleja el lado de la cadena que está visible en ese momento. Cambie a TX y vuelva a RX para confirmar el estado de BYPASS de RX de un vistazo.

## Solución de problemas

- **BYPASS aparece marcado pero algunas etapas siguen activas** — Es posible que haya alternado etapas individuales manualmente después de activar BYPASS. Esos cambios manuales son independientes de la instantánea. Desmarque y vuelva a marcar BYPASS para tomar una nueva instantánea del estado actual de las etapas.
- **Al hacer clic en BYPASS se vuelven a habilitar etapas que no esperaba** — La instantánea se tomó cuando se marcó BYPASS por primera vez. Solo se restauran las etapas que estaban habilitadas en ese momento. Las etapas que deshabilitó antes de activar BYPASS permanecerán desactivadas.

## Relacionados

- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
