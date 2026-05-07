# Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Selecciona qué entrada física o virtual utiliza la radio como fuente de micrófono para las transmisiones de voz. La elección determina de dónde toma el FLEX-8600 el audio de TX: del conector de micrófono del panel frontal, la entrada balanceada, la entrada de línea, el puerto de accesorios o el sistema de audio del PC.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en un modo de fonía (USB, LSB, AM, FM, etc.). El applet Phone/CW muestra automáticamente el subpanel Phone en los modos de voz.

## Pasos

1. Haga clic en el botón `P/CW` de la bandeja en la barra lateral derecha para abrir el applet Phone/CW.
2. Localice el cuadro desplegable **Mic source** en el subpanel Phone.
3. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto inmediatamente en la radio.

## Qué hace cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| **Mic source** | Selecciona la fuente de entrada de micrófono enviada a la radio. | — |
| **Mic gain** | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, o cuando el modo RADE está activo, el valor se almacena en el lado del cliente en `PcMicGain` porque la radio no gestiona la ganancia en esas rutas. | 50 |

**Descripciones de las fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono del puerto de accesorios.
- **PC** — Sistema de audio del ordenador. La radio no informa del nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

## Modo RADE y ganancia de micrófono

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente, en lugar de enviar un comando de nivel de micrófono a la radio. El valor del deslizador se almacena en `PcMicGain`, el mismo ajuste utilizado para la fuente `PC`. Mover el deslizador no sobrescribe el ajuste de nivel de micrófono del hardware de la radio mientras RADE está activo.

El medidor **Level** permanece activo durante la recepción cuando RADE está activado. Esto permite monitorear el nivel de entrada entre transmisiones sin activar `met_in_rx` en la radio.

Cuando se desactiva el modo RADE, el deslizador vuelve al nivel de micrófono informado por la radio y el indicador **Level** se restablece a −150 dBFS hasta que llegue un nuevo valor del medidor.

## Controles de CW (v0.9.8+)

Cuando el slice activo está en modo CW, el applet cambia al subpanel CW. En v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) se han convertido en widgets `QLineEdit` con `QIntValidator`. Haga clic en cualquier valor y escriba un número directamente, imitando el comportamiento de SmartSDR.

### Entrada de valores CW

