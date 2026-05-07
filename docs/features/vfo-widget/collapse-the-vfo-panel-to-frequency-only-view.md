# Contraer el panel VFO a una vista solo de frecuencia

Cuando el espacio en pantalla es limitado, puede contraer el panel VFO a una tira compacta que muestra únicamente la frecuencia del segmento. El estado contraído se guarda por segmento, por lo que persiste entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del segmento debe estar abierto. Si no está visible, haga clic en la bandera marcadora VFO en la visualización del espectro de ese segmento.

## Pasos

1. Localice la etiqueta del segmento en el área del encabezado del panel VFO. La etiqueta muestra el identificador del segmento (por ejemplo, **A** o **B**).
2. Haga clic en la etiqueta del segmento. El panel se contrae a una tira compacta que solo muestra la frecuencia.
3. Para restaurar el panel completo, haga clic en cualquier lugar de la tira contraída.

## Función de cada control

| Control                      | Predeterminado                                                                                                                         | Configuración persistida                                                                                               |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Alternar contracción         | Expandido                                                                                                                              | `SliceFlagCollapsed_{N}`                                                                                               |
| Botón antena RX              | Abre el menú de selección de antena para la antena receptora de este segmento.                                                         | Ninguna                                                                                                                |
| Botón antena TX              | Abre el menú de selección de antena para la antena transmisora de este segmento.                                                       | Ninguna                                                                                                                |
| Visualización de frecuencia  | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. | Ninguna                                                                                                                |
| Etiqueta de ancho de filtro  | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0,1 kHz que afectaba las lecturas de modo SSB/digital (#2197, v0.9.8). | Ninguna |
| Deslizador de ganancia AF (pestaña Audio) | 100                                                                                                                          | Ninguna — refleja el estado en vivo de la radio.                                                                       |
| Deslizador de paneo (pestaña Audio) | 50                                                                                                                               | Ninguna                                                                                                                |
| Botón de silencio (pestaña Audio) | Desactivado                                                                                                                        | Ninguna                                                                                                                |
| Botón + deslizador de silenciador (pestaña Audio) | Desactivado                                                                                                          | Ninguna                                                                                                                |
| Combinado AGC (pestaña Audio) | FAST                                                                                                                                   | Ninguna                                                                                                                |
| Botón NR (pestaña DSP)       | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón NB (pestaña DSP)       | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón ANF (pestaña DSP)      | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón APF (pestaña DSP)      | Desactivado (visible solo en modo CW)                                                                                                  | Ninguna                                                                                                                |
| Botón NRL (pestaña DSP)      | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón NRS (pestaña DSP)      | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón RNN (pestaña DSP)      | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón NRF (pestaña DSP)      | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón ANFL (pestaña DSP)     | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón ANFT (pestaña DSP)     | Desactivado                                                                                                                            | Ninguna                                                                                                                |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene el estilo de una palanca DSP del lado de la radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Activa o desactiva la tira de canal de audio Aetherial — la suite unificada de DSP de TX/RX (v0.9.8).                           | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combinado Mode (pestaña Mode) | USB                                                                                                                                   | Ninguna                                                                                                                |
| Botones de preajuste de filtro (pestaña Mode) | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura.        | `FilterPresets`                                                                                                         |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Desactivado                                                                                                                | Ninguna                                                                                                                |
| Combinado de canal DAX (pestaña DAX) | Desactivado                                                                                                                      | Ninguna                                                                                                                |
| Botón de grosor del marcador  | 1 px                                                                                                                                  | `Slice{N}_MarkerWidth`                                                                                                 |
| Botón de bordes de filtro    | Mostrado                                                                                                                              | `Slice{N}_FilterEdgesHidden`                                                                                            |

La configuración `SliceFlagCollapsed_{N}` se almacena por segmento, donde `{N}` es el número del segmento. Contraer un segmento no afecta a otros segmentos.

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO ahora muestra solo los algoritmos de reducción de ruido y filtrado suministrados directamente por la radio. Los siguientes botones se han eliminado de la cuadrícula de la pestaña DSP:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (eliminación de ruido neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener en macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos algoritmos de procesamiento del lado del cliente siguen estando disponibles. Acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

Los botones que permanecen en la cuadrícula de la pestaña DSP están dispuestos en un diseño de cuatro columnas. Los botones ADSP y AetherVoice se colocan debajo de los botones DSP del lado de la radio:

| Posición | Botón |
|---|---|
| Fila 0, Col 0 | NR |
| Fila 0, Col 1 | NB |
| Fila 0, Col 2 | ANF |
| Fila 0, Col 3 | APF (visible solo en modo CW) |
| Fila 1, Col 0 | NRL |
| Fila 1, Col 1 | NRS |
| Fila 1, Col 2 | RNN |
| Fila 1, Col 3 | NRF |
| Fila 2, Col 0 | ANFL |
| Fila 2, Col 1 | ANFT |
| Fila 3, Col 0 | ADSP |
| Fila 3, Cols 1-2 | AetherVoice (ocupa 2 columnas) |

### Deslizador de nivel DSP

Una fila de deslizador de nivel compartido aparece debajo de la cuadrícula de botones DSP. El deslizador apunta al algoritmo DSP con nivel que se haya activado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor numérico se muestra a la derecha.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP activo. Se reorienta automáticamente cuando activa un algoritmo diferente. |

La fila del deslizador permanece en el diseño en todo momento. Cuando ningún algoritmo compatible está activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del deslizador se atenúa y no responde a la entrada. Al activar un algoritmo compatible, la fila se vuelve visible y el deslizador se reorienta hacia ese algoritmo.

Algoritmos a los que el deslizador de nivel puede apuntar: NR, NB, ANF, NRL, NRS, NRF, ANFL.

El deslizador de nivel ahora refleja correctamente el estado de la radio en la conexión inicial. Cuando un algoritmo DSP con nivel ya está activo en el perfil guardado de la radio, el deslizador aparece inmediatamente sin necesidad de una activación manual (#startup-slider, v0.9.8).

## Consejos

- En la vista contraída, al desplazar la rueda del ratón sobre la tira se sintoniza la frecuencia del segmento según el tamaño de paso actual, de la misma manera que al desplazarse sobre la visualización de frecuencia en el panel completo.
- En la vista contraída, al hacer clic en la etiqueta TX pintada en la tira se alterna la asignación de TX para ese segmento. Al hacer clic en cualquier otro lugar de la tira se expande el panel.
- El panel se voltea automáticamente al lado derecho del marcador VFO si al expandirlo se cortara con el borde de la ventana. Este comportamiento se aplica tanto en el estado expandido como en el contraído.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la visualización del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Relacionados

- [VFO Panel overview](overview.md)
- [Tune the radio by typing a frequency into the VFO panel](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Hide or show filter edge lines on the spectrum](hide-or-show-filter-edge-lines-on-the-spectrum.md)
