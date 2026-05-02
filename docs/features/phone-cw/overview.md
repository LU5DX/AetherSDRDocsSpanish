# Descripción general de Phone/CW

El applet Phone/CW es un panel de transmisión adaptado al modo activo: proporciona controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a los controles de CW cuando el slice activo está en un modo CW. Ábralo para ajustar el audio de transmisión o configurar los parámetros de manipulación.

## Cómo funciona

El applet está siempre presente en el Panel de Applets de la barra lateral derecha. Actívelo o desactívelo con el botón **P/CW** de la bandeja. Contiene dos subpaneles organizados en un diseño apilado:

- **Subpanel Phone** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **Subpanel CW** — visible cuando el slice activo está en un modo CW.

AetherSDR alterna entre subpaneles automáticamente al cambiar el modo del slice. No es necesario cambiarlos manualmente.

### Subpanel Phone

| Control | Tipo | Función |
|---|---|---|
| Level | Medidor | Muestra el nivel de pico de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no se está transmitiendo. Excepción: cuando la fuente de micrófono es PC, el indicador utiliza medición del lado del cliente y no es suprimido por met_in_rx (#2086). |
| Compression | Medidor | Muestra la cantidad de compresión de voz en dB (relleno inverso: mayor compresión rellena hacia la izquierda). |
| Mic profile | Cuadro combinado | Carga el perfil de procesamiento de micrófono indicado desde la lista de perfiles del equipo. |
| Mic source | Cuadro combinado | Selecciona la fuente de entrada del micrófono. |
| Mic gain | Control deslizante | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se mantiene en el lado del cliente porque el equipo siempre informa nivel 0 para fuentes PC. |
| +ACC | Botón de alternancia | Activa la mezcla de entrada del micrófono accesorio. |
| PROC | Botón de alternancia | Activa o desactiva el procesador de voz. |
| NOR/DX/DX+ | Control deslizante | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2). |
| DAX | Botón de alternancia | Habilita DAX como fuente de audio TX. |
| MON | Botón de alternancia | Activa el monitor TX de banda lateral. |
| Monitor volume | Control deslizante | Establece el volumen del monitor de banda lateral. |

### Subpanel CW

| Control | Tipo | Función | Valor predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|---|
| ALC | Medidor | Muestra la lectura del control automático de nivel. Rojo por encima de 80. | — | 0–100 | — |
| Delay | Control deslizante | Establece el retardo de break-in de CW en milisegundos. | — | 0–2000 ms (paso 10) | — |
| Speed | Control deslizante | Establece la velocidad de manipulación CW. | — | 5–100 WPM | — |
| Breakin | Botón de alternancia | Activa o desactiva el full break-in (QSK). | — | On / Off | — |
| Iambic | Botón de alternancia | Activa o desactiva el manipulador de paleta iámbico. | — | On / Off | — |
| Pitch < / > | Cuadro de número | Incrementa o decrementa el tono de sidetone y decodificación CW en 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | — |
| Sidetone | Botón de alternancia | Activa o desactiva simultáneamente el monitor de sidetone CW del equipo (alimentado por DAX) y el generador de sidetone CW de baja latencia del lado del cliente. En Windows, el flujo de sidetone se inicia inmediatamente al conectar (#2105). | — | On / Off | — |
| Sidetone volume | Control deslizante | Establece simultáneamente el volumen del monitor CW del equipo (mon_gain_cw) y el volumen del generador de sidetone del lado del cliente. | — | 0–100 | — |
| L / R pan (CW) | Control deslizante | Posición de paneo del monitor CW. Aplica paneo de potencia constante tanto al monitor del equipo como al generador de sidetone local. Doble clic para centrar. | 50 | 0–100 | — |

### Comportamiento del sidetone (v0.9.1+)

El botón **Sidetone** y el control deslizante **Sidetone volume** controlan simultáneamente el monitor del equipo alimentado por DAX y el generador de sidetone CW de baja latencia del lado del cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia). No existe un botón de alternancia ni un control de volumen independiente para el sidetone local. El tono y el paneo siguen siempre automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del equipo; no se requiere ni se permite ninguna anulación manual.

El sidetone local es adecuado para transmisiones con paleta, llave recta y generadas por CWX, donde la latencia de ida y vuelta por red haría inutilizable el monitor DAX del equipo a velocidades más altas.

### Comportamiento de VOX y atajos de teclado (v0.9.3)

Cuando se activa VOX mediante un atajo de teclado, el panel Phone ahora se actualiza inmediatamente para reflejar el nuevo estado de VOX (#2084). En versiones anteriores, el panel no se actualizaba hasta que ocurría algún otro evento de interfaz.

## Sugerencias

- El valor `PcMicGain` se almacena únicamente en el lado del cliente. Si cambia la fuente del micrófono desde PC y vuelve a ella, AetherSDR restaura el valor guardado en lugar de leerlo del equipo.
- Cuando la fuente del micrófono es PC, el indicador Level utiliza medición del lado del cliente y aparece inmediatamente al conectar, independientemente del ajuste met_in_rx.
- Dado que el tono y el paneo siempre siguen los ajustes del equipo automáticamente, ajuste el tono CW con el cuadro de número **Pitch < / >** y el paneo con el control deslizante **L / R pan (CW)**; tanto el monitor del equipo como el sidetone local se actualizan de forma conjunta.
- El botón **Sidetone** activa o desactiva el sidetone local al mismo tiempo que el monitor del equipo. No es posible habilitar uno de forma independiente del otro.

## Temas relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y activar la mezcla accesoria](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
- [Activar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
