# Omitir el tubo en cualquiera de las cadenas

Use este procedimiento para activar o desactivar el saturador de tubo en la cadena TX, la cadena RX, o en ambas, sin modificar ninguno de los controles de ajuste. La función de omisión (bypass) permite comparar la señal procesada y la no procesada de forma inmediata, y deja todos los ajustes intactos.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe ser visible en el panel de applets. Los subcontenedores "Aetherial Mic-PreAmp" (TX) y "Aetherial Dynamic Tube" (RX) aparecen dentro de él.
- La etapa TUBE debe estar presente en el widget CHAIN correspondiente. El bypass se controla con un solo clic sobre la etapa TUBE en el widget CHAIN del lado correspondiente.

## Pasos

1. Localice el widget CHAIN del lado que desea cambiar: TX o RX.
2. Haga clic una vez sobre la etapa **TUBE** en ese widget CHAIN para activar o desactivar el bypass.
   - Cuando el tubo está activo, la etapa aparece iluminada.
   - Cuando está en bypass, la etapa aparece apagada y la señal pasa sin procesar.
3. Repita el proceso en el widget CHAIN del otro lado si también desea omitir esa cadena.

El estado de bypass se guarda de forma inmediata. El estado TX se guarda en `ClientTubeTxEnabled`; el estado RX se guarda en `ClientTubeRxEnabled`.

## Qué hace cada control

| Control | Función | Valor predeterminado | Clave de persistencia |
|---|---|---|---|
| Etapa TUBE (TX) — clic simple | Activa o desactiva el saturador de tubo TX en la cadena de señal | — | `ClientTubeTxEnabled` |
| Etapa TUBE (RX) — clic simple | Activa o desactiva el saturador de tubo RX en la cadena de señal | — | `ClientTubeRxEnabled` |

## Consejos

- Hacer doble clic sobre la etapa TUBE en el widget CHAIN abre el editor flotante ("Aetherial Tube — TX" o "Aetherial Tube — RX") en lugar de alternar el bypass. Use un solo clic únicamente para el bypass.
- Todos los valores de los controles (Drive, Tone, Bias, Output, Dry/Wet, Envelope, Attack, Release) no se ven afectados por el bypass. Puede reactivar el tubo en cualquier momento y los ajustes anteriores se restauran.
- La curva de transferencia y la bola de entrada en tiempo real en el mosaico del applet continúan reflejando las posiciones actuales de los controles aunque el bypass esté activo.
- El editor flotante incluye un **medidor de nivel de salida** (etiquetado como **OUT**) en el extremo derecho. Muestra el nivel de pico post-saturación con balística de ataque rápido y caída lenta, y usa código de colores: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB) y rojo (por encima de −3 dB). El medidor no es visible en el mosaico del applet acoplado.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste el Drive hasta que la curva empiece a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Saturación en paralelo con Dry/Wet](parallel-blend-saturation-with-mix.md)
