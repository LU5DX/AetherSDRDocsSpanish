# Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Seleccione qué entrada física o virtual utiliza el radio como fuente de micrófono para transmisiones de voz. La elección determina de dónde toma el FLEX-8600 su audio de TX: el conector de micrófono del panel frontal, la entrada balanceada, la entrada de línea, el puerto de accesorios o el sistema de audio de la PC.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- La porción activa debe estar en un modo de teléfono (USB, LSB, AM, FM, etc.). El applet Phone/CW muestra automáticamente el subpanel Phone en modos de voz.

## Pasos

1. Haga clic en el botón `P/CW` de la bandeja en la barra lateral derecha para abrir el applet Phone/CW.
2. Localice el cuadro desplegable **Mic source** en el subpanel Phone.
3. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto inmediatamente en el radio.

## Qué hace cada control

| Control                  | Descripción                                                                                                                                                                                                                     | Valor predeterminado |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| **Mic source**           | Selecciona la fuente de entrada de micrófono enviada al radio.                                                                                                                                                                  | —                     |
| **Mic gain**             | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, o cuando el modo RADE está activo, el valor se almacena del lado del cliente en `PcMicGain` porque el radio no gestiona la ganancia en esas rutas.          | 50                    |
| **ALC (panel Phone)**    | Muestra la lectura de control automático de nivel desde `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Se reemplazó desde HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). | — |
| **ALC (panel CW)**       | Refleja el indicador ALC del panel Phone; ambas lecturas provienen de `MeterModel::swAlcChanged` para lecturas consistentes entre voz y CW. Se agregó en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo `HGauge::setFillFromRight`. En v26.5.3 ambos indicadores se inicializan a -20 dBFS inmediatamente para evitar una lectura obsoleta durante el inicio (#2899). | — |

**Descripciones de las fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono del puerto de accesorios.
- **PC** — Sistema de audio de la computadora. El radio no informa el nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

## Modo RADE y ganancia de micrófono

Cuando el modo RADE está activo, el control deslizante de **Mic gain** actúa como un control de ganancia RADE del lado del cliente en lugar de enviar un comando de nivel de micrófono al radio. El valor del control deslizante se almacena en `PcMicGain`, la misma configuración utilizada para la fuente `PC`. Mover el control deslizante no sobrescribe la configuración de nivel de micrófono de hardware del radio mientras RADE está activo.

El medidor **Level** permanece activo durante la recepción cuando RADE está encendido. Esto permite monitorear el nivel de entrada entre transmisiones sin habilitar `met_in_rx` en el radio.

Cuando se desactiva el modo RADE, el control deslizante vuelve al nivel de micrófono informado por el radio y el indicador **Level** se restablece a −150 dBFS hasta que llegue un nuevo valor de medición.

## Controles CW (v0.9.8+)

Cuando la porción activa está en modo CW, el applet cambia al subpanel CW. En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume, Pitch) se han convertido en widgets `QLineEdit` con `QIntValidator`. Haga clic en cualquier valor y escriba un número directamente, imitando el comportamiento de SmartSDR.

### Ingreso de valores CW

| Control                  | Descripción                                                                                                                   | Valor predeterminado | Rango válido            | Notas                                                                                     |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------|----------------------|-------------------------|-------------------------------------------------------------------------------------------|
| **Delay**                | Retardo de pausa CW en milisegundos. Escriba un valor directamente en el campo de texto o use el control deslizante adyacente. | 500 ms               | 0–2000 ms (paso 10)     | En v0.9.8, `setCwDelay` se corrigió para almacenar en caché el valor inmediatamente para que la emisión del radio no devuelva el control deslizante (#2428). |
| **Speed**                | Velocidad de tecleo CW en palabras por minuto. Escriba un valor directamente o use el control deslizante.                      | 20 WPM               | 5–100 WPM               | —                                                                                         |
| **Sidetone volume**      | Volumen de monitorización CW. Escriba un valor directamente o use el control deslizante. Controla tanto el radio (`mon_gain_cw`) como el generador de tono local del lado del cliente de forma sincronizada. | 50 | 0–100 | (v0.9.8, #2429)                                                                          |
| **Pitch**                | Tono de monitorización y decodificación CW. Escriba un valor (100–6000) o haga clic en los botones **< / >** para avanzar en pasos de 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | (v0.9.8, #2429)                                                                           |

### Cómo funciona la escritura

1. Haga clic en cualquier campo de texto de valor (por ejemplo, el campo **Delay** que muestra "500").
2. Escriba un nuevo número usando su teclado.
3. Presione Enter o Tab para confirmar el valor. El control deslizante se actualiza inmediatamente para coincidir.
4. Si escribe un valor fuera del rango válido, se ajustará al valor válido más cercano cuando presione Enter.

### Comportamiento del tono local (Sidetone)

El interruptor **Sidetone** y el control deslizante **Sidetone volume** controlan tanto la monitorización alimentada por DAX del radio como el generador de tono local de baja latencia (~10 ms de latencia) de forma sincronizada. No hay controles de tono local separados; un único conjunto de controles gobierna ambas rutas.

| Control                     | Descripción                                                                                                                                                  | Valor predeterminado | Valores válidos | Clave de configuración |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|-----------------|------------------------|
| **Sidetone**                | Habilita o deshabilita el tono local CW. Controla tanto la monitorización alimentada por DAX del radio como el generador de tono local del lado del cliente simultáneamente. | —                    | On / Off        | —                      |
| **Sidetone volume**         | Establece el volumen del tono local tanto para el radio (`mon_gain_cw`) como para el generador del lado del cliente.                                        | —                    | 0–100           | —                      |
| **L / R pan (CW)**          | Establece la panorámica estéreo para la monitorización CW y aplica panorámica de potencia constante al generador de tono local. Haga doble clic para centrar en 50. | 50                 | 0–100           | —                      |
| **Pitch < / >**             | Avanza el tono de monitorización y decodificación CW en pasos de 10 Hz, o escriba un valor directamente.                                                     | 600 Hz              | 100–6000 Hz     | —                      |

El tono y la panorámica siempre siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` del radio. No hay un interruptor "Follow" separado ni un control deslizante de anulación manual de tono; esos controles se eliminaron en v0.9.2.1.

