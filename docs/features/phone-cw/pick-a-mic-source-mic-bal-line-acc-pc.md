# Seleccione una fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Seleccione qué entrada física o virtual utiliza la radio como fuente de micrófono para transmisiones de voz. La elección determina de dónde toma el FLEX-8600 el audio de TX: del conector de micrófono del panel frontal, de la entrada balanceada, de la entrada de línea, del puerto de accesorios o del sistema de audio de la PC.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- La franja activa debe estar en un modo de telefonía (USB, LSB, AM, FM, etc.). El applet Phone/CW muestra automáticamente el subpanel Phone en los modos de voz.

## Pasos

1. Haga clic en el botón de la bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Localice el cuadro desplegable **Mic source** en el subpanel Phone.
3. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto inmediatamente en la radio.

## Función de cada control

| Control               | Descripción                                                                                                                                                                                                             | Predeterminado |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **Mic source**        | Selecciona la fuente de entrada de micrófono enviada a la radio.                                                                                                                                                        | —              |
| **Mic gain**          | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, o cuando el modo RADE está activo, el valor se almacena del lado del cliente en `PcMicGain` porque la radio no gestiona la ganancia en esas rutas. | 50             |
| **ALC (subpanel Phone)** | Muestra la lectura del control automático de nivel proveniente de `MeterModel::swAlcChanged` (pico SSB post-ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reemplazado desde HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). | — |
| **ALC (subpanel CW)**     | Refleja el indicador ALC del subpanel Phone; ambos leen de `MeterModel::swAlcChanged` para lecturas consistentes en voz y CW. Agregado en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo `HGauge::setFillFromRight`. | — |

**Descripciones de fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono del puerto de accesorios.
- **PC** — Sistema de audio de la computadora. La radio no informa el nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

## Modo RADE y ganancia de micrófono

Cuando el modo RADE está activo, el control deslizante **Mic gain** actúa como un control de ganancia RADE del lado del cliente, en lugar de enviar un comando de nivel de micrófono a la radio. El valor del control deslizante se almacena en `PcMicGain`, la misma configuración utilizada para la fuente `PC`. Mover el control deslizante no sobrescribe la configuración de nivel de micrófono del hardware de la radio mientras RADE está activo.

El medidor **Level** permanece activo durante la recepción cuando RADE está activado. Esto permite monitorear el nivel de entrada entre transmisiones sin activar `met_in_rx` en la radio.

Cuando el modo RADE se desactiva, el control deslizante vuelve al nivel de micrófono informado por la radio y el indicador **Level** se restablece a −150 dBFS hasta que llegue un nuevo valor del medidor.

## Controles de CW (v0.9.8+)

Cuando la franja activa está en un modo CW, el applet cambia al subpanel CW. En v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) se han convertido en widgets `QLineEdit` con `QIntValidator`. Haga clic en cualquier valor y escriba un número directamente, igualando el comportamiento de SmartSDR.

### Ingreso de valores CW

