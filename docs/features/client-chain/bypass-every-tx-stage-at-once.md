# Omitir todas las etapas de TX a la vez

Use el botón BYPASS para silenciar toda la cadena DSP de TX de un solo clic; por ejemplo, para comparar su audio de transmisión procesado y sin procesar, o para descartar una etapa de procesamiento durante la resolución de problemas.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrarlo.
- Haga clic en TX en el encabezado del applet para asegurarse de que la cadena TX sea el lado activo. BYPASS solo actúa sobre la cadena mostrada actualmente.

## Pasos

1. Abra el applet Aetherial Audio Chain haciendo clic en el botón de la bandeja PUDU en la barra lateral derecha.
2. Haga clic en TX en el encabezado del applet para seleccionar la cadena TX. El botón se vuelve ámbar cuando está activo.
3. Haga clic en BYPASS. El botón se resalta para indicar que está marcado, y todas las etapas TX habilitadas se deshabilitan a la vez.
4. Para restaurar las etapas, haga clic en BYPASS nuevamente. Solo se re-habilitan las etapas que estaban habilitadas antes de activar BYPASS.

## Qué hace cada control

| Control                                                                                              | Tipo                                                                                                                                                                                                                                                                                                                                                                               | Valor predeterminado                                                                                                                                                                                                                                                                               |
|------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                                                                   | Muestra y edita la cadena DSP de TX (ClientChainWidget) — completamente interactivo: clic para omitir, doble clic para editar, arrastrar para reordenar.                                                                                                                                                                                                                           | Parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa persiste mediante PooDooAudioActiveTab='TX' / 'RX'.                                                                                                                                      |
| RX                                                                                                   | Botón de conmutación                                                                                                                                                                                                                                                                                                                                                               | Sin marcar                                                                                                                                                                                                                                                                                         |
| BYPASS                                                                                               | Botón de conmutación                                                                                                                                                                                                                                                                                                                                                               | Sin marcar                                                                                                                                                                                                                                                                                         |
| Etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)                                       | Un solo clic conmuta la omisión de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX.                                                                                                                                                                                                                                          | Delegado a ClientRxChainWidget. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. Tipo MIME distinto 'application/x-aethersdr-rx-chain-stage' evita caídas accidentales entre las dos tiras. |
| Mosaico de estado / omisión de ADSP                                                                   | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta rota al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic omite todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. Doble clic abre el diálogo AetherDSP Settings. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de instantánea vuelve a NR2 si no había módulos activos al momento de la omisión.                                                                       |

El orden de las etapas y el estado de cada etapa individual se conservan mediante `ClientCompTxChainStages`. La visibilidad del contenedor del applet se conserva mediante `Applet_TXDSP`.

## Consejos

- TX y RX mantienen instantáneas de BYPASS completamente separadas. Activar BYPASS en la cadena TX no tiene efecto en la cadena RX, y viceversa.
- Si cambia manualmente una etapa mientras BYPASS está activo, ese cambio manual se conserva fuera de la instantánea y no se revertirá cuando desactive BYPASS.
- El estado marcado de BYPASS que se muestra en el encabezado sigue la cadena que esté visible actualmente. Si cambia a RX y luego vuelve a TX, el estado BYPASS de TX se restaura exactamente como lo dejó.
- En v0.9.8, tanto la omisión de TX como la de RX son propiedad del motor de audio. El botón BYPASS en el applet Aetherial Audio Chain, el botón BYPASS en el Aetherial Audio Channel Strip (TX), y cualquier control BYPASS futuro para RX reflejan y controlan el mismo estado propiedad del motor. Hacer clic en BYPASS en cualquiera de estas ubicaciones para la misma cadena produce el mismo resultado.
- Hacer doble clic en cualquier mosaico de etapa de la cadena TX ahora abre el Aetherial Audio Channel Strip — la ventana unificada del editor DSP de TX — en lugar de un editor de etapa flotante. Los editores de etapa individual permanecen accesibles desde el channel strip.
- El intervalo de discriminación de clic utilizado para la detección de clic simple frente a doble clic en los mosaicos de la cadena TX y RX se puede configurar en Interaction Settings. Por defecto, utiliza el intervalo de doble clic del sistema, pero puede ajustarlo de forma independiente si es necesario.

## Solución de problemas

- **BYPASS aparece sin marcar después de cambiar de RX a TX** — Esto es normal. TX y RX rastrean estados separados. Para cada lado, el estado mostrado ahora refleja directamente el valor `isTxBypassed` o `isRxBypassed` del motor. Verifique en qué lado activó BYPASS.
- **Al hacer clic en BYPASS se re-habilitan menos etapas de las esperadas** — Cualquier etapa que haya desactivado manualmente antes de hacer clic en BYPASS ya estaba deshabilitada y no formaba parte de la instantánea, por lo tanto no se restaurará.
- **El estado BYPASS en el applet no coincide con el channel strip** — Asegúrese de estar ejecutando v0.9.8 o posterior. Las versiones anteriores solo rastreaban el estado de omisión de TX en la instantánea del applet; v0.9.8 sincroniza todos los controles BYPASS (TX y RX) a través del motor de audio.
- **El doble clic abre el editor de manera inconsistente en la cadena TX o RX** — El intervalo de discriminación de clic se puede ajustar en Interaction Settings. Si tiene un movimiento de doble clic lento, aumente este intervalo. Si accidentalmente activa editores en lugar de omitir, disminuya el intervalo.

## Relacionado

- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Re-habilitar una etapa específica después de una omisión global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
- Configurar los ajustes de interacción
