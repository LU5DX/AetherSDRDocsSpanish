# Omitir el tubo de cualquiera de las cadenas

Utilice este procedimiento para habilitar o deshabilitar el saturador de tubo en la cadena de TX, en la cadena de RX, o en ambas, sin cambiar ninguno de los mandos de ajuste. Omitir le permite comparar la señal procesada y la no procesada al instante y mantiene todos los ajustes intactos.

## Antes de empezar

- El contenedor principal de Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores "Aetherial Mic-PreAmp" (TX) y "Aetherial Dynamic Tube" (RX) aparecen dentro de él.
- La etapa TUBE debe estar presente en el widget CHAIN correspondiente. La omisión se controla con un solo clic en la etapa TUBE del widget CHAIN para el lado correspondiente.

## Pasos

1. Localice el widget CHAIN para el lado que desea cambiar — TX o RX.
2. Haga un solo clic en la etapa **TUBE** de ese widget CHAIN para activar o desactivar la omisión.
   - Cuando el tubo está activo, la etapa aparece iluminada.
   - Cuando está omitido, la etapa aparece sin iluminar y la señal pasa sin procesar.
3. Repita la operación en el widget CHAIN del otro lado si también desea omitir esa cadena.

El estado de omisión se conserva inmediatamente. El estado de TX se guarda en `ClientTubeTxEnabled`; el estado de RX se guarda en `ClientTubeRxEnabled`.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Clave persistida |
|---|---|---|---|
| Etapa TUBE (TX) — un solo clic | Activa o desactiva el saturador de tubo de TX en la cadena de señal | — | `ClientTubeTxEnabled` |
| Etapa TUBE (RX) — un solo clic | Activa o desactiva el saturador de tubo de RX en la cadena de señal | — | `ClientTubeRxEnabled` |

## Consejos

- Al hacer doble clic en la etapa TUBE del widget CHAIN se abre el editor flotante ("Aetherial Tube — TX" o "Aetherial Tube — RX") en lugar de activar la omisión. Use un solo clic únicamente para la omisión.
- Todos los valores de los mandos (Drive, Tone, Bias, Output, Dry/Wet, Envelope, Attack, Release) no se ven afectados por la omisión. Puede reactivar el tubo en cualquier momento y se restaurarán los ajustes anteriores.
- Cuando la etapa del tubo está omitida, todo el mosaico del applet acoplado se atenúa aproximadamente al 55 % de opacidad. Esto coincide con el efecto de atenuación utilizado por el mosaico de la curva EQ y proporciona una indicación clara de un vistazo de que el procesamiento está inactivo. El mosaico recupera la opacidad total tan pronto como se desactiva la omisión.
- La curva de transferencia y la bola de entrada en vivo en el mosaico del applet continúan reflejando las posiciones actuales de los mandos incluso mientras están omitidos.
- El editor flotante incluye un **medidor de nivel de salida** (etiquetado como **OUT**) en el extremo derecho. Muestra el nivel pico posterior a la saturación con una dinámica de ataque rápido/liberación lenta y está codificado por colores: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB) y rojo (por encima de −3 dB). El medidor no es visible en el mosaico del applet acoplado.
- Cada mando admite la edición de valor en línea. Haga clic en la etiqueta de valor de un mando en el editor flotante para abrir una superposición QLineEdit. Escriba un valor y presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido del mando. Presione Escape para cancelar sin cambiar el valor.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Saturación de mezcla en paralelo con Dry/Wet](parallel-blend-saturation-with-mix.md)
