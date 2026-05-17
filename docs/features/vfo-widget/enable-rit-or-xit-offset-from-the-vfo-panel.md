# Habilitar el desplazamiento RIT o XIT desde el panel VFO

RIT (Sintonización Incremental del Receptor) y XIT (Sintonización Incremental del Transmisor) permiten desplazar la frecuencia de recepción o transmisión mediante un pequeño desfase sin mover el VFO principal. Esto es útil para trabajar contactos en división de frecuencia o para compensar una estación que está ligeramente fuera de su frecuencia de marcación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO para el segmento (slice) de destino debe estar abierto y expandido. Si está colapsado a la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento que desea ajustar. El panel VFO aparece anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el desfase del receptor, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el desfase RIT actual.
4. Para habilitar el desfase del transmisor, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el desfase XIT actual.
5. Con RIT o XIT activos, coloque el puntero del ratón sobre el botón correspondiente y gire la rueda del ratón para ajustar el desfase. Cada paso de la rueda cambia el desfase en 10 Hz.
6. Para deshabilitar RIT o XIT, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control                          | Tipo                                                                                                                                   | Predeterminado                                                                                                           |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX               | Botón pulsador                                                                                                                         | Abre el menú de selección de antena para la antena receptora de este segmento.                                           |
| Botón de antena TX               | Botón pulsador                                                                                                                         | Abre el menú de selección de antena para la antena transmisora de este segmento.                                         |
| Visualización de frecuencia      | Indicador                                                                                                                              | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro      | Indicador                                                                                                                              | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Deslizador de ganancia AF (pestaña Audio) | Deslizador                                                                                                                  | 100                                                                                                                     |
| Deslizador Pan (pestaña Audio)   | Deslizador                                                                                                                             | 50                                                                                                                      |
| Botón Silenciar (pestaña Audio)  | Botón de conmutación                                                                                                                   | apagado                                                                                                                 |
| Botón + deslizador de Squelch (pestaña Audio) | Botón de conmutación                                                                                                          | apagado                                                                                                                 |
| Combinación AGC (pestaña Audio)  | Cuadro combinado                                                                                                                       | FAST                                                                                                                    |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de conmutación                                                                                         | apagado                                                                                                                 |
| Botón ADSP (pestaña DSP)        | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de conmutación DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Conmuta la Tira de Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                                                     | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combinación Mode (pestaña Mode)  | Cuadro combinado                                                                                                                       | USB                                                                                                                     |
| Botones preestablecidos de filtro (pestaña Mode) | Botón pulsador                                                                                                                       | Conservado en FilterPresets                                                                                              |
| Botones + etiquetas RIT / XIT   | Botón de conmutación                                                                                                                   | apagado                                                                                                                 |
| Combinación de canal DAX (pestaña DAX) | Cuadro combinado                                                                                                                | Apagado                                                                                                                 |
| Botón de grosor del marcador     | Botón pulsador                                                                                                                         | 1 px                                                                                                                    |
| Botón de bordes del filtro      | Botón de conmutación                                                                                                                   | mostrado                                                                                                                |
| Conmutador de colapso            | Botón de conmutación                                                                                                                   | expandido                                                                                                               |
| Insignia TX                      | Indicador                                                                                                                              | Muestra TX (rojo) cuando este segmento es el segmento transmisor activo. Oculto en caso contrario.                       |
| Insignia SPLIT                   | Indicador                                                                                                                              | Muestra SPLIT (ámbar) cuando TX está asignado a un segmento diferente al segmento receptor activo. Oculto en caso contrario. |

**Botón de antena RX** — Abre un menú de selección de antena para la antena receptora de este segmento. El menú ahora utiliza la propiedad `rxAntennaList()` por segmento cuando está disponible, recurriendo a la lista global de antenas. Los elementos del menú muestran una etiqueta legible junto al identificador interno de la antena.

**Botón de antena TX** — Abre un menú de selección de antena para la antena transmisora de este segmento. El menú filtra los puertos de antena solo de recepción. Utiliza la función auxiliar `txAntennaOptions()` para determinar las antenas transmisoras válidas. Los elementos del menú muestran una etiqueta legible junto al identificador interno de la antena.

**Botón de grosor del marcador** — Recorre la línea del marcador VFO entre Apagado, 1 px y 3 px. Se conserva por segmento.

**Botón de bordes del filtro** — Conmuta las líneas de borde del filtro en la banda de paso del espectro. Se conserva por segmento.

**Conmutador de colapso** — Colapsa el panel VFO a una tira compacta de solo frecuencia. Se conserva por segmento.

**Insignia TX** — Se muestra cuando este segmento es el segmento transmisor activo. Muestra un indicador TX rojo.

**Insignia SPLIT** — Se muestra cuando TX está asignado a un segmento diferente al segmento receptor activo. Muestra un indicador SPLIT ámbar.

**Botones + etiquetas RIT / XIT** — Habilitan la sintonización incremental del receptor (RIT) o del transmisor (XIT) para este segmento. Cuando está activo, la etiqueta junto a cada botón muestra el valor de desfase actual. Gire la rueda del ratón sobre el botón para ajustar el desfase en pasos de 10 Hz. Ninguna configuración se conserva; el estado refleja el estado en vivo de la radio.