| Control | Descripción | Predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Delay** | Retardo de break-in de CW en milisegundos. Escriba un valor directamente en el campo de texto o use el deslizador adyacente. | 500 ms | 0–2000 ms (paso 10) | En v0.9.8, se corrigió `setCwDelay` para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no restablezca el deslizador (#2428). |
| **Speed** | Velocidad de codeo CW en palabras por minuto. Escriba un valor directamente o use el deslizador. | 20 WPM | 5–100 WPM | — |
| **Sidetone volume** | Volumen del monitor CW. Escriba un valor directamente o use el deslizador. Controla tanto el lado de la radio (`mon_gain_cw`) como el generador de tono local del cliente de forma sincronizada. | 50 | 0–100 | (v0.9.8, #2429) |
| **Pitch** | Tono del monitor y decodificación CW. Escriba un valor (100–6000) o haga clic en los botones **< / >** para ajustar en pasos de 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | (v0.9.8, #2429) |

### Cómo funciona la escritura

1. Haga clic en cualquier campo de texto de valor (por ejemplo, el campo **Delay** que muestra "500").
2. Escriba un nuevo número con el teclado.
3. Presione Enter o Tab para confirmar el valor. El deslizador se actualiza inmediatamente para coincidir.
4. Si escribe un valor fuera del rango válido, se ajustará al valor válido más cercano al presionar Enter.

### Comportamiento del tono local

El interruptor **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono local de baja latencia (~10 ms) de forma sincronizada. No hay controles de tono local separados; un único conjunto de controles gobierna ambas rutas.

| Control | Descripción | Predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|---|
| **Sidetone** | Activa o desactiva el tono local de CW. Controla simultáneamente el monitor alimentado por DAX de la radio y el generador de tono local. | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del tono local tanto para el lado de la radio (`mon_gain_cw`) como para el generador local. | — | 0–100 | — |
| **L / R pan (CW)** | Establece la panorámica estéreo del monitor CW y aplica panorámica de potencia constante al generador de tono local. Haga doble clic para centrar en 50. | 50 | 0–100 | — |
| **Pitch < / >** | Ajusta el tono del monitor y la decodificación CW en pasos de 10 Hz, o escriba un valor directamente. | 600 Hz | 100–6000 Hz | — |

El tono y la panorámica siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No hay un interruptor "Follow" separado ni un deslizador de anulación manual del tono; esos controles se eliminaron en v0.9.2.1.

## Consejos

- Cuando se usa `PC` como fuente, el medidor **Level** aparece inmediatamente cuando AetherSDR se conecta a la radio, porque la medición del micrófono de PC se ejecuta en el lado del cliente independientemente del ajuste `met_in_rx` de la radio. El medidor no se suprime entre transmisiones para fuentes PC.
- Cuando el modo RADE está activo, el medidor **Level** también se ejecuta en el lado del cliente y no se suprime entre transmisiones, independientemente del ajuste `met_in_rx`. Esto coincide con el comportamiento de la fuente `PC`.
- Para mezclar el puerto de accesorios junto con su fuente principal, active el botón de conmutación **+ACC** después de seleccionar su fuente principal.
- A velocidades CW más altas, la ruta de tono local del lado del cliente (~10 ms de latencia) es más utilizable que el monitor alimentado por DAX de la radio. Debido a que el interruptor **Sidetone** controla ambas rutas juntas, activar el tono local siempre activa automáticamente la ruta de baja latencia.
- Cuando se activa o desactiva VOX mediante un atajo de teclado, el panel Phone se actualiza instantáneamente para reflejar el nuevo estado de VOX (v0.9.3).
- En Windows, el flujo de tono local de CW se inicia inmediatamente al conectar (v0.9.3). Si el tono local está habilitado antes de conectar, no se requieren pasos adicionales después de establecer la conexión.
- El indicador **Compression** muestra 0 dB durante la recepción. Esto es intencional: en v0.9.7, el indicador se habilita según el estado de interbloqueo TRANSMITTING de la radio, por lo que las lecturas obsoletas de la cadena de TX no se muestran entre transmisiones.
- El botón **Breakin** respeta completamente el ajuste `break_in` de la radio a partir de v0.9.7. Con **Breakin** activado (QSK), los bordes de las teclas activan la TX y el retardo de break-in mantiene el relé. Con **Breakin** desactivado, las teclas se ponen en cola y se debe activar PTT manualmente. Se ha eliminado el comportamiento anterior, donde un envelope de PTT automático enmascaraba el estado desactivado de **Breakin** e interfería con el tiempo de espera de QSK.

## Solución de problemas

- **El combo de fuente de micrófono no muestra selección o se restablece** — La lista se completa con las entradas informadas por la radio. Si el combo está vacío, verifique que la conexión con la radio esté activa (`Settings > Connect to Radio...`).
- **El medidor de nivel no muestra nada cuando la fuente es PC** — Este no es el comportamiento esperado en v0.9.3. El indicador **Level** debería aparecer inmediatamente al conectar cuando la fuente de micrófono es `PC`. Si no es así, verifique que AetherSDR esté ejecutando v0.9.3 o posterior. Para fuentes que no sean PC, el medidor se suprime a −150 dBFS cuando no se transmite y `met_in_rx` está desactivado; esto es normal.
- **El medidor de nivel no muestra nada cuando RADE está activo** — El indicador **Level** debería permanecer activo durante la recepción cuando el modo RADE está activado, independientemente de `met_in_rx`. Si el indicador no se actualiza, verifique que AetherSDR esté ejecutando v0.9.7 o posterior.
- **El deslizador de ganancia de micrófono se restablece a 100 cuando se activa RADE** — El modo RADE y la fuente `PC` utilizan ambos el ajuste `PcMicGain`. Si no ha establecido previamente un valor para `PcMicGain`, el deslizador toma el valor predeterminado de 100 cuando RADE se activa. Ajuste el deslizador a su nivel preferido; el valor se almacena inmediatamente.
- **El tono local no coincide con lo esperado** — El tono sigue automáticamente el ajuste `cw_pitch` de la radio. Ajuste el tono usando el cuadro de giro **Pitch < / >** o escriba un valor directamente.
- **El tono local no se inicia al conectar (Windows)** — Este era un problema conocido en versiones anteriores a v0.9.3 causado por el orden de inicialización de AudioEngine. Actualice a v0.9.3 o posterior para resolverlo.
- **El indicador de compresión muestra un valor durante la recepción** — Esto no debería ocurrir en v0.9.7. El indicador se habilita según el estado de interbloqueo TRANSMITTING de la radio y muestra 0 durante RX. Si ve un valor distinto de cero durante la recepción, verifique que está ejecutando v0.9.7 o posterior.
- **Breakin desactivado no evita la TX al presionar una tecla** — Este comportamiento se corrigió en v0.9.7. Actualice a v0.9.7 o posterior. En versiones anteriores, un envelope de PTT automático interno podía forzar la TX independientemente del ajuste **Breakin**.
- **El valor CW escrito se restablece inmediatamente** — Si escribe un valor en un campo de texto CW y se restablece antes de presionar Enter, asegúrese de presionar Enter o Tab para confirmar el valor. Los campos solo aceptan el valor escrito cuando se finaliza la edición.

## Relacionado

- [Adjust mic gain and enable the accessory mix](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Select a mic profile for a specific microphone](select-a-mic-profile-for-a-specific-microphone.md)
- [Enable speech processor at NOR, DX, or DX+ level](enable-speech-processor-at-nor-dx-or-dx-level.md)
