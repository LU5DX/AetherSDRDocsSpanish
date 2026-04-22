# Omitir el de-esser en la cadena

Use esta página para deshabilitar la etapa de de-esser de modo que el audio pase sin ninguna reducción de sibilancias. La omisión (bypass) es útil al comparar el audio TX procesado y sin procesar, o cuando desea saltarse el de-essing en una sesión específica sin modificar sus ajustes configurados.

## Antes de comenzar

- La etapa De-Esser debe existir previamente en la cadena PooDoo Audio (TXDSP). Si aún no la ha agregado, consulte [Descripción general del De-Esser](overview.md).
- El subcontenedor DESS o el widget CHAIN deben estar visibles en el panel de applets.

## Pasos

1. Localice la etapa **DeEss** en el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
2. Haga clic una vez en la etapa **DeEss** para activar o desactivar el bypass.

Cuando la etapa está en bypass, `ClientDeEssTxEnabled` se establece en `false`. Los cuatro controles de ajuste, la curva de respuesta del sidechain y la barra de reducción de ganancia permanecen visibles, pero el de-esser no aplica ninguna atenuación al audio TX. Sus ajustes de `Freq`, `Q`, `Thresh` y `Amount` se conservan y surten efecto de inmediato al reactivar la etapa.

## Consejos

- Un solo clic activa o desactiva el bypass; un doble clic abre el editor flotante De-Ess. Evite hacer doble clic si solo desea activar el bypass.
- La barra de reducción de ganancia en el subcontenedor DESS no mostrará movimiento mientras la etapa esté en bypass, lo que confirma que el bypass está activo.
- Activar el bypass desde el widget CHAIN no restablece ninguno de los cuatro valores de los controles. Al reactivar la etapa, se restaura el de-essing completo con sus últimos ajustes guardados.

## Solución de problemas

- **Al hacer clic en la etapa DeEss no ocurre nada** — Confirme que está haciendo clic en el mosaico de la etapa del widget CHAIN y no en la barra de título del subcontenedor DESS. Hacer clic derecho en la barra de título ofrece opciones de flotante/desplegable/ocultar, no de bypass.
- **La barra de reducción de ganancia sigue mostrando actividad después del bypass** — El medidor realiza consultas a aproximadamente 30 Hz y puede mostrar una lectura residual breve. Si continúa, verifique que `ClientDeEssTxEnabled` haya sido realmente conmutado al reabrir el editor flotante mediante doble clic y comprobando el estado de habilitación.

## Relacionado

- [Descripción general del De-Esser](overview.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Ver la reducción de ganancia en vivo al leer una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
