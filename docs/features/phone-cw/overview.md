# Descripción general de Phone/CW

El applet Phone/CW es un panel de transmisión adaptado al modo que ofrece controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a los controles de CW cuando el slice activo está en un modo CW. Ábralo para ajustar el audio de transmisión, configurar los parámetros de manipulación o configurar el sidetone CW local de baja latencia.

## Cómo funciona

El applet siempre está presente en el Panel de Applets de la barra lateral derecha. Actívelo o desactívelo con el botón de bandeja **P/CW**. Contiene dos subpaneles gestionados mediante un diseño apilado:

- **Subpanel Phone** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **Subpanel CW** — visible cuando el slice activo está en un modo CW.

AetherSDR cambia entre subpaneles automáticamente al cambiar el modo del slice. No es necesario cambiarlos manualmente.

### Subpanel Phone

| Control | Tipo | Función | Valor predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|---|
| Level | Medidor | Muestra el nivel de pico de entrada del micrófono en dBFS. Indica -150 cuando el medidor está inactivo y no se está transmitiendo. | — | -40 a +10 dBFS (rojo por encima de 0) | — |
| Compression | Medidor | Muestra la cantidad de compresión de voz en dB (relleno invertido: mayor compresión rellena hacia la izquierda). | — | -25 a 0 dB | — |
| Mic profile | Cuadro combinado | Carga el perfil de procesamiento de micrófono indicado desde la lista de perfiles del equipo. | — | Proviene del equipo | — |
| Mic source | Cuadro combinado | Selecciona la fuente de entrada del micrófono. | — | MIC, BAL, LINE, ACC, PC | — |
| Mic gain | Control deslizante | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se mantiene en el lado del cliente porque el equipo siempre reporta el nivel 0 para fuentes PC. | 50 | 0–100 | `PcMicGain` |
| +ACC | Botón de alternancia | Activa la mezcla de entrada del micrófono accesorio. | — | Activado / Desactivado | — |
| PROC | Botón de alternancia | Activa o desactiva el procesador de voz. | — | Activado / Desactivado | — |
| NOR/DX/DX+ | Control deslizante | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2). | NOR (0) | 0, 1, 2 | — |
| DAX | Botón de alternancia | Activa DAX como fuente de audio de TX. | — | Activado / Desactivado | — |
| MON | Botón de alternancia | Activa el monitor de TX de banda lateral. | — | Activado / Desactivado | — |
| Monitor volume | Control deslizante | Establece el volumen del monitor de banda lateral. | — | 0–100 | — |

### Subpanel CW

| Control | Tipo | Función | Valor predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|---|
| ALC | Medidor | Muestra la lectura del control automático de nivel. Rojo por encima de 80. | — | 0–100 | — |
| Delay | Control deslizante | Establece el retardo de break-in de CW en milisegundos. | — | 0–2000 ms (paso 10) | — |
| Speed | Control deslizante | Establece la velocidad de manipulación CW. | — | 5–100 WPM | — |
| Breakin | Botón de alternancia | Activa o desactiva el break-in completo (QSK). | — | Activado / Desactivado | — |
| Iambic | Botón de alternancia | Activa o desactiva el manipulador de paleta iámbica. | — | Activado / Desactivado | — |
| Pitch < / > | Cuadro de giro | Ajusta el tono del sidetone y la decodificación de CW en pasos de 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | — |
| Sidetone | Botón de alternancia | Activa o desactiva el monitor de sidetone CW del equipo (alimentado por DAX). | — | Activado / Desactivado | — |
| Sidetone volume | Control deslizante | Establece el volumen del monitor CW del equipo. | — | 0–100 | — |
| L / R pan | Control deslizante | Posición de paneo del monitor CW. | 50 | 0–100 | — |
| Local STn | Botón de alternancia | Activa o desactiva el sidetone CW local de baja latencia generado por el motor de audio de AetherSDR (~10 ms de latencia). Independiente del monitor del equipo alimentado por DAX. Funciona con paleta, manipulador recto y transmisiones generadas por CWX. | Desactivado | Activado / Desactivado | `CwLocalSidetoneEnabled` |
| Local sidetone volume | Control deslizante | Establece el volumen del sidetone local de forma independiente a la ganancia del monitor del equipo. | 50 | 0–100 | `CwLocalSidetoneVolume` |
| Follow | Botón de alternancia | Cuando está activado, el tono del sidetone local sigue la configuración de tono CW del equipo. Cuando está desactivado, se habilita el control deslizante de tono manual. | Activado | Activado / Desactivado | `CwLocalSidetonePitchFollow` |
| Local sidetone pitch | Control deslizante | Ajuste manual del tono del sidetone local en Hz. Solo activo cuando Follow está desactivado. | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` |

### Sidetone del equipo vs. sidetone local

El sidetone del equipo (Sidetone / Sidetone volume) se enruta a través de la ruta del monitor DAX del equipo y tiene la latencia típica del audio en red. El sidetone local (Local STn) se genera completamente dentro del motor de audio de AetherSDR con aproximadamente 10 ms de latencia, lo que lo hace más adecuado para operación con paleta y manipulador recto. Ambos pueden estar activos simultáneamente.

## Consejos

- El valor de `PcMicGain` se almacena únicamente en el lado del cliente. Si cambia la fuente del micrófono desde PC y vuelve a ella, AetherSDR restaura el valor guardado en lugar de leerlo del equipo.
- El control deslizante de tono del sidetone local aparece atenuado mientras Follow está activado. Desactive Follow antes de intentar establecer un tono manual.
- Local STn responde tanto al texto generado por CWX como a la manipulación por hardware, por lo que puede usarlo como única fuente de sidetone durante la operación de CW por teclado.

## Temas relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y activar la mezcla accesoria](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
- [Activar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- [Activar el sidetone CW local de baja latencia (Local STn) para operación rápida con paleta, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Ajustar el volumen del sidetone local de forma independiente al monitor del equipo](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
- [Hacer que el tono del sidetone local siga el tono CW del equipo, o ajustarlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
