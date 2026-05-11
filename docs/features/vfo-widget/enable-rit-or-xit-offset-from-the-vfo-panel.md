# Habilitar el desplazamiento RIT o XIT desde el panel VFO

RIT (Receiver Incremental Tuning) y XIT (Transmitter Incremental Tuning) permiten desplazar la frecuencia de recepción o transmisión en un pequeño margen sin mover el VFO principal. Esto es útil para realizar contactos en frecuencias divididas o para compensar una estación que está ligeramente fuera de la frecuencia de sintonía.

## Antes de empezar

- AetherSDR debe estar conectado al equipo de radio. El panel VFO requiere una conexión activa con el equipo.
- El panel VFO del segmento (slice) de destino debe estar abierto y expandido. Si está colapsado a la tira que solo muestra la frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en el marcador del VFO en la pantalla de espectro del segmento que desea ajustar. El panel VFO aparecerá anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el desplazamiento del receptor, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el desplazamiento RIT actual.
4. Para habilitar el desplazamiento del transmisor, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el desplazamiento XIT actual.
5. Con RIT o XIT activos, coloque el puntero del ratón sobre el botón correspondiente y gire la rueda del ratón para ajustar el desplazamiento. Cada paso de la rueda cambia el desplazamiento en 10 Hz.
6. Para desactivar RIT o XIT, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control                              | Tipo                                                                                                                                | Valor por defecto                                                                                                          |
|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX                   | Botón pulsador                                                                                                                      | Abre el menú de selección de antena para la antena de recepción de este segmento.                                          |
| Botón de antena TX                   | Botón pulsador                                                                                                                      | Abre el menú de selección de antena para la antena de transmisión de este segmento.                                        |
| Visualización de frecuencia          | Indicador                                                                                                                           | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar a introducir la frecuencia directamente; escriba MHz y pulse Enter o Tab. |
| Etiqueta de ancho de filtro          | Indicador                                                                                                                           | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajustes de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Deslizador de ganancia AF (pestaña Audio) | Deslizador                                                                                                                          | 100                                                                                                                        |
| Deslizador Pan (pestaña Audio)       | Deslizador                                                                                                                          | 50                                                                                                                         |
| Botón de silencio (pestaña Audio)    | Botón de conmutación                                                                                                                | apagado                                                                                                                    |
| Botón + deslizador de Squelch (pestaña Audio) | Botón de conmutación                                                                                                               | apagado                                                                                                                    |
| Combo AGC (pestaña Audio)            | Cuadro combinado                                                                                                                    | FAST                                                                                                                       |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de conmutación                                                                                             | apagado                                                                                                                    |
| Botón ADSP (pestaña DSP)             | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo similar a los conmutadores de DSP del lado del equipo pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP)      | Conmuta la tira de canal de audio Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8).                                         | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combo Mode (pestaña Mode)            | Cuadro combinado                                                                                                                    | USB                                                                                                                        |
| Botones de preajuste de filtro (pestaña Mode) | Botón pulsador                                                                                                                    | Conservado en FilterPresets                                                                                                |
| Botones + etiquetas RIT / XIT        | Botón de conmutación                                                                                                                | apagado                                                                                                                    |
| Combo de canal DAX (pestaña DAX)     | Cuadro combinado                                                                                                                    | Off                                                                                                                        |
| Botón de grosor de marcador          | Botón pulsador                                                                                                                      | 1 px                                                                                                                       |
| Botón de bordes de filtro            | Botón de conmutación                                                                                                                | mostrado                                                                                                                   |
| Conmutador de colapso                | Botón de conmutación                                                                                                                | expandido                                                                                                                  |

**Botones + etiquetas RIT / XIT** — Habilita la sintonía incremental del receptor (RIT) o transmisor (XIT) para este segmento. Cuando está activo, la etiqueta junto a cada botón muestra el valor de desplazamiento actual. Gire la rueda del ratón sobre el botón para ajustar el desplazamiento en pasos de 10 Hz. Ninguno de los ajustes se conserva; el estado refleja el estado en vivo del equipo.

