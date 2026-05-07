# Omitir el tubo de cualquiera de las cadenas

Use este procedimiento para habilitar o deshabilitar el saturador de tubo en la cadena de TX, la cadena de RX o en ambas, sin cambiar ninguna de las perillas de sintonización. Omitir le permite comparar la señal procesada y la no procesada al instante y deja todos los ajustes intactos.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores "Aetherial Mic-PreAmp" (TX) y "Aetherial Dynamic Tube" (RX) aparecen dentro de él.
- La etapa TUBE debe estar presente en el widget CHAIN correspondiente. La omisión se controla con un solo clic en la etapa TUBE del widget CHAIN del lado correspondiente.

## Pasos

1. Localice el widget CHAIN del lado que desea cambiar: TX o RX.
2. Haga un solo clic en la etapa **TUBE** de ese widget CHAIN para activar o desactivar la omisión.
   - Cuando el tubo está activo, la etapa aparece iluminada.
   - Cuando está omitido, la etapa aparece sin iluminar y la señal pasa sin procesar.
3. Repita en el widget CHAIN del otro lado si también desea omitir esa cadena.

El estado de omisión se conserva de inmediato. El estado de TX se guarda en `ClientTubeTxEnabled`; el estado de RX se guarda en `ClientTubeRxEnabled`.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Clave conservada |
|---|---|---|---|
| Etapa TUBE (TX) — un solo clic | Activa o desactiva el saturador de tubo de TX en la cadena de señal | — | `ClientTubeTxEnabled` |
| Etapa TUBE (RX) — un solo clic | Activa o desactiva el saturador de tubo de RX en la cadena de señal | — | `ClientTubeRxEnabled` |

## Consejos

- Al hacer doble clic en la etapa TUBE del widget CHAIN, se abre el editor flotante ("Aetherial Tube — TX" o "Aetherial Tube — RX") en lugar de activar la omisión. Use un solo clic solo para omitir.
- Todos los valores de las perillas (Drive, Tone, Bias, Output, Dry/Wet, Envelope, Attack, Release) no se ven afectados por la omisión. Puede reactivar el tubo en cualquier momento y se restaurarán los ajustes anteriores.
- Cuando la etapa de tubo está omitida, todo el mosaico del applet acoplado se atenúa aproximadamente al 55 % de opacidad. Esto coincide con el efecto de atenuación que usa el mosaico de la curva EQ y proporciona una indicación clara de un vistazo de que el procesamiento está inactivo. El mosaico vuelve a la opacidad completa en cuanto se desactiva la omisión.
- La curva de transferencia y la bola de entrada en vivo en el mosaico del applet continúan reflejando las posiciones actuales de las perillas incluso mientras está omitido.
- El editor flotante incluye un **medidor de nivel de salida** (etiquetado **OUT**) en el extremo derecho. Muestra el nivel máximo posterior a la saturación con una balística de ataque rápido/liberación lenta y está codificado por colores: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB) y rojo (por encima de −3 dB). El medidor no es visible en el mosaico del applet acoplado.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Drive hasta que la curva comience a doblarse (calidez de TX o modelado de tono de RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Saturación de mezcla paralela con Dry/Wet](parallel-blend-saturation-with-mix.md)
