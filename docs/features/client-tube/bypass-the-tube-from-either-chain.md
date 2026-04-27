# Omitir el tubo en cualquiera de las cadenas

Use este procedimiento para activar o desactivar el saturador de tubo en la cadena TX, la cadena RX, o en ambas, sin modificar ninguno de los cinco controles de ajuste. La omisión (bypass) le permite comparar instantáneamente la señal procesada y la no procesada, dejando todos los ajustes intactos.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores "Aetherial Mic-PreAmp" (TX) y "Aetherial Dynamic Tube" (RX) aparecen dentro de él.
- La etapa TUBE debe estar presente en el widget CHAIN correspondiente. El bypass se controla con un solo clic sobre la etapa TUBE en el widget CHAIN del lado correspondiente.

## Pasos

1. Localice el widget CHAIN del lado que desea cambiar: TX o RX.
2. Haga clic una sola vez sobre la etapa **TUBE** en ese widget CHAIN para activar o desactivar el bypass.
   - Cuando el tubo está activo, la etapa aparece iluminada.
   - Cuando está en bypass, la etapa aparece apagada y la señal pasa sin procesamiento.
3. Repita el paso en el widget CHAIN del otro lado si también desea aplicar bypass a esa cadena.

El estado del bypass se guarda de inmediato. El estado TX se guarda en `ClientTubeTxEnabled`; el estado RX se guarda en `ClientTubeRxEnabled`.

## Qué hace cada control

| Control | Función | Valor predeterminado | Clave persistida |
|---|---|---|---|
| Etapa TUBE (TX) — clic simple | Activa o desactiva el saturador de tubo TX en la cadena de señal | — | `ClientTubeTxEnabled` |
| Etapa TUBE (RX) — clic simple | Activa o desactiva el saturador de tubo RX en la cadena de señal | — | `ClientTubeRxEnabled` |

## Consejos

- Hacer doble clic sobre la etapa TUBE en el widget CHAIN abre el editor flotante ("Aetherial Tube — TX" o "Aetherial Tube — RX") en lugar de conmutar el bypass. Use un clic simple únicamente para el bypass.
- Los cinco valores de los controles (Drive, Tone, Bias, Output, Mix) no se ven afectados por el bypass. Puede reactivar el tubo en cualquier momento y los ajustes anteriores se restauran.
- La curva de transferencia y la bola de entrada en vivo en el mosaico del applet siguen reflejando las posiciones actuales de los controles incluso durante el bypass.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste de Drive hasta que la curva comience a curvarse (calidez TX o modelado de tono RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
