# Activar el offset RIT o XIT desde el panel VFO

RIT (Receiver Incremental Tuning) y XIT (Transmitter Incremental Tuning) le permiten desplazar la frecuencia de recepción o transmisión en un pequeño offset sin mover el VFO principal. Esto es útil para trabajar contactos en frecuencias divididas o para compensar una estación que está ligeramente fuera de la frecuencia del dial.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO para el slice de destino debe estar abierto y expandido. Si está colapsado a la tira de solo frecuencia, haga clic en cualquier parte para expandirlo.

## Pasos

1. Haga clic en el marcador VFO en la pantalla del espectro para el slice que desea ajustar. El panel VFO aparece anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el offset de recepción, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el offset RIT actual.
4. Para habilitar el offset de transmisión, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el offset XIT actual.
5. Con RIT o XIT activo, coloque el puntero del mouse sobre el botón correspondiente y gire la rueda del mouse para ajustar el offset. Cada paso de la rueda cambia el offset en 10 Hz.
6. Para deshabilitar RIT o XIT, haga clic en el botón activo nuevamente.

## Qué hace cada control

| Control                          | Tipo                                                                                                                                  | Valor predeterminado                                                                                                      |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX               | Botón pulsador                                                                                                                        | Abre el menú de selección de antena para la antena receptora de este slice.                                                |
| Botón de antena TX               | Botón pulsador                                                                                                                        | Abre el menú de selección de antena para la antena transmisora de este slice.                                              |
| Visualización de frecuencia      | Indicador                                                                                                                             | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro      | Indicador                                                                                                                             | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente de verdad única, corrigiendo un offset de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Deslizador de ganancia AF (pestaña Audio) | Deslizador                                                                                                                         | 100                                                                                                                       |
| Deslizador de paneo (pestaña Audio) | Deslizador                                                                                                                         | 50                                                                                                                        |
| Botón de silencio (pestaña Audio) | Botón de alternancia                                                                                                                  | off                                                                                                                       |
| Botón + deslizador de squelch (pestaña Audio) | Botón de alternancia                                                                                                             | off                                                                                                                       |
| Combobox AGC (pestaña Audio)     | Combobox                                                                                                                              | FAST                                                                                                                      |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia                                                                                  | off                                                                                                                       |
| Botón ADSP (pestaña DSP)         | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un botón de alternancia DSP del lado de la radio pero sin posibilidad de marcar. Al hacer clic, abre y enfoca el diálogo no modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP)  | Activa la tira de canal de audio Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8).                                           | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada de menú/cadena existentes para la tira. |
| Deslizador de nivel DSP (pestaña DSP) | Deslizador                                                                                                                         | Establece la profundidad de procesamiento para la función DSP compatible activada más recientemente en este slice. La etiqueta a la izquierda identifica el objetivo actual. La fila se atenúa cuando ninguna función DSP elegible está activa. No se persiste; refleja el estado en vivo de la radio. |
| Combobox de modo (pestaña Mode)  | Combobox                                                                                                                              | USB                                                                                                                       |
| Botones de preselección de filtro (pestaña Mode) | Botón pulsador                                                                                                                       | Persistido en FilterPresets                                                                                               |
| Botones + etiquetas RIT / XIT   | Botón de alternancia                                                                                                                  | off                                                                                                                       |
| Combobox de canal DAX (pestaña DAX) | Combobox                                                                                                                           | Off                                                                                                                       |
| Botón de grosor del marcador    | Botón pulsador                                                                                                                        | 1 px                                                                                                                      |
| Botón de bordes de filtro       | Botón de alternancia                                                                                                                  | shown (mostrado)                                                                                                          |
| Alternancia de colapso          | Botón de alternancia                                                                                                                  | expanded (expandido)                                                                                                      |
| Distintivo TX                   | Indicador                                                                                                                             | Muestra TX (rojo) cuando este slice es el slice de transmisión activo. Oculto en caso contrario.                          |
| Distintivo SPLIT                | Indicador                                                                                                                             | Muestra SPLIT (ámbar) cuando TX está asignado a un slice diferente al slice de recepción activo. Oculto en caso contrario. |

**Botón de antena RX** — Abre un menú de selección de antena para la antena receptora de este slice. El menú ahora usa la propiedad `rxAntennaList()` por slice cuando está disponible, recurriendo a la lista de antenas global. Los elementos del menú muestran una etiqueta legible junto al identificador interno de la antena.

