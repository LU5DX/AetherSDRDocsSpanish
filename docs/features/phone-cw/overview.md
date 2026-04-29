# Descripción general de Phone/CW

El applet Phone/CW es un panel de transmisión con reconocimiento de modo que proporciona controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a los controles de CW cuando el slice activo está en un modo CW. Ábralo para ajustar el audio de transmisión o configurar los parámetros de manipulación.

## Cómo funciona

El applet siempre está presente en el Panel de Applets de la barra lateral derecha. Actívelo con el botón de bandeja **P/CW**. Contiene dos subpaneles gestionados mediante un diseño apilado:

- **Subpanel Phone** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **Subpanel CW** — visible cuando el slice activo está en un modo CW.

AetherSDR cambia entre subpaneles automáticamente al cambiar el modo del slice. No es necesario cambiarlos manualmente.

### Subpanel Phone

| Control | Tipo | Qué hace | Valor predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|---|
| Level | Medidor | Muestra el nivel de pico de entrada del micrófono en dBFS. Indica -150 cuando el medidor está inactivo y no se está transmitiendo. | — | -40 a +10 dBFS (rojo por encima de 0) | — |
| Compression | Medidor | Muestra la cantidad de compresión de voz en dB (relleno invertido: mayor compresión rellena hacia la izquierda). | — | -25 a 0 dB | — |
| Mic profile | Lista desplegable | Carga el perfil de procesamiento de micrófono indicado desde la lista de perfiles del equipo. | — | Poblado desde el equipo | — |
| Mic source | Lista desplegable | Selecciona la fuente de entrada del micrófono. | — | MIC, BAL, LINE, ACC, PC | — |
| Mic gain | Control deslizante | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se mantiene en el lado del cliente porque el equipo siempre reporta nivel 0 para fuentes PC. | 50 | 0–100 | `PcMicGain` |
| +ACC | Botón de activación | Habilita la mezcla de entrada de micrófono accesorio. | — | On / Off | — |
| PROC | Botón de activación | Activa o desactiva el procesador de voz. | — | On / Off | — |
| NOR/DX/DX+ | Control deslizante | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2). | NOR (0) | 0, 1, 2 | — |
| DAX | Botón de activación | Habilita DAX como fuente de audio de TX. | — | On / Off | — |
| MON | Botón de activación | Habilita el monitor de TX en banda lateral. | — | On / Off | — |
| Monitor volume | Control deslizante | Establece el volumen del monitor de banda lateral. | — | 0–100 | — |

### Subpanel CW

| Control | Tipo | Qué hace | Valor predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|---|
| ALC | Medidor | Muestra la lectura del control automático de nivel. Rojo por encima de 80. | — | 0–100 | — |
| Delay | Control deslizante | Establece el retardo de break-in de CW en milisegundos. | — | 0–2000 ms (paso 10) | — |
| Speed | Control deslizante | Establece la velocidad de manipulación CW. | — | 5–100 WPM | — |
| Breakin | Botón de activación | Activa o desactiva el break-in completo (QSK). | — | On / Off | — |
| Iambic | Botón de activación | Activa o desactiva el manipulador de paleta iámbica. | — | On / Off | — |
| Pitch < / > | Cuadro de número | Ajusta el tono de sidetone y decodificación de CW en pasos de 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | — |
| Sidetone | Botón de activación | Activa o desactiva simultáneamente el monitor de sidetone CW del equipo (alimentado por DAX) y el generador de sidetone CW de baja latencia del lado del cliente. | — | On / Off | — |
| Sidetone volume | Control deslizante | Establece simultáneamente el volumen del monitor CW del equipo (mon_gain_cw) y el volumen del generador de sidetone del lado del cliente. | — | 0–100 | — |
| L / R pan (CW) | Control deslizante | Posición de paneo del monitor CW. Aplica paneo de potencia constante tanto al monitor del equipo como al generador de sidetone local. Haga doble clic para centrar. | 50 | 0–100 | — |

### Comportamiento del sidetone (v0.9.1+)

El botón de activación **Sidetone** y el control deslizante **Sidetone volume** controlan simultáneamente el monitor alimentado por DAX del equipo y el generador de sidetone CW de baja latencia del lado del cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia). No existe un botón de activación ni un control de volumen independiente para el sidetone local. El tono y el paneo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del equipo — no se requiere ni está disponible ningún ajuste manual.

El sidetone local es adecuado para transmisiones con paleta, llave recta y generadas por CWX, donde la latencia de ida y vuelta por red haría inutilizable el monitor alimentado por DAX del equipo a velocidades más altas.

## Consejos

- El valor de `PcMicGain` se almacena únicamente en el lado del cliente. Si cambia la fuente de micrófono desde PC y vuelve a ella, AetherSDR restaura el valor guardado en lugar de leerlo del equipo.
- Como el tono y el paneo siempre siguen los ajustes del equipo automáticamente, ajuste el tono de CW con el cuadro de número **Pitch < / >** y el paneo con el control deslizante **L / R pan (CW)** — tanto el monitor del equipo como el sidetone local se actualizan juntos.
- El botón de activación **Sidetone** habilita o deshabilita el sidetone local al mismo tiempo que el monitor del equipo. No es posible habilitar uno independientemente del otro.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
- [Habilitar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono de CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
