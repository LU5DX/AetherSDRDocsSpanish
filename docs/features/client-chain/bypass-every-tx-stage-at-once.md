# Omitir todas las etapas de TX a la vez

Use el botón BYPASS para silenciar toda la cadena DSP de TX en un solo clic — por ejemplo, para comparar su audio de transmisión procesado y sin procesar, o para descartar una etapa de procesamiento durante la resolución de problemas.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja PUDU en la barra lateral derecha para mostrarlo.
- Haga clic en TX en el encabezado del applet para asegurarse de que la cadena de TX es el lado activo. BYPASS actúa únicamente sobre la cadena que se muestra en ese momento.

## Pasos

1. Abra el applet Aetherial Audio Chain haciendo clic en el botón de bandeja PUDU en la barra lateral derecha.
2. Haga clic en TX en el encabezado del applet para seleccionar la cadena de TX. El botón se torna ámbar cuando está activo.
3. Haga clic en BYPASS. El botón se resalta para indicar que está activado, y todas las etapas de TX habilitadas se deshabilitan a la vez.
4. Para restaurar las etapas, haga clic en BYPASS nuevamente. Solo se vuelven a habilitar las etapas que estaban habilitadas antes de activar BYPASS.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Configuración persistida | Comportamiento |
|---|---|---|---|---|
| TX | Botón de alternancia | Activado | `PooDooAudioActiveTab` | Selecciona la cadena de TX para visualización y edición. BYPASS actúa sobre esta cadena cuando TX está activo. |
| RX | Botón de alternancia | Desactivado | `PooDooAudioActiveTab` | Selecciona la cadena de RX. TX y RX mantienen instantáneas de BYPASS independientes; al cambiar de lado se refleja el estado de BYPASS de ese lado. |
| BYPASS | Botón de alternancia | Desactivado | — | Activado: guarda una instantánea de todas las etapas habilitadas en el lado activo y las deshabilita todas. Desactivado: vuelve a habilitar únicamente las etapas que estaban activas antes. |

El orden de las etapas y el estado individual de cada etapa se persisten mediante `ClientCompTxChainStages`. La visibilidad del contenedor del applet se persiste mediante `Applet_TXDSP`.

## Consejos

- TX y RX mantienen instantáneas de BYPASS completamente independientes. Activar BYPASS en la cadena de TX no tiene efecto sobre la cadena de RX, y viceversa.
- Si alterna manualmente una etapa mientras BYPASS está activo, ese cambio manual se conserva fuera de la instantánea y no se revertirá al desactivar BYPASS.
- El estado activado de BYPASS que se muestra en el encabezado corresponde a la cadena que esté visible en ese momento. Si cambia a RX y vuelve a TX, el estado de BYPASS de TX se restaura exactamente como lo dejó.

## Resolución de problemas

- **BYPASS aparece desactivado después de cambiar de RX a TX** — Esto es normal. TX y RX registran estados activados independientes. Verifique si activó BYPASS mientras la cadena de RX estaba seleccionada en lugar de la cadena de TX.
- **Al hacer clic en BYPASS se vuelven a habilitar menos etapas de las esperadas** — Cualquier etapa que haya desactivado manualmente antes de hacer clic en BYPASS ya estaba deshabilitada y no formaba parte de la instantánea, por lo que no será restaurada.

## Relacionados

- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
