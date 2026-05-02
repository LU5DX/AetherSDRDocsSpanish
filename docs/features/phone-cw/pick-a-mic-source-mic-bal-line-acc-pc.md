# Seleccionar la fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Seleccione qué entrada física o virtual utiliza el radio como fuente de micrófono para transmisiones de voz. La elección determina de dónde toma el FLEX-8600 su audio de TX: el conector de micrófono del panel frontal, la entrada balanceada, la entrada de línea, el puerto de accesorios o el sistema de audio del PC.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo de fonia (USB, LSB, AM, FM, etc.). El applet Phone/CW muestra el subpanel Phone automáticamente en modos de voz.

## Pasos

1. Haga clic en el botón de bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Localice el menú desplegable **Mic source** en el subpanel Phone.
3. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto de inmediato en el radio.

## Qué hace cada control

| Control        | Descripción                                                                                                                                                                         | Predeterminado |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **Mic source** | Selecciona la fuente de entrada de micrófono enviada al radio.                                                                                                                      | —              |
| **Mic gain**   | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, el valor se almacena en el cliente porque el radio siempre reporta un nivel de 0 para las fuentes PC. | 50             |

**Descripción de las fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono del puerto de accesorios.
- **PC** — Sistema de audio del computador. El radio no reporta el nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

## Controles de tono lateral CW (v0.9.1+)

Cuando el slice activo está en modo CW, el applet cambia al subpanel CW. El interruptor **Sidetone** y el control deslizante **Sidetone volume** gobiernan de forma sincronizada tanto el monitor alimentado por DAX del radio como el generador de tono lateral de baja latencia del lado del cliente (~10 ms de latencia). No existen controles de tono lateral local separados; un único conjunto de controles gobierna ambas rutas.

| Control | Descripción | Predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Sidetone** | Habilita o deshabilita el tono lateral CW. Controla simultáneamente el monitor alimentado por DAX del radio y el generador de tono lateral del lado del cliente. | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del tono lateral tanto para el lado del radio (`mon_gain_cw`) como para el generador del lado del cliente. | — | 0–100 | — |
| **L / R pan (CW)** | Establece el paneo estéreo para el monitor CW y aplica paneo de potencia constante al generador de tono lateral local. Haga doble clic para recentrar en 50. | 50 | 0–100 | — |
| **Pitch < / >** | Ajusta el tono de escucha y decodificación CW en pasos de 10 Hz. | 600 Hz | 100–6000 Hz | — |

El tono y el paneo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio. No existe un interruptor "Follow" separado ni un control deslizante manual de ajuste de tono; esos controles fueron eliminados en v0.9.2.1.

## Consejos

- Al utilizar `PC` como fuente, el medidor **Level** aparece de inmediato cuando AetherSDR se conecta al radio, porque la medición del micrófono PC se ejecuta del lado del cliente independientemente del ajuste `met_in_rx` del radio. El medidor no se suprime entre transmisiones para fuentes PC.
- Para mezclar el puerto de accesorios junto con su fuente principal, habilite el botón de alternancia **+ACC** después de seleccionar la fuente principal.
- A velocidades CW altas, la ruta de tono lateral del lado del cliente (~10 ms de latencia) es más utilizable que el monitor alimentado por DAX del radio. Dado que el interruptor **Sidetone** controla ambas rutas conjuntamente, habilitar el tono lateral siempre activa automáticamente la ruta de baja latencia.
- Cuando VOX se activa mediante un atajo de teclado, el panel Phone se actualiza de inmediato para reflejar el nuevo estado de VOX (v0.9.3).
- En Windows, el flujo de tono lateral CW se inicia de inmediato al conectar (v0.9.3). Si el tono lateral está habilitado antes de conectar, no se requieren pasos adicionales después de establecer la conexión.

## Resolución de problemas

- **El combo de Mic source no muestra selección o se restablece** — La lista se llena con las entradas reportadas por el radio. Si el combo está vacío, verifique que la conexión al radio esté activa (`Settings > Connect to Radio...`).
- **El medidor Level no registra nada cuando la fuente es PC** — Este no es el comportamiento esperado en v0.9.3. El indicador **Level** debe aparecer de inmediato al conectar cuando la fuente de micrófono es `PC`. Si no lo hace, verifique que AetherSDR esté ejecutando v0.9.3 o posterior. Para fuentes que no sean PC, el medidor se suprime a −150 dBFS cuando no se está transmitiendo y `met_in_rx` está desactivado; esto es normal.
- **El tono del tono lateral no coincide con lo esperado** — El tono sigue automáticamente el ajuste `cw_pitch` del radio. Ajuste el tono usando el control **Pitch < / >**, que escribe directamente al radio.
- **El tono lateral no inicia al conectar (Windows)** — Este era un problema conocido en versiones anteriores a v0.9.3 causado por el orden de inicialización del AudioEngine. Actualice a v0.9.3 o posterior para resolverlo.

## Relacionado

- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
