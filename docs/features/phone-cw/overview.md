# Descripción general de Phone/CW

El applet Phone/CW es un panel de transmisión consciente del modo que proporciona controles de micrófono, procesador y monitor en modos de voz, e intercambia automáticamente a controles de CW cuando el slice activo está en un modo CW. Ábralo para ajustar el audio de transmisión o establecer parámetros de tecleo.

## Cómo funciona

El applet siempre está presente en el Applet Panel en la barra lateral derecha. Actívelo o desactívelo usando el botón de bandeja **P/CW**. Contiene dos subpaneles administrados por un diseño apilado:

- **Subpanel Phone** — visible cuando el slice activo está en un modo de voz (SSB, AM, FM y similares).
- **Subpanel CW** — visible cuando el slice activo está en un modo CW.

AetherSDR cambia entre subpaneles automáticamente cuando modifica el modo del slice. Usted no los cambia manualmente.

### Subpanel Phone

| Control        | Tipo          | Qué hace                                                                                                                                                                                                                             |
|----------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level          | Medidor       | Muestra el nivel máximo de entrada del micrófono en dBFS. Se suprime a -150 cuando met_in_rx está desactivado y no está transmitiendo. Excepción: cuando la fuente de micrófono es PC, el medidor usa medición del lado del cliente y no se suprime por met_in_rx (#2086). |
| Compression    | Medidor       | Muestra la cantidad de compresión de voz en dB (relleno invertido — mayor compresión rellena hacia la izquierda).                                                                                                                                                   |
| Mic profile    | Cuadro combinado     | Carga el perfil de procesamiento de micrófono nombrado de la lista de perfiles de la radio.                                                                                                                                                                    |
| Mic source     | Cuadro combinado     | Selecciona la fuente de entrada de micrófono.                                                                                                                                                                                                     |
| Mic gain       | Deslizador        | Ajusta el nivel de entrada del micrófono. Cuando la fuente es PC, el valor se mantiene del lado del cliente porque la radio siempre reporta nivel 0 para fuentes PC.                                                                                                       |
| +ACC           | Botón de alternancia | Habilita la mezcla de entrada del micrófono accesorio.                                                                                                                                                                                                     |
| PROC           | Botón de alternancia | Alterna el procesador de voz.                                                                                                                                                                                            |
| NOR/DX/DX+     | Deslizador        | Establece el nivel del procesador de voz. Tres posiciones: NOR (0), DX (1), DX+ (2).                                                                                                                                             |
| DAX            | Botón de alternancia | Habilita DAX como fuente de audio TX.                                                                                                                                                                                                      |
| MON            | Botón de alternancia | Habilita el monitor TX de banda lateral.                                                                                                                                                                                                         |
| Monitor volume | Deslizador        | Establece el volumen del monitor de banda lateral.                                                                                                                                                                                                        |

### Subpanel CW

| Control | Tipo | Qué hace | Predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|---|
| ALC | Medidor | Muestra la lectura del control de nivel automático. Rojo arriba de 80. | — | 0–100 | — |
| Delay | Deslizador | Establece el retardo de ruptura de CW en milisegundos. | — | 0–2000 ms (paso 10) | — |
| Speed | Deslizador | Establece la velocidad de tecleo de CW. | — | 5–100 WPM | — |
| Breakin | Botón de alternancia | Alterna la ruptura completa (QSK). | — | Activado / Desactivado | — |
| Iambic | Botón de alternancia | Alterna el teclador de paleta iámbico. | — | Activado / Desactivado | — |
| Pitch < / > | Cuadro de ajuste | Incrementa el tono lateral y la frecuencia de decodificación de CW en pasos de 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | — |
| Sidetone | Botón de alternancia | Alterna el monitor lateral de CW de la radio (alimentado por DAX) y el generador lateral de CW de baja latencia del lado del cliente en sincronización. En Windows, la transmisión lateral ahora se inicia inmediatamente al conectar (#2105). | — | Activado / Desactivado | — |
| Sidetone volume | Deslizador | Establece el volumen del monitor lateral de la radio (mon_gain_cw) y el volumen del generador lateral del lado del cliente en sincronización. | — | 0–100 | — |
| L / R pan (CW) | Deslizador | Posición de panorámica del monitor CW. Aplica panorámica de potencia constante tanto al monitor de la radio como al generador lateral local. Haga doble clic para recentrar. | 50 | 0–100 | — |

### Comportamiento de sidetone (v0.9.1+)

El botón de alternancia **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador lateral de CW de baja latencia del lado del cliente (CwSidetoneGenerator, aproximadamente 10 ms de latencia) en sincronización. No hay un botón de alternancia de sidetone local separado ni un deslizador de volumen. El tono y la panorámica siempre siguen automáticamente los parámetros `cw_pitch` y `mon_pan_cw` de la radio — no se requiere ni está disponible ningún ajuste manual.

El sidetone local es adecuado para transmisiones generadas por paleta, llave recta y CWX donde la latencia de ida y vuelta de la red haría que el monitor alimentado por DAX de la radio fuera inutilizable a velocidades más altas.

### Comportamiento de VOX y acceso directo de teclado (v0.9.3)

Cuando VOX se alterna mediante un acceso directo de teclado, el panel Phone ahora se actualiza inmediatamente para reflejar el nuevo estado de VOX (#2084). En versiones anteriores el panel no se actualizaba hasta que ocurría otro evento de interfaz de usuario.

## Consejos

- El valor `PcMicGain` se almacena solo del lado del cliente. Si cambia la fuente del micrófono desde PC y vuelve atrás, AetherSDR restaura el valor guardado en lugar de leer desde la radio.
- Cuando la fuente del micrófono es PC, el medidor Level usa medición del lado del cliente y aparece inmediatamente al conectar, independientemente de la configuración met_in_rx.
- Como el tono y la panorámica siempre siguen automáticamente los parámetros de la radio, ajuste el tono de CW usando el cuadro de ajuste **Pitch < / >** y la panorámica usando el deslizador **L / R pan (CW)** — tanto el monitor de la radio como el sidetone local se actualizan juntos.
- El botón de alternancia **Sidetone** habilita o deshabilita el sidetone local al mismo tiempo que el monitor de la radio. No puede habilitar uno independientemente del otro.

## Relacionado

- [Seleccione una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajuste la ganancia del micrófono y habilite la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccione un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilite el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Escuche un monitor lateral de TX](listen-to-a-tx-sidetone-monitor.md)
- [Establezca la velocidad de tecleo de CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establezca el retardo de ruptura de CW](set-cw-break-in-delay.md)
- [Habilite el tecleo de paleta iámbico](enable-iambic-paddle-keying.md)
- [Cambie el tono de CW / frecuencia lateral](change-cw-pitch-sidetone-frequency.md)