En v26.5.3 (#2899), el tono local CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada. Esto significa que el tono se escucha a través del dispositivo que haya configurado en Settings > Audio, no necesariamente el predeterminado del sistema.

## Medición: Indicadores ALC (v26.5.1+)

En v26.5.1 (#2552), tanto el panel Phone como el panel CW recibieron indicadores ALC nuevos e idénticos. Estos reemplazan la ruta HWALC anterior (tensión RCA) que producía lecturas sin sentido.

| Indicador                    | Rango         | Zona roja   | Dirección de llenado | Fuente                                              |
|------------------------------|---------------|-------------|----------------------|------------------------------------------------------|
| **ALC (panel Phone)**        | -20 a 0 dBFS  | > -3 dBFS   | De derecha a izquierda | `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software) |
| **ALC (panel CW)**           | -20 a 0 dBFS  | > -3 dBFS   | De derecha a izquierda | `MeterModel::swAlcChanged` (fuente idéntica)                       |

En v26.5.3, ambos indicadores ALC se inicializan a -20 dBFS inmediatamente después de su construcción. Esto evita una breve lectura obsoleta durante el inicio mientras llega la primera actualización de medición.

Puntos clave:
- Ambos indicadores leen de la misma fuente `MeterModel::swAlcChanged`, lo que garantiza lecturas consistentes entre voz y CW.
- El indicador está vacío a -20 dBFS y se llena hacia la izquierda hasta 0 dBFS.
- Los valores por debajo de -20 dBFS se fijan en el extremo izquierdo; los valores por encima de 0 dBFS se fijan en el extremo derecho (escala completa).
- La zona roja (> -3 dBFS) indica ALC excesivo; procure mantener la lectura del indicador por debajo de -3 dBFS para una transmisión limpia.

## Medición: Supresión del indicador Level durante recepción (v26.5.3+)

En v26.5.3 (#2899), la lógica que suprime el indicador **Level** durante la recepción se trasladó a un método dedicado `applyLevelMeterReceiveGate()`. Este método se llama desde las señales de estado RX/TX y cambio de MOX, así como desde `updateMeters()` y `setRadeActive()`:

- Cuando el radio está recibiendo y `met_in_rx` está deshabilitado, el indicador **Level** se establece en -150 dBFS independientemente de la fuente de micrófono (PC o RADE).
- Anteriormente, la fuente `PC` y el modo RADE tenían una excepción que mantenía el indicador **Level** activo durante la recepción. A partir de v26.5.3, esa excepción se elimina: todas las fuentes de micrófono se suprimen por igual cuando `met_in_rx` está desactivado y el radio no está transmitiendo.

## Medición: Indicador de compresión (v26.5.3+)

En v26.5.3 (#2899), la ranura `updateCompression()` se actualizó para interpretar correctamente el valor `COMPPEAK` del radio. El radio informa la compresión como una cantidad positiva de 0–25 dB. La cara del indicador P/CW está invertida: 0 = sin compresión (sin reducción), -25 = compresión completa (reducción de 25 dB). El indicador ahora mapea el valor de compresión positivo del radio a un valor de indicador negativo:

- `compPeak = 0 dB` → el indicador muestra `0 dB`
- `compPeak = 25 dB` → el indicador muestra `-25 dB`

Los valores se limitan al rango de 0–25 dB antes de la conversión, por lo que el indicador nunca lee más allá de `-25 dB`.

## Soporte de temas (v26.6.1)

En v26.6.1, el applet Phone/CW obtuvo soporte completo de temas. Los siguientes elementos visuales ahora respetan el tema activo:

- **Contenedor del applet** — Usa `theme::setContainer(this, "applet/digi")` para un estilo de fondo consistente.
- **Controles deslizantes y ranuras** — Todos los controles deslizantes (Mic gain, Processor level, Monitor volume, Delay, Speed, Sidetone volume, CW pan) ahora usan `applyPrimarySliderStyle()` en lugar de una hoja de estilo codificada, lo que permite aplicar los colores del tema.
- **Colores de etiquetas** — Las etiquetas como "Delay:", "Speed:", y las etiquetas de panorámica "L" y "R" ahora usan `{{color.text.secondary}}` del tema.
- **Botones de paso** — Los botones **<** y **>** para CW Pitch ahora usan `{{color.background.1}}` para los estados normal y hover, y `{{color.accent}}` para el estado presionado, reemplazando los colores codificados anteriores.

La integración de temas asegura que el applet Phone/CW coincida con el estilo visual del resto de la interfaz de AetherSDR cuando se selecciona un tema.

## Consejos

- Cuando use `PC` como fuente, el medidor **Level** aparece inmediatamente cuando AetherSDR se conecta al radio, porque la medición del micrófono de PC se ejecuta del lado del cliente independientemente de la configuración `met_in_rx` del radio. El medidor no se suprime entre transmisiones para fuentes PC.
- Cuando el modo RADE está activo, el medidor **Level** también se ejecuta del lado del cliente y no se suprime entre transmisiones, independientemente de la configuración `met_in_rx`. Esto coincide con el comportamiento de la fuente `PC`.
- Para mezclar el puerto de accesorios junto con su fuente principal, habilite el botón de alternancia **+ACC** después de seleccionar su fuente principal.
- A velocidades CW más altas, la ruta de tono local del lado del cliente (~10 ms de latencia) es más utilizable que la monitorización alimentada por DAX del radio. Debido a que el interruptor **Sidetone** controla ambas rutas juntas, habilitar el tono local siempre activa la ruta de baja latencia automáticamente.
- Cuando VOX se alterna mediante un atajo de teclado, el panel Phone se actualiza instantáneamente para reflejar el nuevo estado de VOX (v0.9.3).
- En Windows, la transmisión de tono local CW comienza inmediatamente al conectar (v0.9.3). Si el tono local está habilitado antes de conectar, no se requieren pasos adicionales después de establecer la conexión.
- El indicador **Compression** lee 0 dB durante la recepción. Esto es intencional: en v0.9.7, el indicador está bloqueado en el estado TRANSMITTING del interbloqueo del radio, por lo que no se muestran lecturas obsoletas de la cadena de TX entre transmisiones. En v26.5.3, el mapeo del valor de compresión se corrigió para usar el rango positivo de 0–25 dB del radio.
- El botón **Breakin** respeta completamente la configuración `break_in` del radio a partir de v0.9.7. Con **Breakin** activado (QSK), los flancos de la tecla activan TX y el retardo de pausa mantiene el relé.
