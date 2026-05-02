# Ajustar la ganancia del micrófono y activar la mezcla de accesorios

Use esta página para configurar el nivel de entrada del micrófono y mezclar la entrada de accesorios junto con la fuente de micrófono principal en el modo Phone.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión activa con la radio.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible. Si el slice está en modo CW, se muestra el subpanel CW en su lugar.

## Pasos

1. Abra el applet Phone/CW en el Panel de Applets de la barra lateral derecha. Si no está visible, haga clic en el botón de bandeja **P/CW**.
2. Localice el cuadro combinado **Mic source**. Confirme que la fuente que desea ajustar está seleccionada (por ejemplo, MIC, BAL, LINE, ACC o PC).
3. Arrastre el control deslizante **Mic gain** hacia la izquierda o la derecha para establecer el nivel de entrada. El valor numérico a la derecha del control deslizante se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
   - Cuando **Mic source** está configurado en PC, el valor se almacena en el lado del cliente como `PcMicGain`. La radio siempre reporta `mic_level=0` para la fuente PC; AetherSDR conserva el valor localmente.
4. Observe el indicador **Level** encima de los controles. Procure que los picos se sitúen entre −20 y −10 dBFS durante el habla normal. El indicador se vuelve rojo por encima de 0 dBFS.
5. Para mezclar la entrada de accesorios junto con la fuente de micrófono activa, haga clic en **+ACC** hasta que quede iluminado. Haga clic de nuevo para desactivar la mezcla.

## Qué hace cada control

| Control               | Función                                                                                                                   | Predeterminado |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------|----------------|
| **Mic gain**          | Establece el nivel de entrada del micrófono. Cuando Mic source es PC, el valor se conserva localmente.                   | 50             |
| **+ACC**              | Activa la mezcla de la entrada de accesorios junto con la fuente principal seleccionada.                                  | —              |
| Indicador **Level**   | Muestra el nivel de pico de entrada del micrófono en dBFS. Se vuelve rojo por encima de 0 dBFS.                          | —              |
| Indicador **Compression** | Muestra la cantidad de compresión de voz que se está aplicando. El relleno está invertido (completo a la derecha = sin compresión). | —     |

## Controles de tono lateral CW

Cuando el slice activo está en modo CW, el subpanel CW reemplaza al subpanel Phone. Los siguientes controles rigen el comportamiento del tono lateral (sidetone) CW.

### Cómo funciona el tono lateral (v0.9.1 y posteriores)

Un único botón de alternancia **Sidetone** y un control deslizante **Sidetone volume** controlan de forma sincronizada tanto el monitor de la radio alimentado por DAX como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, con una latencia aproximada de 10 ms). Activar o desactivar **Sidetone** habilita o deshabilita ambos simultáneamente. Mover **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local al mismo tiempo.

El tono y el paneo estéreo siempre siguen automáticamente los parámetros `cw_pitch` y `mon_pan_cw` de la radio. No existen controles locales separados de tono ni de seguimiento.

### Cambio en v0.9.2.1: controles de tono lateral local independientes eliminados

Antes de v0.9.2.1, el subpanel CW incluía un botón de alternancia independiente **Local STn**, un control deslizante de volumen local, un botón de seguimiento de tono **Follow** y un control deslizante de tono manual. Estos controles se eliminaron en v0.9.2.1. El botón **Sidetone** y el control deslizante **Sidetone volume** ahora controlan conjuntamente el tono lateral del lado de la radio y del lado del cliente, y el tono y el paneo siguen la radio automáticamente.

Si anteriormente usaba el botón **Local STn** de forma independiente del botón principal **Sidetone**, utilice en adelante el botón **Sidetone**. El generador local de baja latencia permanece disponible y activo siempre que **Sidetone** esté activado.

### Controles del subpanel CW

