# Ajuste la ganancia del micrófono y habilite la mezcla de accesorios

Use esta página para establecer el nivel de entrada del micrófono y mezclar la entrada del accesorio junto con la fuente de micrófono principal en modo Phone.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión de radio activa.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible. Si el slice está en modo CW, se muestra el subpanel CW en su lugar.

## Pasos

1. Abra el applet Phone/CW en el Applet Panel en la barra lateral derecha. Si no está visible, haga clic en el botón de bandeja **P/CW**.
2. Localice el cuadro combinado **Mic source**. Confirme que la fuente que desea ajustar está seleccionada (por ejemplo, MIC, BAL, LINE, ACC o PC).
3. Arrastre el regulador **Mic gain** hacia la izquierda o derecha para establecer el nivel de entrada. La lectura numérica a la derecha del regulador se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
   - Cuando **Mic source** está configurado en PC, el valor se almacena en el cliente como `PcMicGain`. La radio siempre reporta `mic_level=0` para la fuente PC; AetherSDR retiene el valor localmente.
4. Observe el medidor **Level** arriba de los controles. Apunte a picos entre −20 y −10 dBFS durante el habla normal. El medidor se vuelve rojo por encima de 0 dBFS.
5. Para mezclar la entrada del accesorio junto con la fuente de micrófono activa, haga clic en **+ACC** para que se ilumíne. Haga clic nuevamente para desactivar la mezcla.

## Qué hace cada control

| Control               | Qué hace                                                                                          | Predeterminado |
|-----------------------|-------------------------------------------------------------------------------------------------------|---------|
| **Mic gain**          | Establece el nivel de entrada del micrófono. Cuando Mic source es PC, el valor se persiste localmente.               | 50      |
| **+ACC**              | Habilita la mezcla de entrada del micrófono del accesorio junto con la fuente principal seleccionada.                            | —       |
| **Level** medidor       | Muestra el nivel de pico de entrada del micrófono en dBFS. Se vuelve rojo por encima de 0 dBFS.                                    | —       |
| **Compression** medidor | Muestra la cantidad de compresión de voz que se está aplicando. El relleno está invertido (completamente a la derecha = sin compresión). | —       |

## Controles de sidetone CW

Cuando el slice activo está en modo CW, el subpanel CW reemplaza al subpanel Phone. Los siguientes controles rigen el comportamiento del sidetone CW.

### Cómo funciona el sidetone (v0.9.1 y posteriores)

Un único interruptor **Sidetone** y un regulador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) en sincronía. Habilitar o deshabilitar **Sidetone** habilita o deshabilita ambos simultáneamente. Mover **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local al mismo tiempo.

El tono y la panoramización estéreo siempre siguen automáticamente los parámetros `cw_pitch` y `mon_pan_cw` de la radio. No hay controles locales separados de tono o seguimiento.

### Cambio en v0.9.2.1: controles de sidetone local separados removidos

Antes de v0.9.2.1, el subpanel CW incluía un interruptor **Local STn** separado, un regulador de volumen local, un interruptor **Follow** de seguimiento de tono y un regulador de tono manual. Estos controles se eliminan en v0.9.2.1. El interruptor **Sidetone** y el regulador **Sidetone volume** ahora controlan tanto el sidetone del lado de la radio como del cliente en conjunto, y el tono y la panoramización siempre siguen la radio automáticamente.

Si anteriormente utilizaba el botón **Local STn** independientemente del interruptor **Sidetone** principal, use el interruptor **Sidetone** en adelante. El generador local de baja latencia permanece disponible y activo siempre que **Sidetone** esté encendido.

### Controles del subpanel CW

