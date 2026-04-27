# Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio

Use esta página para configurar el nivel de entrada del micrófono y mezclar la entrada de accesorio junto con la fuente de micrófono principal en modo Phone.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW requiere una conexión de radio activa.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible. Si el slice está en modo CW, se muestra el subpanel CW en su lugar.

## Pasos

1. Abra el applet Phone/CW en el Panel de Applets de la barra lateral derecha. Si no está visible, haga clic en el botón de bandeja **P/CW**.
2. Localice el cuadro combinado **Mic source**. Confirme que la fuente que desea ajustar esté seleccionada (por ejemplo, MIC, BAL, LINE, ACC o PC).
3. Arrastre el control deslizante **Mic gain** hacia la izquierda o la derecha para establecer el nivel de entrada. El valor numérico a la derecha del control se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
   - Cuando **Mic source** está configurado en PC, el valor se almacena del lado del cliente como `PcMicGain`. El radio siempre reporta `mic_level=0` para la fuente PC; AetherSDR retiene el valor localmente.
4. Observe el indicador **Level** sobre los controles. Procure que los picos se encuentren entre −20 y −10 dBFS durante el habla normal. El indicador se pone rojo por encima de 0 dBFS.
5. Para mezclar la entrada de accesorio junto con la fuente de micrófono activa, haga clic en **+ACC** para activarlo. Haga clic de nuevo para deshabilitar la mezcla.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **Mic gain** | Establece el nivel de entrada del micrófono. Cuando Mic source es PC, el valor se conserva localmente. | 50 | 0–100 | `PcMicGain` (solo fuente PC) |
| **+ACC** | Habilita la mezcla de la entrada de micrófono de accesorio junto con la fuente principal seleccionada. | — | On / Off | — |
| Indicador **Level** | Muestra el nivel de pico de entrada del micrófono en dBFS. Se pone rojo por encima de 0 dBFS. | — | −40 a +10 dBFS | — |
| Indicador **Compression** | Muestra la cantidad de compresión de voz que se está aplicando. El relleno está invertido (completamente a la derecha = sin compresión). | — | −25 a 0 dB | — |

## Sugerencias

- El indicador **Level** se suprime a −150 dBFS cuando el radio no está transmitiendo y el monitor en recepción está desactivado. Esto es normal; el indicador se activa cuando transmite.
- Si usa la fuente PC, tenga en cuenta que el valor de `PcMicGain` no se envía al radio — es administrado completamente por AetherSDR. Al cambiar a otra fuente y volver a PC se restaura el valor guardado.

## Solución de problemas

- **El control deslizante Mic gain vuelve a su posición o muestra 0 después de ajustarlo** — Está usando la fuente PC y el radio está reportando `mic_level=0`. Este es el comportamiento esperado; AetherSDR conserva el valor en `PcMicGain` y no lo escribe en el radio. La posición del control es correcta.
- **+ACC no tiene efecto** — Confirme que el radio esté en un modo de voz y que el subpanel Phone esté activo. El control +ACC solo está disponible en el subpanel Phone; no está disponible cuando el modo CW está activo.
- **El indicador Level no muestra movimiento al hablar** — El indicador se suprime a −150 dBFS cuando no se está transmitiendo y el monitor en recepción está desactivado. Active la transmisión o habilite el monitor TX para ver los niveles en tiempo real.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