| Control               | Descripción                                                                                                                              | Predeterminado | Rango válido         | Notas                                                                                                               |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------|----------------|----------------------|---------------------------------------------------------------------------------------------------------------------|
| **Delay**             | Retardo de break-in CW en milisegundos. Escriba un valor directamente en el campo de texto o use el control deslizante adyacente.        | 500 ms         | 0–2000 ms (paso 10)  | En v0.9.8, se corrigió `setCwDelay` para almacenar en caché el valor inmediatamente, de modo que la emisión de la radio no devuelva el control deslizante (#2428). |
| **Speed**             | Velocidad de tecleo CW en palabras por minuto. Escriba un valor directamente o use el control deslizante.                                | 20 WPM        | 5–100 WPM            | —                                                                                                                   |
| **Sidetone volume**   | Volumen del monitor CW. Escriba un valor directamente o use el control deslizante. Controla tanto el lado de la radio (`mon_gain_cw`) como el generador de señal lateral del lado del cliente al unísono. | 50      | 0–100                | (v0.9.8, #2429)                                                                                                     |
| **Pitch**             | Tono de la señal lateral y decodificación CW. Escriba un valor (100–6000) o haga clic en los botones **< / >** para avanzar en pasos de 10 Hz. | 600 Hz      | 100–6000 Hz (paso 10) | (v0.9.8, #2429)                                                                                                     |

### Cómo funciona la escritura

1. Haga clic en cualquier campo de texto de valor (por ejemplo, el campo **Delay** que muestra "500").
2. Escriba un nuevo número con su teclado.
3. Presione Enter o Tab para confirmar el valor. El control deslizante se actualiza inmediatamente para coincidir.
4. Si escribe un valor fuera del rango válido, se ajusta al valor válido más cercano al presionar Enter.

### Comportamiento del tono lateral (sidetone)

El interruptor **Sidetone** y el control deslizante **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (~10 ms de latencia) al unísono. No hay controles de tono lateral local separados; un único conjunto de controles gobierna ambas rutas.

| Control               | Descripción                                                                                                                                 | Predeterminado | Valores válidos | Clave de configuración |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------------|-----------------|------------------------|
| **Sidetone**          | Habilita o deshabilita el tono lateral CW. Controla simultáneamente el monitor alimentado por DAX de la radio y el generador de tono lateral del lado del cliente. | —       | On / Off        | —                      |
| **Sidetone volume**   | Establece el volumen del tono lateral tanto para el lado de la radio (`mon_gain_cw`) como para el generador del lado del cliente.           | —              | 0–100           | —                      |
| **L / R pan (CW)**    | Establece la panoramización estéreo para el monitor CW y aplica panoramización de potencia constante al generador de tono lateral local. Haga doble clic para centrar en 50. | 50             | 0–100           | —                      |
| **Pitch < / >**       | Avanza el tono de la señal lateral y la decodificación CW en pasos de 10 Hz, o escriba un valor directamente.                               | 600 Hz         | 100–6000 Hz     | —                      |

El tono y la panoramización siempre siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio. No hay un interruptor "Follow" separado ni un control deslizante de anulación manual de tono; esos controles se eliminaron en v0.9.2.1.

## Medición: Indicadores ALC (v26.5.1+)

En v26.5.1 (#2552), tanto el subpanel Phone como el subpanel CW recibieron indicadores ALC nuevos e idénticos. Estos reemplazan la ruta HWALC (tensión RCA) anterior que producía lecturas sin sentido.

| Indicador               | Rango        | Zona roja | Dirección de llenado | Fuente                                      |
|-------------------------|--------------|-----------|----------------------|---------------------------------------------|
| **ALC (subpanel Phone)** | -20 a 0 dBFS | > -3 dBFS | De derecha a izquierda | `MeterModel::swAlcChanged` (pico SSB post-ALC por software) |
| **ALC (subpanel CW)**    | -20 a 0 dBFS | > -3 dBFS | De derecha a izquierda | `MeterModel::swAlcChanged` (fuente idéntica)               |

Puntos clave:
- Ambos indicadores leen de la misma fuente `MeterModel::swAlcChanged`, asegurando lecturas consistentes en voz y CW.
- El indicador está vacío a -20 dBFS y se llena hacia la izquierda hasta 0 dBFS.
- Los valores por debajo de -20 dBFS se fijan en el extremo izquierdo; los valores por encima de 0 dBFS se fijan en el extremo derecho (escala completa).
- La zona roja (> -3 dBFS) indica ALC excesivo; procure mantener la lectura del indicador por debajo de -3 dBFS para una transmisión limpia.

## Consejos

- Cuando use `PC` como fuente, el medidor **Level** aparece inmediatamente cuando AetherSDR se conecta a la radio, porque la medición del micrófono de PC se ejecuta del lado del cliente independientemente de la configuración `met_in_rx` de la radio. El medidor no se suprime entre transmisiones para fuentes PC.
- Cuando el modo RADE está activo, el medidor **Level** también se ejecuta del lado del cliente y no se suprime entre transmisiones, independientemente de la configuración `met_in_rx`. Esto coincide con el comportamiento de la fuente `PC`.
- Para mezclar el puerto de accesorios junto con su fuente principal, active el botón de alternancia **+ACC** después de seleccionar su fuente principal.
- A velocidades CW más altas, la ruta de tono lateral del lado del cliente (~10 ms de latencia) es más utilizable que el monitor alimentado por DAX de la radio. Debido a que el interruptor **Sidetone** controla ambas rutas juntas, al habilitar el tono lateral siempre se activa automáticamente la ruta de baja latencia.
- Cuando se alterna VOX mediante un atajo de teclado, el subpanel Phone se actualiza instantáneamente para reflejar el nuevo estado de VOX (v0.9.3).
- En Windows, el flujo de tono lateral CW se inicia inmediatamente al conectar (v0.9.3). Si el tono lateral está habilitado antes de conectar, no se requieren pasos adicionales después de establecer la conexión.
- El indicador **Compression** lee 0 dB durante la recepción. Esto es intencional: en v0.9.7, el indicador se habilita según el estado TRANSMITTING del interbloqueo de la radio, por lo que no se muestran lecturas obsoletas de la cadena de TX entre transmisiones.
- El botón **Breakin** respeta completamente la configuración `break_in` de la radio a partir de v0.9.7. Con **Breakin** activado (QSK), los bordes de la tecla activan TX y el retardo de break-in mantiene el relé. Con **Breakin** desactivado, las teclas se ponen en cola y es necesario activar PTT manualmente. Se ha eliminado el comportamiento anterior, donde una envolvente de auto-PTT enmascaraba el estado desactivado de **Breakin** e interfería con el tiempo de espera de QSK.
- El **indicador ALC** está presente tanto en el subpanel Phone como en el subpanel CW, por lo que puede monitorear ALC independientemente del modo. En CW, el indicador ayuda a verificar una forma de envolvente de tecleo limpia.

## Solución de problemas

- **El combo de fuente de micrófono no muestra selección o se reinicia** — La lista se completa con las entradas informadas por la radio. Si el combo está vacío, verifique que la conexión de la radio esté activa (`Settings > Connect to Radio...`).
- **El medidor Level no lee nada cuando la fuente es PC** — Este no es un comportamiento esperado en v0.9.3. El indicador **Level** debería aparecer inmediatamente al conectar cuando la fuente de micrófono es `PC`. Si no es así, verifique que AetherSDR esté ejecutando v0.9.3 o posterior. Para fuentes que no son PC, el medidor se suprime a −150 dBFS cuando no se transmite y `met_in_rx` está desactivado; esto es normal.
- **El medidor Level no lee nada cuando RADE está activo** — El indicador **Level** debería permanecer activo durante la recepción cuando el modo RADE está activado, independientemente de `met_in_rx`. Si el indicador no se actualiza, verifique que AetherSDR esté ejecutando v0.9.7 o posterior.
- **El control deslizante Mic gain se reinicia a 100 cuando se activa RADE** — El modo RADE y la fuente `PC` usan ambas la configuración `PcMicGain`. Si no ha establecido previamente un valor para `PcMicGain`, el control deslizante predetermina a 100 cuando RADE se activa. Ajuste el control deslizante a su nivel preferido; el valor se almacena inmediatamente.
- **El tono lateral no coincide con la expectativa** — El tono sigue automáticamente la configuración `cw_pitch` de la radio. Ajuste el tono usando los botones giratorios **Pitch < / >** o escriba un valor directamente.
- **El tono lateral no se inicia al conectar (Windows)** — Este era un problema conocido en versiones anteriores a v0.9.3 causado por el orden de inicialización de AudioEngine. Actualice a v0.9.3 o posterior para resolverlo.
- **El indicador Compression muestra un valor durante la recepción** — Esto no debería ocurrir en v0.9.7. El indicador se habilita según el estado TRANSMITTING del interbloqueo de la radio y lee 0 durante RX. Si ve una lectura distinta de cero mientras recibe, verifique que esté ejecutando v0.9.7 o posterior.
- **Breakin desactivado no evita TX al presionar una tecla** — Este comportamiento se corrigió en v0.9.7. Actualice a v0.9.7 o posterior. En versiones anteriores, una envolvente de auto-PTT interna podía forzar la TX independientemente de la configuración **Breakin**.
- **El valor CW escrito se reinicia inmediatamente** — Si escribe un valor en un campo de texto CW y se reinicia antes de presionar Enter, asegúrese de presionar Enter o Tab para confirmar el valor. Los campos solo aceptan el valor escrito cuando la edición ha finalizado.
- **El indicador ALC muestra 0 o no se mueve** — Verifique que esté ejecutando v26.5.1 o posterior. El indicador ALC se reemplazó de HWALC a SW ALC en esa versión (#2552). El indicador solo se actualiza cuando se transmite.

## Relacionado

- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
