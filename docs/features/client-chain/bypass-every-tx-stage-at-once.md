# Anular todas las etapas de TX a la vez

Utilice el botón BYPASS para silenciar toda la cadena de DSP de TX de un solo clic; por ejemplo, para comparar su audio de transmisión procesado y sin procesar, o para descartar una etapa de procesamiento durante la resolución de problemas.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrarlo.
- Haga clic en TX en el encabezado del applet para asegurarse de que la cadena de TX sea el lado activo. BYPASS solo actúa sobre la cadena que se muestra actualmente.

## Pasos

1. Abra el applet Aetherial Audio Chain haciendo clic en el botón de la bandeja PUDU en la barra lateral derecha.
2. Haga clic en TX en el encabezado del applet para seleccionar la cadena de TX. El botón se vuelve ámbar cuando está activo.
3. Haga clic en BYPASS. El botón se resalta para indicar que está marcado, y todas las etapas de TX habilitadas se deshabilitan a la vez.
4. Para restaurar las etapas, haga clic en BYPASS nuevamente. Solo se vuelven a habilitar las etapas que estaban habilitadas antes de activar BYPASS.

## Qué hace cada control

| Control                                                 | Tipo                                                                                                                                                                                                                                                                                                                                                                                   | Valor predeterminado                                                                                                                                                                                                                                                                |
|---------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                      | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Marcado                                                                                                                                                                                                                                                                            |
| RX                                                      | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | No marcado                                                                                                                                                                                                                                                                         |
| BYPASS                                                  | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | No marcado                                                                                                                                                                                                                                                                         |
| Etapa de cadena de RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un solo clic alterna la anulación de la etapa de RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reorganiza la cadena de RX.                                                                                                                                                                                                                                    | Delegado a ClientRxChainWidget. Las seis etapas de RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena de TX. El tipo MIME distintivo 'application/x-aethersdr-rx-chain-stage' evita caídas accidentales entre las dos tiras. |
| Bloque de estado/anulación de ADSP                      | Bloque interactivo del lado de RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic anula todo el clúster de NR con una instantánea en memoria; otro clic simple restaura el estado anterior de NR. El doble clic abre el cuadro de diálogo de configuración de AetherDSP. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul y punto LED verde que los bloques de etapa implementados. La restauración de la instantánea recurre a NR2 si ningún módulo estaba activo en el momento de la anulación.                                                |

El orden de las etapas y el estado individual de cada etapa se conservan mediante `ClientCompTxChainStages`. La visibilidad del contenedor del applet se conserva mediante `Applet_TXDSP`.

## Consejos

- TX y RX mantienen instantáneas de BYPASS completamente separadas. Activar BYPASS en la cadena de TX no tiene efecto en la cadena de RX, y viceversa.
- Si alterna manualmente una etapa mientras BYPASS está activo, ese cambio manual se conserva fuera de la instantánea y no se revertirá cuando desactive BYPASS.
- El estado marcado de BYPASS que se muestra en el encabezado sigue la cadena que esté visible actualmente. Si cambia a RX y luego vuelve a TX, el estado de BYPASS de TX se restaura exactamente como lo dejó.
- En la versión v0.9.8, tanto la anulación de TX como la de RX son propiedad del motor de audio. El botón BYPASS en el applet Aetherial Audio Chain, el botón BYPASS en el Aetherial Audio Channel Strip (TX) y cualquier control BYPASS futuro para RX reflejan y controlan el mismo estado propiedad del motor. Hacer clic en BYPASS en cualquiera de estas ubicaciones para la misma cadena produce el mismo resultado.
- Al hacer doble clic en cualquier bloque de etapa de la cadena de TX ahora se abre el Aetherial Audio Channel Strip — la ventana unificada del editor de DSP de TX — en lugar de un editor flotante por etapa. Los editores de etapa individual siguen siendo accesibles desde el channel strip.

## Solución de problemas

- **BYPASS aparece sin marcar después de cambiar de RX a TX** — Esto es normal. TX y RX rastrean estados separados. Para cada lado, el estado mostrado ahora refleja directamente el valor `isTxBypassed` o `isRxBypassed` del motor. Verifique en qué lado activó BYPASS.
- **Al hacer clic en BYPASS se vuelven a habilitar menos etapas de las esperadas** — Cualquier etapa que haya desactivado manualmente antes de hacer clic en BYPASS ya estaba deshabilitada y no formaba parte de la instantánea, por lo que no se restaurará.
- **El estado de BYPASS en el applet no coincide con el channel strip** — Asegúrese de estar ejecutando la versión v0.9.8 o posterior. Las versiones anteriores solo rastreaban el estado de anulación de TX en la instantánea del applet; v0.9.8 sincroniza todos los controles BYPASS (TX y RX) a través del motor de audio.

## Relacionado

- [Anular todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reactivar una etapa específica después de una anulación global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas de TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
