# Ajustar la ganancia del micrófono y habilitar la mezcla con el accesorio

Use el applet Phone/CW para establecer el nivel de entrada del micrófono y, opcionalmente, combinar la entrada del conector de accesorio junto con su fuente de micrófono principal.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles del applet Phone/CW solo están activos con una conexión de radio en vivo.
- El slice activo debe estar en un modo de voz (SSB, AM, FM). En modo CW, el applet cambia al panel CW y los controles del micrófono no se muestran.
- Abra el applet Phone/CW si no está visible: haga clic en el botón **P/CW** de la barra lateral derecha, o confirme que el panel del applet está visible mediante `View > Applet Panel`.

## Pasos

1. En el applet Phone/CW, localice la fila que contiene el cuadro combinado **Mic source**, el control deslizante **Mic gain** y el botón **+ACC**.
2. Arrastre el control deslizante **Mic gain** hacia la izquierda o la derecha para establecer el nivel de entrada deseado. El valor numérico a la derecha del control se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
3. Observe el indicador **Level** sobre el control deslizante. Mantenga los picos por debajo de 0 dBFS (el indicador se vuelve rojo por encima de 0). Apunte a picos en la región de −10 a −6 dBFS durante el habla normal.
4. Para agregar la entrada del conector de accesorio a la mezcla, haga clic en **+ACC** hasta que se ilumine en verde. Haga clic de nuevo para deshabilitar la mezcla.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Clave de persistencia |
|---|---|---|---|---|
| **Mic gain** | Control deslizante | 50 | 0–100 | `PcMicGain` (cuando Mic source es PC) |
| **+ACC** | Botón de alternancia | — | On / Off | — |
| **Level** | Medidor | — | −40 a +10 dBFS (rojo por encima de 0) | — |

## Consejos

- Cuando **Mic source** está configurado en **PC**, el radio no devuelve el nivel del micrófono desde el firmware. AetherSDR almacena el valor de **Mic gain** localmente usando `PcMicGain` y lo restaura en la próxima sesión. Para todas las demás fuentes (MIC, BAL, LINE, ACC), el radio retiene el valor.
- **+ACC** mezcla la entrada ACC sobre cualquier fuente seleccionada en **Mic source**. No reemplaza la fuente principal.
- El indicador **Compression** muestra cuánta reducción está aplicando el procesador de voz. Si el indicador no se mueve, el procesador de voz (PROC) está apagado.

## Solución de problemas

- **El control deslizante Mic gain no tiene efecto y el indicador Level permanece en −150** — El radio no está transmitiendo y el monitoreo `met_in_rx` está desactivado. El indicador Level se suprime a −150 dBFS en ese estado. Accione el transmisor brevemente para confirmar que el control deslizante funciona.
- **El valor de Mic gain se restablece a 50 después de reconectar** — Esto solo afecta a la fuente **PC**. El valor se guarda en `PcMicGain`. Si el control deslizante se restablece, es posible que la configuración almacenada no se haya escrito antes de que terminara la sesión. Reconecte y establezca el nivel nuevamente.
- **El botón +ACC no tiene ningún efecto visible en el audio** — Confirme que el conector de accesorio tiene una señal de audio activa y que la entrada ACC del radio está físicamente conectada.

## Relacionado

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