**Botón de antena TX** — Abre un menú de selección de antena para la antena transmisora de este slice. El menú filtra los puertos de antena solo de recepción. Usa el helper `txAntennaOptions()` para determinar las antenas de transmisión válidas. Los elementos del menú muestran una etiqueta legible junto al identificador interno de la antena.

**Botón de grosor del marcador** — Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se persiste por slice.

**Botón de bordes de filtro** — Activa o desactiva las líneas del borde del filtro en la banda pasante del espectro. Se persiste por slice.

**Alternancia de colapso** — Colapsa el panel VFO a una tira compacta de solo frecuencia. Se persiste por slice.

**Distintivo TX** — Se muestra cuando este slice es el slice de transmisión activo. Muestra un indicador TX rojo.

**Distintivo SPLIT** — Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo. Muestra un indicador SPLIT ámbar.

**Botones + etiquetas RIT / XIT** — Activan la sintonización incremental del receptor (RIT) o del transmisor (XIT) para este slice. Cuando están activos, la etiqueta junto a cada botón muestra el valor del offset actual. Gire la rueda del mouse sobre el botón para ajustar el offset en pasos de 10 Hz. Ninguno de los ajustes se persiste; el estado refleja el estado en vivo de la radio.

**Botón + deslizador de squelch (pestaña Audio)** — Activa el squelch para este slice. El deslizador adyacente establece el umbral. El squelch se desactiva automáticamente cuando el modo del slice es CW, digital o RTTY, porque en esos modos el audio alimenta decodificadores externos a través de DAX donde el squelch bloquearía señales FSK débiles (#2504). El botón y el deslizador se atenúan en esos modos.

**Deslizador de nivel DSP (pestaña DSP)** — Establece la profundidad de procesamiento para la función DSP compatible activada más recientemente en este slice. La etiqueta a la izquierda identifica el objetivo actual. La fila se atenúa cuando ninguna función DSP elegible está activa. No se persiste; refleja el estado en vivo de la radio.

## Consejos

- Los offsets de RIT y XIT son independientes. Puede activar ambos al mismo tiempo para desplazar recepción y transmisión de forma independiente.
- El ajuste con la rueda del mouse es de 10 Hz por paso. Para offsets mayores, gire la rueda varias muescas.
- Cuando un slice está bloqueado, la sintonización con la rueda del mouse en el panel VFO está bloqueada. Aparece una notificación indicando que la sintonización está bloqueada por el bloqueo. La entrada directa de frecuencia también se cancela si estaba en progreso cuando se aplica el bloqueo.

## Cambios en v26.5.3

### Comportamiento de sintonización en slice bloqueado

Cuando un slice está bloqueado, las siguientes interacciones de sintonización en el panel VFO ahora están bloqueadas:

- **Sintonización con rueda del mouse**: Girar la rueda del mouse sobre el panel VFO colapsado o expandido ya no cambia la frecuencia. Se muestra una notificación `tuneBlockedByLock`.
- **Entrada directa de frecuencia**: Si está escribiendo una frecuencia y el slice se bloquea, la entrada directa se cancela y la visualización vuelve a la frecuencia bloqueada.

La superposición de bloqueo (icono de candado) es gestionada centralmente por `SliceModel` y se limpia automáticamente cuando el slice se desbloquea (#2983).

### Mejoras en la entrada directa de banda XVTR

Al ingresar una frecuencia directamente en el panel VFO, el analizador ahora maneja correctamente las entradas explícitas en MHz por encima de 54 MHz incluso cuando no está en una banda XVTR. Si escribe un valor en formato MHz (por ejemplo, `144.200`), se acepta hasta 50 000 MHz sin ser malinterpretado como kHz o Hz. La inserción de conveniencia de banda de 3 dígitos para enteros simples en bandas de 2m/70cm solo se aplica cuando la frecuencia del slice está entre 100 MHz y 999 MHz.

### Optimización de altura de pestañas

La pila de pestañas del panel VFO ahora usa un widget `TabStack` personalizado que informa solo el tamaño preferido de la página actual. Anteriormente, cuando la pestaña DSP era más alta que la pestaña Mode (por ejemplo, cuando el contenedor de filtro digital era visible en modo DIGU/DIGL), el panel VFO asignaba una altura excesiva, causando un espacio vacío dentro de la pestaña Mode. Esto ahora está resuelto.

## Cambios en v26.5.2.1

### Manejo de frecuencia en banda XVTR

Cuando el slice está en una banda XVTR, la frecuencia máxima aceptada durante la entrada directa se ha incrementado de 450 MHz a 50 000 MHz para soportar bandas de microondas. El comportamiento de inserción de banda de 3 dígitos (insertar automáticamente un decimal después del tercer dígito para enteros simples en 2m/70cm) ahora solo se activa cuando la frecuencia del slice está entre 100 MHz y 999 MHz. Para bandas como 23cm (1296 MHz), los enteros simples se interpretan directamente como la frecuencia en MHz.

### Mejoras en el menú de antena

Tanto los botones de antena RX como TX ahora muestran una etiqueta legible en el menú junto al identificador interno de la antena. El menú usa `data()` internamente para la selección, coincidiendo con la cadena completa de la antena en lugar de la etiqueta mostrada. Los elementos del menú también incluyen texto de tooltip y status tip que muestra el identificador de antena sin procesar.

### Soporte de texto enriquecido para distintivos de slice

El distintivo de slice ahora soporta el formato de texto enriquecido (`Qt::RichText`), permitiendo formato HTML en ciertos casos (#2606).

## Cambios en v26.5.1

### Squelch deshabilitado en modo RTTY

El botón y el deslizador de squelch ahora se deshabilitan automáticamente cuando el slice está en modo RTTY, además de las restricciones existentes en modo digital y CW. Cuando el modo es RTTY, el botón de squelch se atenúa y no se puede alternar, y el deslizador de squelch se atenúa y no se puede ajustar. Si el squelch estaba previamente habilitado, se desactiva automáticamente al cambiar al modo RTTY. Esto evita que el squelch bloquee señales FSK débiles que los decodificadores RTTY externos necesitan recibir a través de DAX (#2504).

## Cambios en v0.9.8

### Pestaña DSP — nuevos botones ADSP y AetherVoice

La **pestaña DSP** en el panel VFO ahora incluye dos nuevos botones de lanzamiento de DSP del lado cliente:

- **ADSP** — Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Este es un botón pulsador de una sola celda estilizado como los botones de alternancia DSP del lado de la radio pero sin posibilidad de marcar. Al hacer clic, abre y enfoca el diálogo no modal AetherDSP Settings.
- **AetherVoice** — Activa la tira de canal de audio Aetherial, el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas.

Ambos botones están colocados en la misma fila de la cuadrícula, con **ADSP** ocupando la columna más a la izquierda y **AetherVoice** ocupando las columnas 2-3.

**Corrección de la etiqueta de ancho de filtro**

La etiqueta de ancho de filtro ahora usa `RxApplet::formatFilterWidth` como la única fuente de verdad para el formato. Esto corrige un offset de 0.1 kHz que anteriormente afectaba las lecturas de filtro en modo SSB y digital (#2197).

**Mejora del deslizador de nivel DSP**

Los cambios de estado DSP desde el perfil de la radio ahora insertan correctamente el objetivo de nivel DSP asociado en la pila del deslizador. Esto asegura que el deslizador aparezca al inicio para cualquier función DSP que estuviera habilitada en el perfil guardado de la radio, sin requerir que el usuario la active manualmente primero.

## Cambios en v0.9.7

### Pestaña DSP — solo botones del lado de la radio

La **pestaña DSP** en el panel VFO ahora muestra solo botones para funciones DSP que la propia radio proporciona. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (eliminación de ruido neuronal GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener para macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos módulos DSP del lado cliente ahora son accesibles desde el menú de superposición del espectro y desde el applet AetherDSP. Use esas ubicaciones para activarlos o ajustarlos.

Los botones que permanecen en la pestaña DSP son: **NR**, **NB**, **ANF**, **APF**, **NRL**, **NRS**, **RNN**, **NRF**, **ANFL** y **ANFT**. La disposición de la cuadrícula es de cuatro columnas en tres filas. El botón **APF** es visible solo cuando el slice está en modo CW.

### Pestaña DSP — deslizador de nivel DSP

Se ha añadido una fila de deslizador de nivel compartida en la parte inferior de la pestaña DSP. El deslizador ajusta la profundidad de procesamiento de la función DSP compatible que se haya activado más recientemente. La