| Control | Función | Predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **Delay (CW)** | Establece el retardo de break-in CW. | — | 0–2000 ms (paso 10) | — |
| **Speed (CW)** | Establece la velocidad de manipulación CW en palabras por minuto. | — | 5–100 WPM | — |
| **Sidetone** | Alterna el tono lateral CW. Activa/desactiva tanto el monitor de la radio alimentado por DAX como el generador local de baja latencia de forma sincronizada. En Windows, el flujo de tono lateral ahora se inicia inmediatamente al conectar (v0.9.3, #2105). | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del monitor CW. Controla tanto `mon_gain_cw` en la radio como el volumen del generador de tono lateral local simultáneamente. | — | 0–100 | — |
| **L / R pan (CW)** | Establece el paneo estéreo del monitor CW. Se aplica tanto al monitor del lado de la radio como al generador de tono lateral local. Haga doble clic para centrar. | 50 | 0–100 | — |
| **Pitch < / >** | Ajusta el tono de sidetone y decodificación CW en pasos de 10 Hz. El tono también se sigue automáticamente desde el parámetro `cw_pitch` de la radio. | 600 Hz | 100–6000 Hz (paso 10) | — |
| **Breakin** | Alterna el break-in completo (QSK). | — | On / Off | — |
| **Iambic** | Alterna el manipulador de paleta iámbico. | — | On / Off | — |
| Indicador **ALC** | Muestra la lectura del control automático de nivel. Se vuelve rojo por encima de 80. | — | 0–100 | — |

## Consejos

- El indicador **Level** se suprime a −150 dBFS cuando la radio no está transmitiendo y el monitor en recepción está desactivado. Esto es normal; el indicador se activa al transmitir. Cuando **Mic source** está configurado en PC, el indicador utiliza medición del lado del cliente y no está sujeto a esta supresión — aparece inmediatamente al conectar (v0.9.3, #2086).
- Si usa la fuente PC, tenga en cuenta que el valor `PcMicGain` no se envía a la radio — es administrado íntegramente por AetherSDR. Cambiar a otra fuente y volver a la fuente PC restaura el valor guardado.
- El generador de tono lateral del lado del cliente proporciona una latencia aproximada de 10 ms, lo cual resulta útil a velocidades CW más altas donde la latencia de ida y vuelta del DAX de la radio se vuelve perceptible. Como ambos están controlados por el único botón **Sidetone**, no existe riesgo de que uno esté activo sin el otro.
- Haga doble clic en **L / R pan (CW)** para devolver la posición de paneo al centro (50).

## Solución de problemas

- **El control deslizante Mic gain vuelve a su posición o indica 0 después de ajustarlo** — Está usando la fuente PC y la radio está reportando `mic_level=0`. Este es el comportamiento esperado; AetherSDR conserva el valor en `PcMicGain` y no lo escribe en la radio. La posición del control deslizante es correcta.
- **+ACC no tiene efecto** — Confirme que la radio esté en modo de voz y que el subpanel Phone esté activo. El control +ACC solo está disponible en el subpanel Phone; no está disponible cuando el modo CW está activo.
- **El indicador Level no muestra movimiento al hablar** — Si Mic source no es PC, el indicador se suprime a −150 dBFS cuando no se está transmitiendo y el monitor en recepción está desactivado. Transmita con la radio o active el monitor TX para ver los niveles en tiempo real. Si Mic source es PC, el indicador debería estar activo inmediatamente al conectar; si no lo está, verifique que el dispositivo de audio del PC esté seleccionado y que AetherSDR esté conectado a la radio.
- **El panel Phone no se actualiza cuando VOX se alterna mediante el atajo de teclado** — Este problema se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior.
- **El tono lateral no se escucha inmediatamente al conectar en Windows** — Este problema se resolvió en v0.9.3 (#2105) corrigiendo el orden de inicialización del AudioEngine. Actualice a v0.9.3 o posterior.
- **Los controles Local STn / Follow no aparecen después de actualizar a v0.9.2.1** — Estos controles se eliminaron en v0.9.2.1. Use el botón **Sidetone** y el control deslizante **Sidetone volume**; ahora controlan conjuntamente el tono lateral del lado de la radio y el local. El tono y el paneo siguen la radio automáticamente y ya no requieren un botón de seguimiento independiente.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