| Control | Qué hace | Predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **Delay (CW)** | Establece el retraso de break-in CW. | — | 0–2000 ms (paso 10) | — |
| **Speed (CW)** | Establece la velocidad de tecleo CW en palabras por minuto. | — | 5–100 WPM | — |
| **Sidetone** | Alterna el sidetone CW. Habilita/deshabilita tanto el monitor alimentado por DAX de la radio como el generador local de baja latencia en sincronía. En Windows, la transmisión de sidetone ahora se inicia inmediatamente en la conexión (v0.9.3, #2105). | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del monitor CW. Controla tanto `mon_gain_cw` en la radio como el volumen del generador de sidetone local simultáneamente. | — | 0–100 | — |
| **L / R pan (CW)** | Establece la panoramización estéreo del monitor CW. Se aplica tanto al monitor del lado de la radio como al generador de sidetone local. Haga doble clic para recentrar. | 50 | 0–100 | — |
| **Pitch < / >** | Cambia el tono del sidetone y decodificación CW en incrementos de 10 Hz. El tono también se sigue automáticamente desde el parámetro `cw_pitch` de la radio. | 600 Hz | 100–6000 Hz (paso 10) | — |
| **Breakin** | Alterna el break-in completo (QSK). | — | On / Off | — |
| **Iambic** | Alterna el teclado iámbico. | — | On / Off | — |
| **ALC** medidor | Muestra la lectura del control automático de nivel. Se vuelve rojo por encima de 80. | — | 0–100 | — |

## Consejos

- El medidor **Level** se suprime a −150 dBFS cuando la radio no está transmitiendo y el monitor en recepción está desactivado. Esto es normal; el medidor se activa cuando transmite. Cuando **Mic source** está configurado en PC, el medidor utiliza medición del lado del cliente y no está sujeto a esta supresión — aparece inmediatamente en la conexión (v0.9.3, #2086).
- Si utiliza la fuente PC, tenga en cuenta que el valor `PcMicGain` no se envía a la radio — se gestiona completamente por AetherSDR. Cambiar de la fuente PC y volver restaura el valor guardado.
- El generador de sidetone del cliente proporciona aproximadamente 10 ms de latencia, lo que es útil a velocidades CW más altas donde la latencia de ida y vuelta de DAX de la radio se vuelve notoria. Como ambos se controlan por el único interruptor **Sidetone**, no hay riesgo de que uno esté activo sin el otro.
- Haga doble clic en **L / R pan (CW)** para devolver la posición de panoramización al centro (50).

## Solución de problemas

- **El regulador de ganancia del micrófono se vuelve a ajustar o lee 0 después de ajustar** — Está usando la fuente PC y la radio reporta `mic_level=0`. Este es el comportamiento esperado; AetherSDR retiene el valor en `PcMicGain` y no lo escribe en la radio. La posición del regulador es correcta.
- **+ACC no tiene efecto** — Confirme que la radio está en un modo de voz y el subpanel Phone está activo. El control +ACC solo está presente en el subpanel Phone; no está disponible cuando el modo CW está activo.
- **El medidor Level no se mueve mientras habla** — Si Mic source no es PC, el medidor se suprime a −150 dBFS cuando no está transmitiendo y monitor-en-recepción está desactivado. Accione la radio o habilite el monitor TX para ver niveles en vivo. Si Mic source es PC, el medidor debe estar activo inmediatamente en la conexión; si no, verifique que el dispositivo de audio PC esté seleccionado y que AetherSDR esté conectado a la radio.
- **El panel Phone no se actualiza cuando VOX se alterna mediante atajo de teclado** — Esto se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior.
- **El sidetone no se escucha inmediatamente después de conectar en Windows** — Esto se resolvió en v0.9.3 (#2105) corrigiendo el orden de inicialización de AudioEngine. Actualice a v0.9.3 o posterior.
- **Los controles Local STn / Follow faltan después de actualizar a v0.9.2.1** — Estos controles se eliminaron en v0.9.2.1. Use el interruptor **Sidetone** y el regulador **Sidetone volume**; ahora controlan tanto el sidetone del lado de la radio como el local en conjunto. El tono y la panoramización siguen la radio automáticamente y ya no requieren un interruptor de seguimiento separado.

## Relacionado

- [Elija una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccione un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilite el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuche un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
