# Evitar el paso del tubo en cualquiera de las cadenas

Utilice este procedimiento para activar o desactivar el saturador de tubo en la cadena de TX, la cadena de RX, o ambas, sin cambiar ninguno de los mandos de ajuste. Evitar el paso le permite comparar la señal procesada y la no procesada al instante y mantiene todos los ajustes intactos.

## Antes de empezar

- El contenedor principal Aetherial Audio (TXDSP) debe ser visible en el panel de applets. Los subcontenedores "Aetherial Mic-PreAmp" (TX) y "Aetherial Dynamic Tube" (RX) aparecen dentro de él.
- La etapa TUBE debe estar presente en el widget CHAIN correspondiente. El control de paso se realiza con un solo clic en la etapa TUBE en el widget CHAIN del lado correspondiente.

## Pasos

1. Localice el widget CHAIN para el lado que desea cambiar: TX o RX.
2. Haga clic una vez en la etapa **TUBE** de ese widget CHAIN para activar o desactivar el paso.
   - Cuando el tubo está activo, la etapa aparece iluminada.
   - Cuando se evita el paso, la etapa aparece sin iluminar y la señal pasa sin procesar.
3. Repita en el widget CHAIN del otro lado si también desea evitar el paso en esa cadena.

El estado de paso se guarda de inmediato. El estado de TX se guarda en `ClientTubeTxEnabled`; el estado de RX se guarda en `ClientTubeRxEnabled`.

## Qué hace cada control

| Control                        | Qué hace                                                                                                                                                                                                | Valor predeterminado                                                                                                                                                                                                                                                                  |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Etapa TUBE (TX) — un clic      | Activa o desactiva el paso del saturador de tubo de TX en la cadena de señal                                                                                                                            | —                                                                                                                                                                                                                                                                                     |
| Etapa TUBE (RX) — un clic      | Activa o desactiva el paso del saturador de tubo de RX en la cadena de señal                                                                                                                            | —                                                                                                                                                                                                                                                                                     |
| RN2                            | Activación solo en TX (oculto en modo RX). Activa el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al puerta/compresor/saturador. | Ubicado en el panel flotante StripTubePanel debajo del medidor de nivel de salida, solo en el lado TX. Solo en modos de voz; los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) evitan esta etapa. El ajuste se conserva mediante AudioEngine. |

## Consejos

- Al hacer doble clic en la etapa TUBE en el widget CHAIN se abre el editor flotante ("Aetherial Tube — TX" o "Aetherial Tube — RX") en lugar de activar o desactivar el paso. Use un solo clic solo para el paso.
- Todos los valores de los mandos (Drive, Tone, Bias, Output, Dry/Wet, Envelope, Attack, Release) no se ven afectados por la función de paso. Puede reanudar el uso del tubo en cualquier momento y se restaurarán los ajustes anteriores.
- Cuando la etapa del tubo está sin paso, la loseta completa del applet acoplado se atenúa aproximadamente al 55 % de opacidad. Esto coincide con el efecto de atenuación utilizado por la loseta de la curva EQ y proporciona una indicación clara de un vistazo de que el procesamiento está inactivo. La loseta vuelve a la opacidad completa tan pronto como se desactiva el paso.
- La curva de transferencia y la bola de entrada en vivo en la loseta del applet continúan reflejando las posiciones actuales de los mandos incluso mientras se evita el paso.
- El editor flotante incluye un **medidor de nivel de salida** (etiquetado **OUT**) en el extremo derecho. Muestra el nivel máximo posterior a la saturación con una balística de ataque rápido/liberación lenta y está codificado por colores: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB) y rojo (por encima de −3 dB). El medidor no es visible en la loseta del applet acoplado.
- Cada mando admite la edición de valor en línea. Haga clic en la etiqueta de valor de un mando en el editor flotante para abrir una superposición QLineEdit. Escriba un valor y presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido del mando. Presione Escape para cancelar sin cambiar el valor.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Saturación de mezcla paralela con Dry/Wet](parallel-blend-saturation-with-mix.md)
