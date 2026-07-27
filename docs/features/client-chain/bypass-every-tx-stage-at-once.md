# Omitir todas las etapas de TX a la vez

Use el botón BYPASS para silenciar toda la cadena de DSP de TX en un solo clic — por ejemplo, para comparar el audio de transmisión procesado y sin procesar, o para descartar una etapa de procesamiento al solucionar problemas.

## Antes de empezar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrarlo.
- Haga clic en TX en el encabezado del applet para asegurarse de que la cadena de TX es el lado activo. BYPASS actúa solo sobre la cadena que se muestra actualmente.

## Pasos

1. Abra el applet Aetherial Audio Chain haciendo clic en el botón de la bandeja PUDU en la barra lateral derecha.
2. Haga clic en TX en el encabezado del applet para seleccionar la cadena de TX. El botón se vuelve ámbar cuando está activo.
3. Haga clic en BYPASS. El botón se resalta para indicar que está marcado, y todas las etapas de TX habilitadas (incluyendo RN2) se deshabilitan a la vez.
4. Para restaurar las etapas, haga clic en BYPASS nuevamente. Solo se re-habilitan las etapas que estaban habilitadas antes de activar BYPASS.

## Qué hace cada control

| Control                                               | Tipo                                                                                                                                                                                                                                                                                                                                                                                             | Valor predeterminado                                                                                                                                                                                                                                                                                                    |
|-------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                    | Muestra y edita la cadena de DSP de TX (ClientChainWidget) — completamente interactivo: clic para omitir, doble clic para editar, arrastrar para reordenar.                                                                                                                                                                                                                                      | Parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La pestaña de última actividad persiste mediante PooDooAudioActiveTab='TX' / 'RX'.                                                                                                                                                        |
| RX                                                    | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                             | Sin marcar                                                                                                                                                                                                                                                                                                              |
| BYPASS                                                | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                             | Sin marcar                                                                                                                                                                                                                                                                                                              |
| Etapa de cadena de RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un clic alterna la omisión de la etapa de RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena de RX.                                                                                                                                                                                                                                                       | Delegado a ClientRxChainWidget. Las seis etapas de RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena de TX. El tipo MIME distinto 'application/x-aethersdr-rx-chain-stage' evita caídas accidentales entre las dos tiras. |
 | Mosaico de estado/omisión de ADSP                     | Mosaico interactivo del lado de RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un clic omite todo el clúster de NR con una instantánea en memoria; otro clic restaura el estado anterior de NR. El doble clic abre el diálogo de AetherDSP Settings. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de instantánea recurre a NR2 si no había módulos activos al momento de la omisión.                                                                                            |

El orden de las etapas y el estado individual de cada etapa se conservan mediante `ClientCompTxChainStages`. La visibilidad del contenedor del applet se conserva mediante `Applet_TXDSP`.

## Consejos

- TX y RX mantienen instantáneas de BYPASS completamente separadas. Activar BYPASS en la cadena de TX no tiene efecto en la cadena de RX, y viceversa.
- Si alterna manualmente una etapa mientras BYPASS está activo, ese cambio manual se conserva fuera de la instantánea y no se revertirá cuando desactive BYPASS.
- El estado marcado de BYPASS que se muestra en el encabezado sigue la cadena que está visible actualmente. Si cambia a RX y vuelve a TX, el estado de BYPASS de TX se restaura exactamente como lo dejó.
- En v0.9.8, tanto la omisión de TX como la de RX son propiedad del motor de audio. El botón BYPASS en el applet Aetherial Audio Chain, el botón BYPASS en el Aetherial Audio Channel Strip (TX) y cualquier control BYPASS futuro para RX reflejan y controlan el mismo estado propiedad del motor. Hacer clic en BYPASS en cualquiera de estas ubicaciones para la misma cadena produce el mismo resultado.
- Al hacer doble clic en cualquier mosaico de etapa de la cadena de TX ahora se abre el Aetherial Audio Channel Strip — la ventana unificada del editor de DSP de TX — en lugar de un editor flotante por etapa. Los editores de etapas individuales siguen siendo accesibles desde dentro del channel strip.
- El intervalo de discriminación de clic utilizado para la detección de un solo clic frente a doble clic en los mosaicos de las cadenas de TX y RX se puede configurar en Interaction Settings. Por defecto utiliza el intervalo de doble clic del sistema, pero puede ajustarlo de forma independiente si es necesario.
- **BYPASS ahora también deshabilita RN2** en la cadena de TX. La información sobre herramientas del botón BYPASS se actualizó en v26.6.1 para aclarar esto: "Deshabilitar cada etapa en la cadena seleccionada (incluyendo RN2)."
- **El alcance de BYPASS es global (por motor de audio), no por perfil.** El botón BYPASS permanece presionado al cambiar de perfil del Channel Strip. Cambiar de perfil no borra el estado de BYPASS; debe hacer clic en BYPASS nuevamente para restaurar las etapas.

## Solución de problemas

- **BYPASS aparece sin marcar después de cambiar de RX a TX** — Esto es normal. TX y RX rastrean estados separados. Para cada lado, el estado mostrado ahora refleja directamente el valor `isTxBypassed` o `isRxBypassed` del motor. Verifique en qué lado activó BYPASS.
- **Al hacer clic en BYPASS se re-habilitan menos etapas de las esperadas** — Cualquier etapa que alternó manualmente a desactivada antes de hacer clic en BYPASS ya estaba deshabilitada y no formaba parte de la instantánea, por lo que no se restaurará.
- **El estado de BYPASS en el applet no coincide con el channel strip** — Asegúrese de estar usando v0.9.8 o posterior. Las versiones anteriores rastreaban el estado de omisión de TX solo en la instantánea del applet; v0.9.8 sincroniza todos los controles de BYPASS (TX y RX) a través del motor de audio.
- **El doble clic abre el editor de forma inconsistente en la cadena de TX o RX** — El intervalo de discriminación de clic se puede ajustar en Interaction Settings. Si tiene un movimiento de doble clic lento, aumente este intervalo. Si activa editores accidentalmente en lugar de omitir, disminuya el intervalo.
- **BYPASS está activado pero RN2 sigue activo** — En v26.6.1, BYPASS ahora deshabilita explícitamente RN2 como parte de la omisión global. Asegúrese de estar usando v26.6.1 o posterior. Si RN2 permanece activo, intente desactivar y volver a activar BYPASS.
- **BYPASS en el mosaico ADSP no deshabilita BNR** — En v26.7.4, el mosaico ADSP ahora deshabilita y restaura `nvAfxEnabled` en lugar de `bnrEnabled`. Al hacer clic en el mosaico ADSP se alterna todo el clúster de NR, incluyendo el nuevo módulo `nvAfx`. Asegúrese de haber actualizado a v26.7.4 para este comportamiento.

## Relacionado

- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Rehabilitar una etapa específica después de una omisión global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
- Configurar los ajustes de interacción
