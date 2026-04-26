# Ajustar la ganancia del micrófono y habilitar la mezcla del accesorio

Use esta página para establecer el nivel de entrada del micrófono y, opcionalmente, mezclar la entrada del conector de accesorio en su FLEX-8600 mientras opera en un modo de voz.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM, etc.) para que el sub-panel Phone sea visible en el PhoneCwApplet.

## Pasos

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW, si no está ya abierto.
2. Confirme que el sub-panel Phone está visible. Si el slice activo está en un modo CW, cambie primero el slice a un modo de voz.
3. Localice el cuadro combinado **Mic source**. Si usa un micrófono de PC, seleccione **PC** de la lista. Para otras fuentes, consulte [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md).
4. Arrastre el control deslizante **Mic gain** para establecer el nivel de entrada deseado. Observe el indicador **Level**: procure mantener los picos por debajo de 0 dBFS (el indicador se vuelve rojo por encima de 0).
5. Para mezclar la entrada del conector de accesorio, haga clic en **+ACC** hasta que aparezca resaltado. Haga clic de nuevo para desactivar la mezcla.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|---|
| **Level** | Medidor | — | −40 a +10 dBFS (rojo por encima de 0) | — | Muestra el nivel de pico de la entrada del micrófono en dBFS. |
| **Mic gain** | Control deslizante | 50 | 0–100 | `PcMicGain` | Ajusta el nivel de entrada del micrófono. Cuando **Mic source** está configurado en **PC**, el valor se almacena en el lado del cliente; la radio siempre reporta mic_level=0 para la fuente PC. |
| **+ACC** | Botón de alternancia | — | On / Off | — | Habilita la mezcla de entrada del micrófono de accesorio. |

## Consejos

- Cuando **Mic source** es **PC**, la radio no reporta el nivel del micrófono de vuelta a AetherSDR. El valor de **Mic gain** se guarda localmente en `PcMicGain` y se restaura en la próxima sesión.
- Use el indicador **Level** mientras habla para verificar el ajuste de ganancia antes de transmitir. Los picos que alcanzan consistentemente la zona roja (por encima de 0 dBFS) indican que **Mic gain** está demasiado alto.
- **+ACC** puede estar activo al mismo tiempo que cualquier otra fuente de micrófono, lo que permite mezclar un dispositivo de audio conectado como accesorio con la fuente principal.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
