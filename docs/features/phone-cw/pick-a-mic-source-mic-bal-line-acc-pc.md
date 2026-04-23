# Seleccionar la fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Esta página explica cómo seleccionar la fuente de entrada de micrófono para el slice de transmisión activo. Úsela cuando desee alternar entre el micrófono del panel frontal, la entrada balanceada, la entrada de nivel de línea, el conector de accesorios o el audio de PC.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El slice activo debe estar en un modo de voz (el panel Phone debe ser visible en el applet P/CW). Los controles de fuente de micrófono no se muestran cuando el slice está en modo CW.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el panel Phone está visible.
2. Busque el cuadro combinado **Mic source**. Aparece a la izquierda del control deslizante de ganancia de micrófono, directamente debajo del cuadro combinado **Mic profile**.
3. Haga clic en el cuadro combinado **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.
4. La radio cambia a la entrada seleccionada de inmediato.
5. Si seleccionó `PC`, ajuste el control deslizante **Mic gain** al nivel de su preferencia. La radio no reporta un valor de ganancia para la fuente PC — AetherSDR almacena este valor localmente como `PcMicGain`.

## Qué hace cada control

| Control | Tipo | Valores válidos | Predeterminado | Clave de configuración | Notas |
|---|---|---|---|---|---|
| **Mic source** | Cuadro combinado | `MIC`, `BAL`, `LINE`, `ACC`, `PC` | — | — | Envía la fuente seleccionada a la radio de inmediato. Pueden aparecer fuentes adicionales si la radio las reporta. |
| **Mic gain** | Control deslizante | 0–100 | 50 | `PcMicGain` (solo fuente PC) | Cuando la fuente es `PC`, la radio siempre reporta `mic_level=0`; AetherSDR mantiene el valor en el lado del cliente mediante `PcMicGain`. Para todas las demás fuentes, el valor se almacena en la radio. |

## Sugerencias

- El indicador **Level** (−40 a +10 dBFS, rojo por encima de 0) proporciona retroalimentación inmediata después de cambiar la fuente. Obsérvelo mientras habla para confirmar que la señal llega desde la nueva entrada.
- Si también desea mezclar el conector de accesorios junto con otra fuente principal, use el botón de alternancia **+ACC** en lugar de seleccionar `ACC` como única fuente.

## Solución de problemas

- **El indicador Level no muestra movimiento después de seleccionar una nueva fuente** — confirme la conexión física a esa entrada en la radio. El indicador Level se suprime cuando la radio no está transmitiendo y met_in_rx está desactivado; active la transmisión brevemente para verificar la entrada.
- **El control deslizante Mic gain no tiene efecto cuando la fuente es PC** — esto es esperado. La radio ignora el valor de ganancia para la fuente PC; AetherSDR aplica el valor `PcMicGain` localmente. Ajuste el control deslizante y el valor almacenado se actualizará.

## Relacionados

- [Ajustar la ganancia de micrófono y habilitar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
