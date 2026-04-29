# Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio

Use esta página para establecer el nivel de entrada del micrófono y mezclar la entrada de accesorio junto con la fuente de micrófono principal en el modo Phone.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW requiere una conexión de radio activa.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible. Si el slice está en modo CW, se muestra el subpanel CW en su lugar.

## Pasos

1. Abra el applet Phone/CW en el Panel de Applets de la barra lateral derecha. Si no está visible, haga clic en el botón de bandeja **P/CW**.
2. Localice el cuadro combinado **Mic source**. Confirme que la fuente que desea ajustar esté seleccionada (por ejemplo, MIC, BAL, LINE, ACC o PC).
3. Arrastre el control deslizante **Mic gain** hacia la izquierda o la derecha para establecer el nivel de entrada. La lectura numérica a la derecha del control se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
   - Cuando **Mic source** está configurado en PC, el valor se almacena en el lado del cliente como `PcMicGain`. El radio siempre reporta `mic_level=0` para la fuente PC; AetherSDR retiene el valor localmente.
4. Observe el indicador **Level** sobre los controles. Apunte a picos entre −20 y −10 dBFS durante el habla normal. El indicador se vuelve rojo por encima de 0 dBFS.
5. Para mezclar la entrada de accesorio junto con la fuente de micrófono activa, haga clic en **+ACC** de modo que quede iluminado. Haga clic de nuevo para desactivar la mezcla.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **Mic gain** | Establece el nivel de entrada del micrófono. Cuando Mic source es PC, el valor se conserva localmente. | 50 | 0–100 | `PcMicGain` (solo fuente PC) |
| **+ACC** | Habilita la mezcla de entrada de micrófono de accesorio junto con la fuente principal seleccionada. | — | On / Off | — |
| Indicador **Level** | Muestra el nivel de pico de entrada del micrófono en dBFS. Se vuelve rojo por encima de 0 dBFS. | — | −40 a +10 dBFS | — |
| Indicador **Compression** | Muestra la cantidad de compresión de voz que se está aplicando. El relleno es inverso (totalmente a la derecha = sin compresión). | — | −25 a 0 dB | — |

## Controles de tono lateral CW

Cuando el slice activo está en modo CW, el subpanel CW reemplaza al subpanel Phone. Los siguientes controles rigen el comportamiento del tono lateral (sidetone) de CW.

### Cómo funciona el tono lateral (v0.9.1 y posteriores)

Un único botón **Sidetone** y un control deslizante **Sidetone volume** controlan en conjunto tanto el monitor del radio alimentado por DAX como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia). Habilitar o deshabilitar **Sidetone** habilita o deshabilita ambos simultáneamente. Mover **Sidetone volume** establece tanto `mon_gain_cw` en el radio como el volumen del generador local al mismo tiempo.

El tono y el paneo estéreo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio. No existen controles separados de tono local ni de seguimiento.

### Cambio en v0.9.2.1: controles de tono lateral local separados eliminados

Antes de v0.9.2.1, el subpanel CW incluía un botón **Local STn** independiente, un control deslizante de volumen local, un botón de seguimiento de tono **Follow** y un control deslizante de tono manual. Estos controles se eliminaron en v0.9.2.1. El botón **Sidetone** y el control deslizante **Sidetone volume** ahora controlan juntos el tono lateral del lado del radio y del lado del cliente, y el tono y el paneo siempre siguen al radio automáticamente.

Si anteriormente usaba el botón **Local STn** de forma independiente del botón principal **Sidetone**, utilice el botón **Sidetone** a partir de ahora. El generador de baja latencia local permanece disponible y activo siempre que **Sidetone** esté activado.

### Controles del subpanel CW

| Control | Qué hace | Predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **Delay (CW)** | Establece el retardo de break-in de CW. | — | 0–2000 ms (paso 10) | — |
| **Speed (CW)** | Establece la velocidad de manipulación CW en palabras por minuto. | — | 5–100 WPM | — |
| **Sidetone** | Activa o desactiva el tono lateral de CW. Habilita/deshabilita en conjunto tanto el monitor del radio alimentado por DAX como el generador de baja latencia del lado del cliente. | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del monitor CW. Controla simultáneamente tanto `mon_gain_cw` en el radio como el volumen del generador de tono lateral local. | — | 0–100 | — |
| **L / R pan (CW)** | Establece el paneo estéreo del monitor CW. Se aplica tanto al monitor del lado del radio como al generador de tono lateral local. Haga doble clic para recentrar. | 50 | 0–100 | — |
| **Pitch < / >** | Avanza el tono de tono lateral y decodificación de CW en pasos de 10 Hz. El tono también se sigue automáticamente del ajuste `cw_pitch` del radio. | 600 Hz | 100–6000 Hz (paso 10) | — |
| **Breakin** | Activa o desactiva el break-in completo (QSK). | — | On / Off | — |
| **Iambic** | Activa o desactiva el manipulador de paleta iámbica. | — | On / Off | — |
| Indicador **ALC** | Muestra la lectura del control automático de nivel. Se vuelve rojo por encima de 80. | — | 0–100 | — |

## Consejos

- El indicador **Level** se suprime a −150 dBFS cuando el radio no está transmitiendo y el monitor en recepción está desactivado. Esto es normal; el indicador se activa cuando transmite.
- Si usa la fuente PC, tenga en cuenta que el valor `PcMicGain` no se envía al radio — es administrado íntegramente por AetherSDR. Cambiar a otra fuente distinta de PC y volver restaura el valor guardado.
- El generador de tono lateral del lado del cliente proporciona aproximadamente 10 ms de latencia, lo cual es útil a velocidades CW más altas donde la latencia de ida y vuelta de DAX del radio se vuelve perceptible. Dado que ambos están controlados por el único botón **Sidetone**, no existe riesgo de que uno esté activo sin el otro.
- Haga doble clic en **L / R pan (CW)** para devolver la posición de paneo al centro (50).

## Solución de problemas

- **El control deslizante Mic gain vuelve a su posición o muestra 0 después de ajustarlo** — Está usando la fuente PC y el radio está reportando `mic_level=0`. Este es el comportamiento esperado; AetherSDR mantiene el valor en `PcMicGain` y no lo escribe en el radio. La posición del control es correcta.
- **+ACC no tiene efecto** — Confirme que el radio esté en un modo de voz y que el subpanel Phone esté activo. El control +ACC solo está presente en el subpanel Phone; no está disponible cuando el modo CW está activo.
- **El indicador Level no muestra movimiento mientras habla** — El indicador se suprime a −150 dBFS cuando no se transmite y el monitor en recepción está desactivado. Active la transmisión del radio o habilite el monitor TX para ver los niveles en tiempo real.
- **Los controles Local STn / Follow faltan después de actualizar a v0.9.2.1** — Estos controles fueron eliminados en v0.9.2.1. Use el botón **Sidetone** y el control deslizante **Sidetone volume**; ahora controlan juntos el tono lateral del lado del radio y el local. El tono y el paneo siguen al radio automáticamente y ya no requieren un botón de seguimiento independiente.

## Relacionados

- [Elegir una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
