# Omitir todas las etapas de TX a la vez

Use el botón BYPASS para silenciar toda la cadena DSP de TX en un solo clic — por ejemplo, para comparar su audio de transmisión procesado y sin procesar, o para descartar una etapa de procesamiento al solucionar problemas.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- Haga clic en TX en el encabezado del applet para asegurarse de que la cadena TX sea el lado activo. BYPASS actúa únicamente sobre la cadena que se muestra en ese momento.

## Pasos

1. Abra el applet Aetherial Audio Chain haciendo clic en el botón PUDU de la bandeja en la barra lateral derecha.
2. Haga clic en TX en el encabezado del applet para seleccionar la cadena TX. El botón se torna ámbar cuando está activo.
3. Haga clic en BYPASS. El botón se resalta para indicar que está activado, y todas las etapas de TX habilitadas se deshabilitan a la vez.
4. Para restaurar las etapas, haga clic en BYPASS nuevamente. Solo se vuelven a habilitar las etapas que estaban habilitadas antes de activar BYPASS.

## Qué hace cada control

| Control                                           | Tipo                                                                                                                                   | Valor predeterminado                                                                                                                                                                                                                                                             |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                | Botón de alternancia                                                                                                                          | Activado                                                                                                                                                                                                                                                             |
| RX                                                | Botón de alternancia                                                                                                                          | Desactivado                                                                                                                                                                                                                                                           |
| BYPASS                                            | Botón de alternancia                                                                                                                          | Desactivado                                                                                                                                                                                                                                                           |
| Etapa de la cadena RX (EQ / AGC-T / AGC-C / TUBE / PUDU) | Un solo clic alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las cinco etapas RX (EQ, AGC-T/Gate, AGC-C/Comp, Tube, PUDU) están completamente implementadas. El orden es independiente de la cadena TX. El tipo mime `application/x-aethersdr-rx-chain-stage` evita que elementos se suelten entre las dos tiras. |

El orden de las etapas y el estado individual de cada etapa se conservan mediante `ClientCompTxChainStages`. La visibilidad del contenedor del applet se conserva mediante `Applet_TXDSP`.

## Consejos

- TX y RX mantienen instantáneas de BYPASS completamente separadas. Activar BYPASS en la cadena TX no tiene ningún efecto sobre la cadena RX, y viceversa.
- Si alterna manualmente una etapa mientras BYPASS está activo, ese cambio manual se conserva fuera de la instantánea y no se revertirá al desactivar BYPASS.
- El estado activado de BYPASS que se muestra en el encabezado refleja la cadena visible en ese momento. Si cambia a RX y vuelve a TX, el estado de BYPASS de TX se restaura exactamente como lo dejó.

## Solución de problemas

- **BYPASS aparece desactivado después de cambiar de RX a TX** — Esto es lo esperado. TX y RX registran estados activados por separado. Verifique si activó BYPASS mientras la cadena RX estaba seleccionada en lugar de la cadena TX.
- **Al hacer clic en BYPASS se vuelven a habilitar menos etapas de las esperadas** — Cualquier etapa que haya desactivado manualmente antes de hacer clic en BYPASS ya estaba deshabilitada y no formaba parte de la instantánea, por lo que no se restaurará.

## Relacionado

- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
