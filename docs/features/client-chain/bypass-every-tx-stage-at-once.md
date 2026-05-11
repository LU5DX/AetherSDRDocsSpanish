# Omitir toda la cadena de TX a la vez

Use el botón BYPASS para silenciar toda la cadena de DSP de TX en un solo clic — por ejemplo, para comparar su audio de transmisión procesado y sin procesar, o para descartar una etapa de procesamiento durante la resolución de problemas.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrarlo.
- Haga clic en TX en el encabezado del applet para asegurarse de que la cadena de TX sea el lado activo. BYPASS actúa solo sobre la cadena mostrada actualmente.

## Pasos

1. Abra el applet Aetherial Audio Chain haciendo clic en el botón de la bandeja PUDU en la barra lateral derecha.
2. Haga clic en TX en el encabezado del applet para seleccionar la cadena de TX. El botón se vuelve ámbar cuando está activo.
3. Haga clic en BYPASS. El botón se resalta para indicar que está marcado, y todas las etapas de TX habilitadas se deshabilitan a la vez.
4. Para restaurar las etapas, haga clic en BYPASS nuevamente. Solo se re-habilitan las etapas que estaban habilitadas antes de activar BYPASS.

## Función de cada control

| Control                                                 | Tipo                                                                                                                                                                                                                                                                                                                                                                                   | Valor predeterminado                                                                                                                                                                                                                                                                |
|---------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                      | Muestra y edita la cadena de DSP de TX (ClientChainWidget) — completamente interactivo: clic para omitir, doble clic para editar, arrastrar para reordenar.                                                                                                                                                                                                                             | Parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa se persiste mediante PooDooAudioActiveTab='TX' / 'RX'.                                                                                                                       |
| RX                                                      | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Sin marcar                                                                                                                                                                                                                                                                         |
| BYPASS                                                  | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Sin marcar                                                                                                                                                                                                                                                                         |
| Etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un solo clic alterna la omisión de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX.                                                                                                                                                                                                                                             | Delegado a ClientRxChainWidget. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distinto 'application/x-aethersdr-rx-chain-stage' evita caídas accidentales entre las dos tiras. |
| Estado ADSP / mosaico de omisión                        | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta rota al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está encendido. Un solo clic omite todo el grupo NR con una instantánea en memoria; otro solo clic restaura el estado NR previo. El doble clic abre el cuadro de diálogo AetherDSP Settings. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de instantánea recurre a NR2 si no había módulos activos al momento de la omisión.                                                        |

El orden de las etapas y el estado individual de cada una se persisten mediante `ClientCompTxChainStages`. La visibilidad del contenedor del applet se persiste mediante `Applet_TXDSP`.

## Consejos

- TX y RX mantienen instantáneas BYPASS completamente separadas. Activar BYPASS en la cadena TX no tiene ningún efecto en la cadena RX, y viceversa.
- Si alterna manualmente una etapa mientras BYPASS está activo, ese cambio manual se conserva fuera de la instantánea y no se revertirá cuando desactive BYPASS.
- El estado marcado de BYPASS que se muestra en el encabezado sigue la cadena que esté visible actualmente. Si cambia a RX y luego vuelve a TX, el estado BYPASS de TX se restaura exactamente como lo dejó.
- En v0.9.8, tanto la omisión de TX como la de RX son gestionadas por el motor de audio. El botón BYPASS en el applet Aetherial Audio Chain, el botón BYPASS en el Aetherial Audio Channel Strip (TX) y cualquier control BYPASS futuro para RX reflejan y controlan el mismo estado gestionado por el motor. Hacer clic en BYPASS en cualquiera de estas ubicaciones para la misma cadena produce el mismo resultado.
- Al hacer doble clic en cualquier mosaico de etapa de la cadena TX ahora se abre el Aetherial Audio Channel Strip — la ventana unificada del editor DSP de TX — en lugar de un editor flotante por etapa. Los editores de etapa individuales siguen siendo accesibles desde el channel strip.

## Solución de problemas

- **BYPASS aparece sin marcar después de cambiar de RX a TX** — Esto es normal. TX y RX rastrean estados separados. Para cada lado, el estado mostrado ahora refleja directamente el valor `isTxBypassed` o `isRxBypassed` del motor. Verifique en qué lado activó BYPASS.
- **Al hacer clic en BYPASS se re-habilitan menos etapas de las esperadas** — Cualquier etapa que haya desactivado manualmente antes de hacer clic en BYPASS ya estaba deshabilitada y no formaba parte de la instantánea, por lo que no se restaurará.
- **El estado de BYPASS en el applet no coincide con el del channel strip** — Asegúrese de estar ejecutando v0.9.8 o posterior. Las versiones anteriores gestionaban el estado de omisión de TX solo en la instantánea del applet; v0.9.8 sincroniza todos los controles BYPASS (TX y RX) a través del motor de audio.

## Relacionados

- [Omitir toda la cadena de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Rehabilitar una etapa específica después de una omisión global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Visión general de Aetherial Audio Chain](overview.md)
