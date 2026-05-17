# Sintonice la radio escribiendo una frecuencia en el panel VFO

La introducción directa de frecuencia le permite saltar a una frecuencia exacta sin tener que hacer clic en el panadapter. Escriba un valor en MHz en la visualización de frecuencia del panel VFO y presione Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El panel VFO para el slice objetivo debe estar abierto. Si no está visible, haga clic en la bandera marcadora VFO de ese slice en la pantalla del espectro.

## Pasos

1. Haga clic una vez en la **Visualización de frecuencia**. La pantalla entra en modo de introducción directa.
2. Escriba la frecuencia deseada en MHz.
3. Presione **Enter** o **Tab** para aplicar. El slice se resintoniza inmediatamente.

## Función de cada control

| Control                      | Comportamiento                                                                                                                                                                                                 |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Botón de antena RX**       | Abre el menú de selección de antena para la antena receptora de este slice. Los elementos del menú usan la lista de antenas RX dedicada del slice cuando está disponible, recurriendo a la lista global de antenas. Se puede hacer clic derecho. |
| **Botón de antena TX**       | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de antena solo RX. Los elementos del menú usan las opciones de antena TX dedicadas del slice cuando están disponibles. Se puede hacer clic derecho. |
| **Visualización de frecuencia** | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la introducción directa; escriba MHz y presione Enter o Tab para aplicar. Desplace la rueda del ratón sobre la pantalla para sintonizar hacia arriba o hacia abajo según el tamaño de paso actual. |
| **Insignia del slice**       | Muestra la letra del slice (ej., A, B, C) en una insignia de color. Admite formato de texto enriquecido para renderizado HTML (#2606). El clic derecho abre el selector de color del slice.                                          |
| **Etiqueta de ancho de filtro** | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones predefinidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| **Deslizador de ganancia AF (pestaña Audio)** | Establece el nivel de salida de audio para este slice. Valor predeterminado: 100. Rango: 0-100. No se conserva: refleja el estado en vivo de la radio.                                                                                      |
| **Deslizador de paneo (pestaña Audio)** | Establece el paneo estéreo izquierda/derecha para este slice. Valor predeterminado: 50. Rango: 0-100. 50 = centro.                                                                                                                       |
| **Botón de silencio (pestaña Audio)** | Botón de alternancia. Silencia la salida de audio de este slice sin cambiar la configuración de ganancia AF. Valor predeterminado: desactivado.                                                                                                     |
| **Botón + deslizador de squelch (pestaña Audio)** | Botón de alternancia. Activa el squelch para este slice. El deslizador adyacente establece el umbral. Valor predeterminado: desactivado. Rango: 0-100.                                                                             |
| **Combo AGC (pestaña Audio)** | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF. Valor predeterminado: FAST.                                                                                                          |
| **Combo de modo (pestaña Mode)** | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. Valor predeterminado: USB.                                                                            |
| **Botones de preajuste de filtro (pestaña Mode)** | Aplica un preajuste guardado de ancho de filtro. El clic derecho guarda el ancho de filtro actual en esa ranura. Se pueden establecer bordes personalizados lo/hi por ranura mediante clic derecho. Se conserva en `FilterPresets`.         |
| **Botones + etiquetas RIT / XIT (pestaña X/RIT)** | Botones de alternancia. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. Valor predeterminado: desactivado.                         |
| **Combo de canal DAX (pestaña DAX)** | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8. Valor predeterminado: Off.                                                                                                                            |
| **Botón de grosor del marcador** | Recorre la línea marcadora VFO entre Off, 1 px y 3 px. Se conserva por slice en `Slice{N}_MarkerWidth`.                                                                                                  |
| **Botón de bordes del filtro** | Botón de alternancia. Alterna las líneas de borde del filtro en la banda de paso del espectro. Se conserva por slice en `Slice{N}_FilterEdgesHidden`. Valor predeterminado: mostrado.                                                               |
| **Alternancia de colapso**    | Colapsa el panel VFO a una banda compacta de solo frecuencia. En modo colapsado, desplazarse en cualquier lugar de la banda sintoniza según el tamaño de paso actual. Se conserva por slice en `SliceFlagCollapsed_{N}`.           |

## Controles de la pestaña DSP

La pestaña DSP contiene botones de alternancia para algoritmos de reducción de ruido y filtrado proporcionados por la radio, además de botones de lanzamiento del lado del cliente. Los siguientes botones están disponibles en la cuadrícula DSP del panel VFO:

| Botón | Descripción |
|---|---|
| **NR** | Reducción de ruido. |
| **NB** | Eliminador de ruido. |
| **ANF** | Filtro automático de muesca. |
| **APF** | Filtro de pico de audio. Visible solo cuando el slice está en modo CW. |
| **NR2 / NR4 / RN2 / BNR / MNR / DFNR / NRL / NRS / RNN / NRF** | Varios algoritmos de reducción de ruido. La disponibilidad de botones depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de configuración de AetherDSP para ese algoritmo. |
| **ADSP** | Botón pulsador. Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Diseñado como un DSP del lado de la radio, pero no se puede marcar. |
| **AetherVoice** | Botón pulsador. Alterna la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

Todos los botones DSP del lado de la radio están desactivados de forma predeterminada.

### Deslizador de nivel DSP

Cuando uno o más algoritmos DSP del lado de la radio que admiten control de nivel están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra el nombre del algoritmo habilitado más recientemente que admita nivelación (por ejemplo, **NR**, **NB**, **ANF**, **NRL**, **NRS**, **NRF** o **ANFL**). La lectura numérica adyacente muestra el valor actual.

- Arrastre el deslizador para establecer el nivel del algoritmo seleccionado (0–100).
- El deslizador se redirige automáticamente al habilitar un algoritmo de nivelación diferente.
- Cuando no hay ningún algoritmo de nivelación activo, la fila del deslizador se atenúa pero permanece en su lugar para que la cuadrícula de botones no se desplace.
- En v0.9.8, el deslizador ahora está presente al iniciar para cualquier DSP que se haya guardado como habilitado en el perfil de la radio, sin necesidad de alternancia manual.

### Acciones de clic derecho en botones DSP

Haga clic derecho en cualquiera de los siguientes botones para abrir el cuadro de diálogo de configuración de AetherDSP para ese algoritmo:
- **NR2**, **NR4**, **MNR**, **DFNR** (accesible a través del botón ADSP)

## Fila de información RADE

Cuando RADE (Radio Aided Direction Finding Engine) está activo, aparece una fila de información debajo de la visualización de frecuencia y encima del medidor S. Muestra:

| Elemento | Descripción |
|---|---|
| **Callsign** | El indicativo de la estación que RADE está rastreando. |
| **SNR** | Relación señal/ruido de la estación rastreada. |
| **Offset** | Desfase de frecuencia con respecto a la frecuencia central del slice. |

La fila de información RADE se oculta cuando RADE está inactivo. Esta función solo está disponible en compilaciones compiladas con soporte RADE.

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Insignia TX** | TX (rojo), oculto | Se muestra cuando este slice es el slice transmisor activo. |
| **Insignia SPLIT** | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente del slice receptor activo. |

## Selección de antena

Los botones de antena RX y TX muestran la antena actualmente seleccionada para cada ruta. Haga clic en cualquier botón para abrir un menú de selecciones de antena disponibles.

### Menú de antena RX

- Utiliza la lista de antenas RX dedicada del slice cuando está disponible (por ejemplo, en radios que proporcionan puertos de antena RX separados por slice).
- Recurre a la lista global de antenas cuando no hay una lista específica del slice disponible.
- Cada elemento del menú muestra una etiqueta legible con números de antena extraídos del identificador sin procesar.
- La información sobre herramientas muestra el identificador de antena sin procesar.

### Menú de antena TX

- Filtra automáticamente los puertos de antena solo RX.
- Utiliza las opciones de antena TX dedicadas del slice cuando están disponibles.
- La detección de antena TX busca identificadores que comiencen con "ANT", "TX" o "XVTR", y excluye identificadores que comiencen con "RX".
- Cada elemento del menú muestra una etiqueta legible con números de antena extraídos del identificador sin procesar.
- La información sobre herramientas muestra el identificador de antena sin procesar.

## Introducción de frecuencia en bandas XVTR

Cuando se opera en bandas de transverter (XVTR), la lógica de introducción de frecuencia se adapta automáticamente:

- **Comodidad de banda de 3 dígitos**: En bandas de 2m/70cm (rango de 100-999 MHz), un número entero como 1446 se interpreta como 144.6 MHz. El decimal se inserta después del tercer dígito.
- **Bandas de microondas**: Para bandas de 23cm y superiores (1000+ MHz), un número entero se trata como la frecuencia en MHz directamente (ej., 1296 significa 1296 MHz, no 129.6 MHz).
- La frecuencia máxima permitida en bandas XVTR es de 50000 MHz.

## Consejos

- Si el panel está contraído a la banda de solo frecuencia, haga clic en cualquier lugar para expandirlo y que la **Visualización de frecuencia** sea accesible para la introducción directa.
- La rueda de desplazamiento también sintoniza el slice cuando el puntero está sobre la **Visualización de frecuencia**, avanzando según el tamaño de paso actual del slice. En macOS, los eventos de desplazamiento inercial se ignoran para evitar sintonizaciones no deseadas después de que finalice un gesto.
- Haga clic derecho en la insignia del slice para cambiar su color.

## Solución de problemas

- **Escribir no tiene efecto** — Verifique que el slice no esté bloqueado. Un slice bloqueado ignora los comandos de sintonización. Desbloquéelo antes de introducir una frecuencia.
- **El panel VFO no está visible** — Haga clic en la bandera marcadora VFO del slice deseado en la pantalla del espectro para abrir el panel.
- **Faltan los botones NR2, NR4, MNR, BNR, DFNR o RN2 en la pestaña DSP** — Estos módulos del lado del cliente se movieron fuera del panel VFO en v0.9.7. Actívelos desde el menú superpuesto del espectro, el botón ADSP en la pestaña DSP o el applet AetherDSP.
- **El deslizador de nivel DSP está atenuado y no responde a los clics** — El deslizador está inactivo cuando ningún algoritmo DSP del lado de la radio que admita nivelación está habilitado actualmente. Habilite NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el deslizador.
- **El deslizador de nivel DSP falta al iniciar, aunque un DSP estaba habilitado en el perfil guardado de la radio** — Este problema se solucionó en v0.9.8. Actualice a la última versión.
- **La fila de información RADE no aparece** — Verifique que su compilación incluya soporte RADE. La fila solo se compila cuando `HAVE_RADE` está definido.
- **El menú de antena muestra etiquetas duplicadas o confusas** — El menú ahora utiliza etiquetas legibles extraídas de identificadores de antena sin procesar. El identificador sin procesar sigue estando disponible en la información sobre herramientas.

## Relacionados

- [VFO Panel overview](overview.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Change mode from the VFO panel](change-mode-from-the-vfo-panel.md)
- [Enable RIT or XIT offset from the VFO panel](enable-rit-or-xit-offset-from-the-vfo-panel.md)
