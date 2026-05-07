# Habilitar el desplazamiento RIT o XIT desde el panel VFO

RIT (Sintonización incremental del receptor) y XIT (Sintonización incremental del transmisor) permiten desplazar la frecuencia de recepción o transmisión en un pequeño incremento sin mover el VFO principal. Esto es útil para trabajar contactos en frecuencia dividida o para compensar una estación que está ligeramente fuera de la frecuencia de su dial.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO para el segmento (slice) objetivo debe estar abierto y expandido. Si está colapsado en la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento que desea ajustar. El panel VFO aparece anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el desplazamiento del receptor, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el desplazamiento RIT actual.
4. Para habilitar el desplazamiento del transmisor, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el desplazamiento XIT actual.
5. Con RIT o XIT activo, coloque el puntero del ratón sobre el botón correspondiente y gire la rueda del ratón para ajustar el desplazamiento. Cada paso de la rueda cambia el desplazamiento en 10 Hz.
6. Para deshabilitar RIT o XIT, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control                      | Tipo                                                                                                                                   | Valor predeterminado                                                                                                      |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX           | Botón pulsador                                                                                                                         | Abre el menú de selección de antena para la antena receptora de este segmento.                                            |
| Botón de antena TX           | Botón pulsador                                                                                                                         | Abre el menú de selección de antena para la antena transmisora de este segmento.                                          |
| Indicador de frecuencia      | Indicador                                                                                                                              | Muestra la frecuencia actual del segmento. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro   | Indicador                                                                                                                              | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos del filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de información, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas de modo SSB/digital (#2197, v0.9.8). |
| Deslizador de ganancia AF (pestaña Audio) | Deslizador                                                                                                                   | 100                                                                                                                       |
| Deslizador Pan (pestaña Audio) | Deslizador                                                                                                                          | 50                                                                                                                        |
| Botón Silenciar (pestaña Audio) | Botón de alternancia                                                                                                                | apagado                                                                                                                   |
| Botón + deslizador Squelch (pestaña Audio) | Botón de alternancia                                                                                                         | apagado                                                                                                                   |
| Combinación AGC (pestaña Audio) | Cuadro combinado                                                                                                                     | FAST                                                                                                                      |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia                                                                                            | apagado                                                                                                                   |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú de configuración (v0.9.8). | Tiene el estilo de un interruptor DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna la tira de canal de audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                                        | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combinación Mode (pestaña Mode) | Cuadro combinado                                                                                                                     | USB                                                                                                                       |
| Botones de filtro preestablecidos (pestaña Mode) | Botón pulsador                                                                                                                   | Persistido en FilterPresets                                                                                               |
| Botones + etiquetas RIT / XIT | Botón de alternancia                                                                                                                 | apagado                                                                                                                   |
| Combinación de canal DAX (pestaña DAX) | Cuadro combinado                                                                                                                  | Apagado                                                                                                                   |
| Botón de grosor de marcador | Botón pulsador                                                                                                                           | 1 px                                                                                                                      |
| Botón de bordes de filtro    | Botón de alternancia                                                                                                                    | mostrado                                                                                                                  |
| Alternancia de colapso       | Botón de alternancia                                                                                                                    | expandido                                                                                                                 |

**Botones + etiquetas RIT / XIT** — Habilita la sintonización incremental del receptor (RIT) o del transmisor (XIT) para este segmento. Cuando está activo, la etiqueta junto a cada botón muestra el valor de desplazamiento actual. Gire la rueda del ratón sobre el botón para ajustar el desplazamiento en pasos de 10 Hz. Ninguna configuración se persiste; el estado refleja el estado actual de la radio.

## Consejos

- Los desplazamientos RIT y XIT son independientes. Puede habilitar ambos al mismo tiempo para desplazar la recepción y la transmisión de forma independiente.
- El ajuste con la rueda del ratón es de 10 Hz por paso. Para desplazamientos mayores, gire varios pasos.

## Cambios en v0.9.8

### Pestaña DSP — nuevos botones ADSP y AetherVoice

La **pestaña DSP** en el panel VFO ahora incluye dos nuevos botones de lanzamiento de DSP del lado del cliente:

- **ADSP** — Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Este es un botón pulsador de una sola celda con el estilo de los interruptores de DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP.
- **AetherVoice** — Alterna la tira de canal de audio Aetherial, el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas.

Ambos botones están colocados en la misma fila de la cuadrícula, con **ADSP** ocupando la columna más a la izquierda y **AetherVoice** ocupando las columnas 2-3.

**Corrección de la etiqueta de ancho de filtro**

La etiqueta de ancho de filtro ahora utiliza `RxApplet::formatFilterWidth` como fuente única de información para el formateo. Esto corrige un desplazamiento de 0.1 kHz que afectaba anteriormente las lecturas del filtro en modo SSB y digital (#2197).

**Mejora del deslizador de nivel DSP**

Los cambios de estado DSP desde el perfil de la radio ahora empujan correctamente el objetivo de nivel DSP asociado a la pila del deslizador. Esto asegura que el deslizador aparezca al iniciar para cualquier función DSP que estuviera habilitada en el perfil guardado de la radio, sin requerir que el usuario lo alterne manualmente primero.

## Cambios en v0.9.7

### Pestaña DSP — solo botones del lado de la radio

La **pestaña DSP** en el panel VFO ahora muestra solo botones para las funciones DSP que la propia radio proporciona. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (eliminación de ruido neuronal GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener de macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos módulos DSP del lado del cliente ahora son accesibles desde el menú superpuesto del espectro y desde el applet AetherDSP. Utilice esas ubicaciones para habilitarlos o ajustarlos.

Los botones que permanecen en la pestaña DSP son: **NR**, **NB**, **ANF**, **APF**, **NRL**, **NRS**, **RNN**, **NRF**, **ANFL** y **ANFT**. La disposición de la cuadrícula es de cuatro columnas en tres filas. El botón **APF** solo es visible cuando el segmento está en modo CW.

### Pestaña DSP — deslizador de nivel DSP

Se ha agregado una fila de deslizador de nivel compartida en la parte inferior de la pestaña DSP. El deslizador ajusta la profundidad de procesamiento de la función DSP compatible que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El deslizador se dirige a las siguientes funciones: NR, NB, ANF, NRL, NRS, NRF y ANFL. No se dirige a RNN, ANFT ni APF. Cuando ninguna de esas funciones está activa, la fila del deslizador aún está presente en el diseño, pero su contenido aparece visualmente atenuado para indicar que no hay ningún objetivo seleccionado. Hacer clic o arrastrar el deslizador cuando está atenuado no tiene efecto.

| Control | Tipo | Valor predeterminado | Rango válido | Configuración persistida |
|---|---|---|---|---|
| Deslizador de nivel DSP (pestaña DSP) | Deslizador | — | 0–100 | — |

**Deslizador de nivel DSP** — Establece la profundidad de procesamiento para la función DSP compatible activada más recientemente en este segmento. La etiqueta a la izquierda identifica el objetivo actual. La fila se atenúa cuando no hay ninguna función DSP elegible activa. No se persiste; refleja el estado actual de la radio.

## Relacionado

- [Descripción general del panel VFO](overview.md)
- [Cambiar el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Sintonizar la radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