**Botón + deslizador de Squelch (pestaña Audio)** — Habilita el silenciador (squelch) para este segmento. El deslizador adyacente establece el umbral. El silenciador se deshabilita automáticamente cuando el modo del segmento es CW, digital o RTTY, porque en esos modos el audio alimenta decodificadores externos a través de DAX donde el silenciador bloquearía señales FSK débiles (#2504). El botón y el deslizador se atenúan en esos modos.

## Consejos

- Los desfases RIT y XIT son independientes. Puede habilitar ambos al mismo tiempo para desfasar la recepción y la transmisión de forma independiente.
- El ajuste con la rueda del ratón es de 10 Hz por paso. Para desfases mayores, gire la rueda varios pasos.

## Cambios en v26.5.2.1

### Manejo de frecuencia en banda XVTR

Cuando el segmento está en una banda XVTR, la frecuencia máxima aceptada durante la entrada directa se ha incrementado de 450 MHz a 50 000 MHz para admitir bandas de microondas. El comportamiento de inserción de dígitos de 3 bandas (insertar automáticamente un decimal después del tercer dígito para números enteros en 2m/70cm) ahora solo se activa cuando la frecuencia del segmento está entre 100 MHz y 999 MHz. Para bandas como 23cm (1296 MHz), los números enteros se interpretan directamente como la frecuencia en MHz.

### Mejoras en el menú de antena

Tanto los botones de antena RX como TX ahora muestran una etiqueta legible en el menú junto al identificador interno de la antena. El menú usa `data()` internamente para la selección, coincidiendo con la cadena completa de la antena en lugar de la etiqueta mostrada. Los elementos del menú también incluyen texto de información sobre herramientas y de estado que muestra el identificador de antena sin procesar.

### Soporte de texto enriquecido en la insignia del segmento

La insignia del segmento ahora admite formato de texto enriquecido (`Qt::RichText`), lo que permite el formato HTML en ciertos casos (#2606).

## Cambios en v26.5.1

### Silenciador deshabilitado en modo RTTY

El botón y el deslizador de silenciador ahora se deshabilitan automáticamente cuando el segmento está en un modo RTTY, además de las restricciones existentes para los modos digital y CW. Cuando el modo es RTTY, el botón de silenciador se atenúa y no se puede conmutar, y el deslizador de silenciador se atenúa y no se puede ajustar. Si el silenciador estaba previamente habilitado, se apaga automáticamente al cambiar al modo RTTY. Esto evita que el silenciador bloquee las señales FSK débiles que los decodificadores RTTY externos necesitan recibir a través de DAX (#2504).

## Cambios en v0.9.8

### Pestaña DSP — nuevos botones ADSP y AetherVoice

La **pestaña DSP** en el panel VFO ahora incluye dos nuevos botones de inicio de DSP del lado del cliente:

- **ADSP** — Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Es un botón pulsador de una sola celda con el estilo de los conmutadores DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP.
- **AetherVoice** — Conmuta la Tira de Canal de Audio Aetherial, el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas.

Ambos botones se colocan en la misma fila de la cuadrícula, con **ADSP** ocupando la columna más a la izquierda y **AetherVoice** ocupando las columnas 2-3.

**Corrección de la etiqueta de ancho de filtro**

La etiqueta de ancho de filtro ahora utiliza `RxApplet::formatFilterWidth` como la única fuente de verdad para el formateo. Esto corrige un desfase de 0.1 kHz que afectaba anteriormente las lecturas de filtro en modo SSB y digital (#2197).

**Mejora del deslizador de nivel DSP**

Los cambios de estado DSP provenientes del perfil de la radio ahora empujan correctamente el objetivo de nivel DSP asociado a la pila del deslizador. Esto asegura que el deslizador aparezca al inicio para cualquier función DSP que estuviera habilitada en el perfil guardado de la radio, sin requerir que el usuario la conmute manualmente primero.

## Cambios en v0.9.7

### Pestaña DSP — solo botones del lado de la radio

La **pestaña DSP** en el panel VFO ahora muestra solo botones para las funciones DSP que la propia radio proporciona. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (eliminación de ruido neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener para macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos módulos DSP del lado del cliente ahora son accesibles desde el menú de superposición del espectro y el applet AetherDSP. Use esas ubicaciones para habilitarlos o ajustarlos.

Los botones que permanecen en la pestaña DSP son: **NR**, **NB**, **ANF**, **APF**, **NRL**, **NRS**, **RNN**, **NRF**, **ANFL** y **ANFT**. El diseño de la cuadrícula es de cuatro columnas en tres filas. El botón **APF** solo es visible cuando el segmento está en modo CW.

### Pestaña DSP — deslizador de nivel DSP

Se ha añadido una fila de deslizador de nivel compartido en la parte inferior de la pestaña DSP. El deslizador ajusta la profundidad de procesamiento de la función DSP compatible que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El deslizador se dirige a las siguientes funciones: NR, NB, ANF, NRL, NRS, NRF y ANFL. No se dirige a RNN, ANFT ni APF. Cuando ninguna de esas funciones está activa, la fila del deslizador aún está presente en el diseño pero su contenido aparece visualmente atenuado para indicar que no hay ningún objetivo seleccionado. Hacer clic o arrastrar el deslizador mientras está atenuado no tiene efecto.

| Control | Tipo | Predeterminado | Rango válido | Configuración conservada |
|---|---|---|---|---|
| Deslizador de nivel DSP (pestaña DSP) | Deslizador | — | 0–100 | — |

**Deslizador de nivel DSP** — Establece la profundidad de procesamiento para la función DSP compatible activada más recientemente en este segmento. La etiqueta a la izquierda identifica el objetivo actual. La fila se atenúa cuando ninguna función DSP elegible está activa. No se conserva; refleja el estado en vivo de la radio.

## Relacionados

- [Resumen del panel VFO](overview.md)
- [Cambiar el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Sintonizar la radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
