# Contraer el panel VFO a vista solo de frecuencia

Cuando el espacio en pantalla es limitado, puede contraer el panel VFO a una franja compacta que muestra solo la frecuencia del segmento. El estado contraído se guarda por segmento, por lo que persiste entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del segmento debe estar abierto. Si no está visible, haga clic en la bandera marcadora VFO en la pantalla del espectro de ese segmento.

## Pasos

1. Localice la insignia del segmento en el área del encabezado del panel VFO. La insignia muestra el identificador del segmento (por ejemplo, **A** o **B**).
2. Haga clic en la insignia del segmento. El panel se contrae a una franja compacta que solo muestra la frecuencia.
3. Para restaurar el panel completo, haga clic en cualquier lugar de la franja contraída.

## Función de cada control

| Control                      | Predeterminado                                                                                                                              | Configuración persistente                                                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Alternar contracción         | Expandido                                                                                                                                    | `SliceFlagCollapsed_{N}`                                                                                               |
| Botón antena RX              | Abre el menú de selección de antena para la antena receptora de este segmento. Usa la `rxAntennaList` del segmento si está disponible; de lo contrario, recurre a la lista de antenas de la radio. | Ninguna |
| Botón antena TX              | Abre el menú de selección de antena para la antena transmisora de este segmento. Filtra puertos de antena solo RX. Usa la `txAntennaList` del segmento si está disponible. | Ninguna |
| Visualización de frecuencia  | Muestra la frecuencia actual del segmento. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. | Ninguna |
| Etiqueta ancho de filtro     | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones predefinidos de filtros en la pestaña Modo. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). | Ninguna |
| Insignia del segmento        | Muestra la letra del segmento. Haga clic para contraer el panel. Muestra texto formateado en HTML (#2606).                                   | Ninguna                                                                                                                |
| Deslizador Ganancia AF (pestaña Audio) | 100                                                                                                                                | Ninguna — refleja el estado en vivo de la radio.                                                                       |
| Deslizador Pan (pestaña Audio)       | 50                                                                                                                                 | Ninguna                                                                                                                |
| Botón Silenciar (pestaña Audio)      | Desactivado                                                                                                                        | Ninguna                                                                                                                |
| Botón + deslizador Squelch (pestaña Audio) | Desactivado                                                                                                                  | Ninguna                                                                                                                |
| Combinado AGC (pestaña Audio)        | FAST                                                                                                                             | Ninguna                                                                                                                |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Desactivados                                                                                             | Ninguna                                                                                                                |
| Botón ADSP (pestaña DSP)      | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Configuración (v0.9.8). | Estilizado como un conmutador DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo de configuración modeless de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna el Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                                                    | Ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para el canal. |
| Combinado Modo (pestaña Modo)        | USB                                                                                                                                | Ninguna                                                                                                                |
| Botones predefinidos de filtros (pestaña Modo) | Aplica un ancho de filtro predefinido guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | `FilterPresets`                                                                                                        |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Desactivados                                                                                                                  | Ninguna                                                                                                                |
| Combinado canal DAX (pestaña DAX)  | Desactivado                                                                                                                        | Ninguna                                                                                                                |
| Botón grosor del marcador      | 1 px                                                                                                                                 | `Slice{N}_MarkerWidth`                                                                                                 |
| Botón bordes del filtro        | Mostrado                                                                                                                          | `Slice{N}_FilterEdgesHidden`                                                                                            |

La configuración `SliceFlagCollapsed_{N}` se almacena por segmento, donde `{N}` es el número del segmento. Contraer un segmento no afecta a otros segmentos.

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO ahora muestra solo los algoritmos de reducción de ruido y filtrado suministrados directamente por la radio. Se han eliminado los siguientes botones de la cuadrícula de la pestaña DSP:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (eliminación de ruido neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener para macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos algoritmos de procesamiento del lado del cliente aún están disponibles. Acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

Los botones que permanecen en la cuadrícula de la pestaña DSP ahora están dispuestos en un diseño de cuatro columnas con todos los botones DSP del lado del cliente presentes:

| Posición | Botón |
|---|---|
| Fila 0, Col 0 | NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR |
| Fila 0, Col 1 | NRL |
| Fila 0, Col 2 | NRS |
| Fila 0, Col 3 | RNN |
| Fila 1, Col 0 | NRF |
| Fila 1, Cols 1-3 | (vacío) |
| Fila 2, Col 0 | ADSP |
| Fila 2, Cols 1-2 | AetherVoice (ocupa 2 columnas) |

Nota: La entrada del botón NR en la cuadrícula ahora representa un grupo de botones de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR). Los botones específicos que se muestran dependen de la serie de radio y la configuración de compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo.

### Deslizador de nivel DSP

Una fila de deslizador de nivel compartido aparece debajo de la cuadrícula de botones DSP. El deslizador apunta al algoritmo DSP nivelado habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor numérico se muestra a la derecha.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP activo. Se reorienta automáticamente cuando habilita un algoritmo diferente. |

La fila del deslizador permanece en el diseño en todo momento. Cuando ningún algoritmo compatible está activo — o cuando solo RNN, ANFT o APF están activados — la fila del deslizador se atenúa y no responde a la entrada. Habilitar un algoritmo compatible atenúa la fila de nuevo y reorienta el deslizador a ese algoritmo.

Algoritmos que el deslizador de nivel puede apuntar: NR, NB, ANF, NRL, NRS, NRF, ANFL.

El deslizador de nivel ahora refleja correctamente el estado de la radio en la conexión inicial. Cuando un algoritmo DSP nivelado ya está activo en el perfil guardado de la radio, el deslizador aparece inmediatamente sin necesidad de una activación manual (#startup-slider, v0.9.8).

### Comportamiento del Squelch en modo RTTY

A partir de v26.5.1, el botón y el deslizador de squelch están deshabilitados en modo RTTY. El squelch de la radio bloquea las señales FSK débiles, lo que interfiere con decodificadores externos que esperan un flujo de audio continuo a través de DAX. Si el squelch estaba activado al cambiar al modo RTTY, se desactiva automáticamente. El estado guardado del squelch se restaura al cambiar de nuevo a un modo de voz.

## Entrada de frecuencia en bandas XVTR

Al ingresar una frecuencia en bandas XVTR (rango de 100–999 MHz), el panel VFO aplica una conversión de conveniencia: una entrada de entero simple como `1446` se interpreta como `144.6 MHz` insertando un decimal después del tercer dígito. Esto solo se aplica cuando:
- El segmento está sintonizado en una banda XVTR (frecuencia superior a 54 MHz o usando una antena que comience con `XVT`)
- La frecuencia actual está en el rango de 100–999 MHz (banda de tres dígitos)
- El valor ingresado es superior a 450 MHz y no contiene un punto decimal

Para frecuencias en bandas de 23cm y microondas (superiores a 1000 MHz), un entero simple se interpreta directamente como MHz (por ejemplo, `1296` significa `1296 MHz`, no `129.6 MHz`).

La entrada de frecuencia acepta valores de hasta 50000 MHz en bandas XVTR.

## Consejos

- En la vista contraída, desplazar la rueda del ratón sobre la franja sintoniza la frecuencia del segmento en el paso de tamaño actual, igual que al desplazarse sobre la visualización de frecuencia en el panel completo.
- En la vista contraída, al hacer clic en la insignia TX pintada en la franja se alterna la asignación de TX para ese segmento. Al hacer clic en cualquier otro lugar de la franja se expande el panel.
- El panel se voltea automáticamente al lado derecho del marcador VFO si al expandirlo se recortaría contra el borde de la ventana. Este comportamiento se aplica tanto en estado expandido como contraído.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la pantalla del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Relacionados

- [Descripción general del panel VFO](overview.md)
- [Sintonice la radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Cambie el grosor de la línea del marcador VFO](change-the-vfo-marker-line-thickness.md)
- [Oculte o muestre las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