**Botón + deslizador de Squelch (pestaña Audio)** — Habilita el squelch para este segmento. El deslizador adyacente establece el umbral. El squelch se desactiva automáticamente cuando el modo del segmento es CW, digital o RTTY, porque en esos modos el audio se envía a decodificadores externos a través de DAX, donde el squelch bloquearía las señales FSK débiles (#2504). El botón y el deslizador se atenúan en esos modos.

## Consejos

- Los desplazamientos de RIT y XIT son independientes. Puede habilitar ambos al mismo tiempo para desplazar la recepción y la transmisión de forma independiente.
- El ajuste con la rueda del ratón es de 10 Hz por paso. Para desplazamientos mayores, gire la rueda varias muescas.

## Cambios en la versión v26.5.1

### Squelch deshabilitado en modo RTTY

El botón y el deslizador de squelch ahora se desactivan automáticamente cuando el segmento está en un modo RTTY, además de las restricciones existentes para los modos digital y CW. Cuando el modo es RTTY, el botón de squelch se atenúa y no se puede conmutar, y el deslizador de squelch se atenúa y no se puede ajustar. Si el squelch estaba habilitado previamente, se desactiva automáticamente al cambiar al modo RTTY. Esto evita que el squelch bloquee las señales FSK débiles que los decodificadores RTTY externos necesitan recibir a través de DAX (#2504).

## Cambios en la versión v0.9.8

### Pestaña DSP: nuevos botones ADSP y AetherVoice

La **pestaña DSP** del panel VFO ahora incluye dos nuevos botones de inicio de DSP del lado del cliente:

- **ADSP** — Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Es un botón pulsador de una celda con el estilo de los conmutadores de DSP del lado del equipo, pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP.
- **AetherVoice** — Conmuta la tira de canal de audio Aetherial, el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas.

Ambos botones se colocan en la misma fila de la cuadrícula, ocupando **ADSP** la columna más a la izquierda y **AetherVoice** las columnas 2-3.

**Corrección de la etiqueta de ancho de filtro**

La etiqueta de ancho de filtro ahora usa `RxApplet::formatFilterWidth` como única fuente de verdad para el formato. Esto corrige un desplazamiento de 0.1 kHz que anteriormente afectaba las lecturas del filtro en modo SSB y digital (#2197).

**Mejora del deslizador de nivel DSP**

Los cambios de estado de DSP provenientes del perfil del equipo ahora colocan correctamente el objetivo de nivel DSP asociado en la pila del deslizador. Esto asegura que el deslizador aparezca al inicio para cualquier función DSP que estuviera habilitada en el perfil guardado del equipo, sin necesidad de que el usuario la conmute manualmente primero.

## Cambios en la versión v0.9.7

### Pestaña DSP: solo botones del lado del equipo

La **pestaña DSP** del panel VFO ahora muestra solo los botones para las funciones DSP que el propio equipo proporciona. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (eliminación de ruido neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener para macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos módulos DSP del lado del cliente ahora son accesibles desde el menú superpuesto del espectro y el applet AetherDSP. Utilice esas ubicaciones para habilitarlos o ajustarlos.

Los botones que permanecen en la pestaña DSP son: **NR**, **NB**, **ANF**, **APF**, **NRL**, **NRS**, **RNN**, **NRF**, **ANFL** y **ANFT**. La distribución de la cuadrícula es de cuatro columnas en tres filas. El botón **APF** solo es visible cuando el segmento está en modo CW.

### Pestaña DSP: deslizador de nivel DSP

Se ha agregado una fila compartida de deslizador de nivel en la parte inferior de la pestaña DSP. El deslizador ajusta la profundidad de procesamiento de la función DSP compatible que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El deslizador apunta a las siguientes funciones: NR, NB, ANF, NRL, NRS, NRF y ANFL. No apunta a RNN, ANFT o APF. Cuando ninguna de esas funciones está activa, la fila del deslizador sigue presente en la distribución, pero su contenido aparece visualmente atenuado para indicar que no hay ningún objetivo seleccionado. Hacer clic o arrastrar el deslizador mientras está atenuado no tiene efecto.

| Control | Tipo | Valor por defecto | Rango válido | Ajuste conservado |
|---|---|---|---|---|
| Deslizador de nivel DSP (pestaña DSP) | Deslizador | — | 0–100 | — |

**Deslizador de nivel DSP** — Establece la profundidad de procesamiento para la función DSP compatible activada más recientemente en este segmento. La etiqueta de la izquierda identifica el objetivo actual. La fila se atenúa cuando no hay ninguna función DSP elegible activa. No se conserva; refleja el estado en vivo del equipo.

## Relacionados

- [VFO Panel overview](overview.md)
- [Change mode from the VFO panel](change-mode-from-the-vfo-panel.md)
- [Tune the radio by typing a frequency into the VFO panel](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
