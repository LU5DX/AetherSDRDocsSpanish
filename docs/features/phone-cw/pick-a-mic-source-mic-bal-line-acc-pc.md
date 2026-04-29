# Seleccionar la fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Seleccione qué entrada física o virtual utiliza el radio como fuente de micrófono para transmisiones de voz. La elección determina de dónde toma el FLEX-8600 el audio de TX: el conector de micrófono del panel frontal, la entrada balanceada, la entrada de línea, el puerto de accesorios o el sistema de audio de la PC.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM, etc.). El applet Phone/CW muestra el subpanel Phone automáticamente en los modos de voz.

## Pasos

1. Haga clic en el botón `P/CW` del panel lateral derecho para abrir el applet Phone/CW.
2. Localice el menú desplegable **Mic source** en el subpanel Phone.
3. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto de inmediato en el radio.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Mic source** | Selecciona la fuente de entrada de micrófono enviada al radio. | — | `MIC`, `BAL`, `LINE`, `ACC`, `PC` | — |
| **Mic gain** | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, el valor se almacena en el lado del cliente porque el radio siempre reporta un nivel de 0 para fuentes PC. | 50 | 0–100 | `PcMicGain` |

**Descripción de las fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono por el puerto de accesorios.
- **PC** — Sistema de audio de la computadora. El radio no reporta el nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

## Controles de tono lateral CW (v0.9.1+)

Cuando el slice activo está en un modo CW, el applet cambia al subpanel CW. El interruptor **Sidetone** y el control deslizante **Sidetone volume** controlan simultáneamente tanto el monitor alimentado por DAX del radio como el generador de tono lateral de baja latencia del lado del cliente (~10 ms de latencia). No existen controles de tono lateral locales independientes; un único conjunto de controles gobierna ambas rutas.

| Control | Descripción | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Sidetone** | Activa o desactiva el tono lateral CW. Controla simultáneamente el monitor alimentado por DAX del radio y el generador de tono lateral del lado del cliente. | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del tono lateral tanto para el lado del radio (`mon_gain_cw`) como para el generador del lado del cliente. | — | 0–100 | — |
| **L / R pan (CW)** | Ajusta el paneo estéreo del monitor CW y aplica paneo de potencia constante al generador de tono lateral local. Haga doble clic para recentrar en 50. | 50 | 0–100 | — |
| **Pitch < / >** | Incrementa o decrementa el tono de tono lateral y decodificación CW en 10 Hz. | 600 Hz | 100–6000 Hz | — |

El tono y el paneo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio. No existe un interruptor "Follow" independiente ni un control deslizante manual de ajuste de tono; esos controles fueron eliminados en la versión v0.9.2.1.

## Consejos

- Al usar `PC` como fuente, el medidor **Level** del applet se suprime mientras no se transmite. Transmita brevemente para confirmar que el audio está pasando.
- Para mezclar el puerto de accesorios junto con su fuente principal, active el botón **+ACC** después de seleccionar la fuente principal.
- A velocidades CW más altas, la ruta de tono lateral del lado del cliente (~10 ms de latencia) es más utilizable que el monitor alimentado por DAX del radio. Dado que el interruptor **Sidetone** controla ambas rutas a la vez, activar el tono lateral siempre activa automáticamente la ruta de baja latencia.

## Resolución de problemas

- **El selector Mic source no muestra ninguna selección o se reinicia** — La lista se completa con las entradas reportadas por el radio. Si el selector está vacío, verifique que la conexión con el radio esté activa (`Settings > Connect to Radio...`).
- **El medidor Level no registra nada cuando la fuente es PC** — Esto es normal. El radio reporta `mic_level=0` para fuentes PC; la ganancia es gestionada por `PcMicGain` en el lado del cliente.
- **El tono del tono lateral no coincide con lo esperado** — El tono sigue automáticamente el ajuste `cw_pitch` del radio. Ajuste el tono mediante el control **Pitch < / >**, que escribe directamente en el radio.

## Relacionados

- [Ajustar la ganancia del micrófono y activar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
