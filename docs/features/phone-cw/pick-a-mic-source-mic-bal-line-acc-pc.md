# Seleccionar fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Seleccione qué entrada física o virtual utiliza el equipo como fuente de micrófono para transmisiones de voz. La elección determina de dónde toma el FLEX-8600 el audio de TX: el conector de micrófono del panel frontal, la entrada balanceada, la entrada de línea, el puerto de accesorios o el sistema de audio del PC.

## Antes de comenzar

- AetherSDR debe estar conectado a un equipo FLEX-8600.
- El slice activo debe estar en un modo de telefonía (USB, LSB, AM, FM, etc.). El applet Phone/CW muestra automáticamente el subpanel Phone en los modos de voz.

## Pasos

1. Haga clic en el botón `P/CW` de la bandeja en la barra lateral derecha para abrir el applet Phone/CW.
2. Localice el cuadro desplegable **Mic source** en el subpanel Phone.
3. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto inmediatamente en el equipo.

## Qué hace cada control

| Control            | Descripción                                                                                                                                                                                     | Predeterminado |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **Mic source**     | Selecciona la fuente de entrada de micrófono que se envía al equipo.                                                                                                                            | —              |
| **Mic gain**       | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, o cuando el modo RADE está activo, el valor se almacena en el lado del cliente en `PcMicGain` porque el equipo no gestiona la ganancia en esas rutas. | 50             |
| **ALC (panel Phone)** | Muestra la lectura del control automático de nivel procedente de `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Se reemplazó el HWALC (tensión RCA) por el medidor SW ALC en v26.5.1 (#2552). | —              |
| **ALC (panel CW)**     | Refleja el indicador ALC del panel Phone; ambos leen de `MeterModel::swAlcChanged` para obtener lecturas coherentes entre voz y CW. Se añadió en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Utiliza el modo `HGauge::setFillFromRight`. En v26.5.3, ambos indicadores se inicializan a -20 dBFS inmediatamente para evitar una lectura obsoleta durante el arranque (#2899). | —              |

**Descripciones de las fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono del puerto de accesorios.
- **PC** — Sistema de audio del ordenador. El equipo no informa del nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

## Modo RADE y ganancia de micrófono

Cuando el modo RADE está activo, el deslizador **Mic gain** actúa como un control de ganancia RADE del lado del cliente, en lugar de enviar un comando de nivel de micrófono al equipo. El valor del deslizador se almacena en `PcMicGain`, el mismo ajuste utilizado para la fuente `PC`. Mover el deslizador no sobrescribe el ajuste de nivel de micrófono por hardware del equipo mientras RADE esté activo.

El medidor **Level** permanece activo durante la recepción cuando RADE está encendido. Esto permite supervisar el nivel de entrada entre transmisiones sin necesidad de activar `met_in_rx` en el equipo.

Cuando se desactiva el modo RADE, el deslizador vuelve al nivel de micrófono informado por el equipo y el indicador **Level** se restablece a −150 dBFS hasta que llegue un nuevo valor del medidor.

## Controles CW (v0.9.8+)

Cuando el slice activo está en un modo CW, el applet cambia al subpanel CW. En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) se han convertido en widgets `QLineEdit` con `QIntValidator`. Haga clic en cualquier valor y escriba un número directamente, imitando el comportamiento de SmartSDR.

### Introducción de valores CW

| Control               | Descripción                                                                                                          | Predeterminado | Rango válido          | Notas                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------|----------------|-----------------------|------------------------------------------------------------------------------------------------|
| **Delay**             | Retardo de ruptura CW en milisegundos. Escriba un valor directamente en el campo de texto o use el deslizador adyacente. | 500 ms         | 0–2000 ms (paso 10)   | En v0.9.8, `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente, de modo que la emisión del equipo no devuelva el deslizador a su posición anterior (#2428). |
| **Speed**             | Velocidad de manipulación CW en palabras por minuto. Escriba un valor directamente o use el deslizador.              | 20 WPM         | 5–100 WPM            | —                                                                                              |
| **Sidetone volume**   | Volumen de monitorización CW. Escriba un valor directamente o use el deslizador. Controla tanto el lado del equipo (`mon_gain_cw`) como el generador de tono local del lado del cliente de forma simultánea. | 50             | 0–100                | (v0.9.8, #2429)                                                                                |
| **Pitch**             | Tono de monitorización y decodificación CW. Escriba un valor (100–6000) o haga clic en los botones **< / >** para avanzar en pasos de 10 Hz. | 600 Hz         | 100–6000 Hz (paso 10) | (v0.9.8, #2429)                                                                                |

### Cómo funciona la escritura

1. Haga clic en cualquier campo de texto de valor (por ejemplo, el campo **Delay** que muestra "500").
2. Escriba un nuevo número con el teclado.
3. Presione Enter o Tab para confirmar el valor. El deslizador se actualiza inmediatamente para coincidir.
4. Si escribe un valor fuera del rango válido, se ajusta al valor válido más cercano al presionar Enter.

### Comportamiento del tono de monitorización

El conmutador **Sidetone** y el deslizador **Sidetone volume** controlan simultáneamente el monitor alimentado por DAX del equipo y el generador de tono local de baja latencia (~10 ms de latencia). No hay controles de tono local independientes; un único conjunto de controles gobierna ambas rutas.

| Control               | Descripción                                                                                                                                              | Predeterminado | Valores válidos | Clave de ajuste |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|-----------------|-----------------|
| **Sidetone**          | Activa o desactiva el tono de monitorización CW. Controla simultáneamente el monitor alimentado por DAX del equipo y el generador de tono del lado del cliente. | —              | On / Off        | —               |
| **Sidetone volume**   | Establece el volumen del tono de monitorización tanto para el lado del equipo (`mon_gain_cw`) como para el generador del lado del cliente.                 | —              | 0–100           | —               |
| **L / R pan (CW)**    | Establece la panorámica estéreo para el monitor CW y aplica panorámica de potencia constante al generador de tono local. Haga doble clic para centrar en 50. | 50             | 0–100           | —               |
| **Pitch < / >**       | Avanza el tono de monitorización y decodificación CW en pasos de 10 Hz, o escriba un valor directamente.                                                 | 600 Hz         | 100–6000 Hz     | —               |

El tono y la panorámica siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del equipo. No hay un conmutador "Follow" independiente ni un deslizador de anulación manual del tono; esos controles se eliminaron en v0.9.2.1.

En v26.5.3 (#2899), el tono de monitorización CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada. Esto significa que el tono se escucha a través del dispositivo que haya configurado en Settings > Audio, no necesariamente el predeterminado del sistema.

## Medición: Indicadores ALC (v26.5.1+)

En v26.5.1 (#2552), tanto el panel Phone como el panel CW recibieron nuevos indicadores ALC idénticos. Estos reemplazan la ruta HWALC (tensión RCA) anterior que producía lecturas sin sentido.

| Indicador            | Rango        | Zona roja | Dirección de llenado | Fuente                                     |
|----------------------|--------------|-----------|----------------------|--------------------------------------------|
| **ALC (panel Phone)** | -20 a 0 dBFS | > -3 dBFS | De derecha a izquierda | `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software) |
| **ALC (panel CW)**    | -20 a 0 dBFS | > -3 dBFS | De derecha a izquierda | `MeterModel::swAlcChanged` (fuente idéntica)           |

En v26.5.3, ambos indicadores ALC se inicializan a -20 dBFS inmediatamente al construirse. Esto evita una breve lectura obsoleta durante el arranque mientras llega la primera actualización del medidor.

Puntos clave:
- Ambos indicadores leen de la misma fuente `MeterModel::swAlcChanged`, lo que garantiza lecturas coherentes entre voz y CW.
- El indicador está vacío a -20 dBFS y se llena hacia la izquierda hasta 0 dBFS.
- Los valores por debajo de -20 dBFS se fijan en el extremo izquierdo; los valores por encima de 0 dBFS se fijan en el extremo derecho (escala completa).
- La zona roja (> -3 dBFS) indica ALC excesivo; procure mantener la lectura del indicador por debajo de -3 dBFS para una transmisión limpia.

## Medición: Bloqueo del medidor Level durante recepción (v26.5.3+)

En v26.5.3 (#2899), la lógica que suprime el medidor **Level** durante la recepción se trasladó a un método dedicado `applyLevelMeterReceiveGate()`. Este método se llama desde las señales de cambio de estado RX/TX y MOX, así como desde `updateMeters()` y `setRadeActive()`:

- Cuando el equipo está recibiendo y `met_in_rx` está desactivado, el medidor **Level** se establece en -150 dBFS independientemente de la fuente de micrófono (PC o RADE).
- Anteriormente, la fuente `PC` y el modo RADE tenían una excepción que mantenía el medidor **Level** activo durante la recepción. A partir de v26.5.3, esa excepción se elimina: todas las fuentes de micrófono se suprimen por igual cuando `met_in_rx` está desactivado y el equipo no está transmitiendo.

## Medición: Indicador de compresión (v26.5.3+)

En v26.5.3 (#2899), la ranura `updateCompression()` se actualizó para interpretar correctamente el valor `COMPPEAK` del equipo. El equipo informa la compresión como una cantidad positiva de 0 a 25 dB. La cara del indicador P/CW está invertida: 0 = sin compresión (sin reducción), -25 = compresión máxima (reducción de 25 dB). El indicador ahora asigna el valor de compresión positivo del equipo a un valor negativo en el indicador:

- `compPeak = 0 dB` → el indicador muestra `0 dB`
- `compPeak = 25 dB` → el indicador muestra `-25 dB`

Los valores se limitan al rango de 0 a 25 dB antes de la conversión, por lo que el indicador nunca lee más allá de `-25 dB`.

## Consejos

- Cuando use `PC` como fuente, el medidor **Level** aparece inmediatamente cuando AetherSDR se conecta al equipo, porque la medición del micrófono PC se ejecuta del lado del cliente independientemente del ajuste `met_in_rx` del equipo. El medidor no se suprime entre transmisiones para fuentes PC.
- Cuando el modo RADE está activo, el medidor **Level** también se ejecuta del lado del cliente y no se suprime entre transmisiones, independientemente del ajuste `met_in_rx`. Esto coincide con el comportamiento de la fuente `PC`.
- Para mezclar el puerto de accesorios junto con su fuente principal, active el botón de conmutación **+ACC** después de seleccionar su fuente principal.
- A velocidades CW más altas, la ruta de tono local del lado del cliente (~10 ms de latencia) es más utilizable que el monitor alimentado por DAX del equipo. Debido a que el conmutador **Sidetone** controla ambas rutas juntas, activar el tono de monitorización activa automáticamente la ruta de baja latencia.
- Cuando se activa o desactiva VOX mediante un atajo de teclado, el panel Phone se actualiza instantáneamente para reflejar el nuevo estado de VOX (v0.9.3).
- En Windows, la transmisión de tono CW se inicia inmediatamente al conectar (v0.9.3). Si el tono de monitorización está activado antes de conectar, no se requieren pasos adicionales después de establecer la conexión.
- El indicador **Compression** lee 0 dB durante la recepción. Esto es intencional: en v0.9.7, el indicador está bloqueado según el estado de transmisión (TRANSMITTING) del enclavamiento del equipo, por lo que no se muestran lecturas obsoletas de la cadena de TX entre transmisiones. En v26.5.3, la asignación del valor de compresión se corrigió para usar el rango positivo de 0 a 25 dB del equipo.
- El botón **Breakin** respeta completamente el ajuste `break_in` del equipo a partir de v0.9.7. Con **Breakin** activado (QSK), los flancos de la tecla inician la TX y el retardo de ruptura mantiene el relé. Con **Breakin** desactivado, las teclas se ponen en cola y el PTT debe activarse manualmente. Se ha eliminado el comportamiento anterior, donde una envolvente de PTT automática enmascaraba el estado **Breakin** desactivado e interfería con el tiempo de mantenimiento de QSK.
- El **indicador ALC** está presente tanto en el subpanel Phone como en el CW, por lo que puede supervisar el ALC independientemente del modo. En CW, el indicador ayuda a verificar una forma de envolvente de manipulación limpia.
- En v26.5.3, el audio del tono de monitorización CW se enruta al dispositivo de salida de audio seleccionado por el usuario en lugar de a la salida predeterminada del sistema. Si no escucha el tono CW, verifique la configuración de salida de audio en `Settings > Audio`.

## Solución de problemas

- **El cuadro combinado Mic source no muestra ninguna selección o se restablece** — La lista se completa a partir de las entradas informadas por el equipo. Si el cuadro combinado está vacío, verifique que la conexión al equipo esté activa (`Settings > Connect to Radio...`).
- **El medidor Level no lee nada cuando la fuente es PC** — Este no es el comportamiento esperado en v0.9.3. El indicador **Level** debería aparecer inmediatamente al conectar cuando la fuente de micrófono es `PC`. Si no es así, verifique que AetherSDR
