# Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio

Use el applet Phone/CW para establecer el nivel de entrada del micrófono y, opcionalmente, mezclar la entrada del puerto de accesorio cuando opere en un modo de voz.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone/CW requiere una conexión de radio activa.
- Configure el slice activo en un modo de voz (SSB, AM, FM). El applet muestra el panel Phone únicamente cuando el slice activo no está en modo CW.

## Pasos

1. Abra el panel de applets si no está visible. Haga clic en el botón **P/CW** de la barra lateral derecha, o vaya a `View > Applet Panel` para mostrar el panel y luego haga clic en **P/CW**.
2. Confirme que se muestra el panel Phone. Si el slice activo está en modo CW, cámbielo primero a un modo de voz.
3. Localice el control deslizante **Mic gain** en la fila que también contiene el cuadro combinado **Mic source** y el botón **+ACC**.
4. Arrastre el control deslizante **Mic gain** hacia la izquierda o la derecha para establecer el nivel de entrada deseado. El rango válido es 0–100. El valor predeterminado es 50. El valor numérico se actualiza a la derecha del control deslizante mientras lo arrastra.
5. Observe el indicador **Level** encima del control deslizante. Procure mantener los picos por debajo de 0 dBFS; el indicador se torna rojo por encima de 0 dBFS. El rango de visualización válido es −40 a +10 dBFS.
6. Para mezclar la entrada del puerto de accesorio junto con la fuente de micrófono actualmente seleccionada, haga clic en **+ACC** hasta que se ilumine en verde. Haga clic en **+ACC** nuevamente para deshabilitar la mezcla.

## Función de cada control

| Control | Tipo | Predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| **Mic gain** | Control deslizante | 50 | 0–100 | `PcMicGain` |
| **+ACC** | Botón de alternancia | — | On / Off | — |
| **Level** | Medidor | — | −40 a +10 dBFS (rojo por encima de 0) | — |

## Consejos

- Cuando **Mic source** está configurado en **PC**, la radio siempre reporta internamente un nivel de micrófono de 0. AetherSDR mantiene el valor de **Mic gain** de forma local mediante el ajuste `PcMicGain` y lo aplica en el lado del cliente. Establezca el nivel en el applet en lugar de depender del valor reportado por la radio.
- **+ACC** agrega la entrada del puerto de accesorio sobre la fuente **Mic source** seleccionada. No reemplaza la selección de fuente actual.

## Solución de problemas

- **El indicador Level muestra −150 dBFS y no responde mientras se recibe** — El medidor se suprime a −150 cuando la radio no está transmitiendo y met_in_rx está desactivado. El indicador se activa al transmitir.
- **El control deslizante Mic gain se restablece a 0 al cambiar Mic source a PC** — La radio reporta mic_level=0 para la fuente PC. El control deslizante reflejará el valor almacenado localmente en `PcMicGain` en la siguiente actualización. Ajuste el control deslizante al nivel que prefiera y el valor se guardará.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de tono lateral de TX](listen-to-a-tx-sidetone-monitor.md)
