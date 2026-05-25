# Sintonice la radio escribiendo una frecuencia en el panel VFO

La entrada directa de frecuencia le permite saltar a una frecuencia exacta sin hacer clic en el panadaptador. Escriba un valor en MHz en la pantalla de frecuencia del panel VFO y presione Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El panel VFO para el slice destino debe estar abierto. Si no está visible, haga clic en la bandera marcadora VFO de ese slice en la pantalla del espectro.
- El slice no debe estar bloqueado. Un slice bloqueado ignora los comandos de sintonización.

## Pasos

1. Haga clic una vez en la **Pantalla de frecuencia**. La pantalla entra en modo de entrada directa.
2. Escriba la frecuencia deseada en MHz.
3. Presione **Enter** o **Tab** para aplicar. El slice se resintoniza inmediatamente.

### Qué sucede cuando empieza a escribir en un slice bloqueado

Si hace clic en la **Pantalla de frecuencia** mientras el slice está bloqueado, AetherSDR sale inmediatamente del modo de entrada directa sin aplicar la frecuencia. La pantalla muestra brevemente una superposición **LOCKED**, y el slice permanece en su frecuencia actual. Desbloquee el slice primero, luego ingrese la frecuencia.

## Función de cada control

| Control                      | Comportamiento                                                                                                                                                                                                                     |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Botón de antena RX**       | Abre el menú de selección de antena para la antena receptora de este slice. Los elementos del menú usan la lista de antenas RX dedicada del slice cuando está disponible, y recurren a la lista global de antenas. Clic derecho disponible. |
| **Botón de antena TX**       | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de solo RX. Los elementos del menú usan las opciones de antena TX dedicadas del slice cuando están disponibles. Clic derecho disponible.        |
| **Pantalla de frecuencia**   | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa; escriba MHz y presione Enter o Tab para aplicar. Gire la rueda del ratón sobre la pantalla para sintonizar hacia arriba o abajo según el tamaño de paso actual. |
| **Insignia del slice**       | Muestra la letra del slice (ej., A, B, C) en una insignia de color. Admite formato de texto enriquecido para renderizado HTML (#2606). Clic derecho abre el selector de color del slice.                                                        |
| **Etiqueta de ancho de filtro** | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Modo. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| **Control deslizante de ganancia AF (pestaña Audio)** | Establece el nivel de salida de audio para este slice. Predeterminado: 100. Rango: 0-100. No se conserva — refleja el estado en vivo de la radio.                                                                                  |
| **Control deslizante de paneo (pestaña Audio)** | Establece el paneo estéreo izquierdo/derecho para este slice. Predeterminado: 50. Rango: 0-100. 50 = centro.                                                                                                                       |
| **Botón de silencio (pestaña Audio)** | Botón de alternancia. Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. Predeterminado: desactivado.                                                                                              |
| **Botón + control deslizante de squelch (pestaña Audio)** | Botón de alternancia. Activa el squelch para este slice. El control deslizante adyacente establece el umbral. Predeterminado: desactivado. Rango: 0-100.                                                                       |
| **Combo AGC (pestaña Audio)** | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF. Predeterminado: FAST.                                                                                                          |
| **Combo de modo (pestaña Modo)** | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. Predeterminado: USB.                                                                                     |
| **Botones preestablecidos de filtro (pestaña Modo)** | Aplica un ancho de filtro guardado preestablecido. Clic derecho para guardar el ancho de filtro actual en esa ranura. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. Se conservan en `FilterPresets`. |
| **Botones + etiquetas RIT/XIT (pestaña X/RIT)** | Botones de alternancia. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. Predeterminado: desactivado.      |
| **Combo de canal DAX (pestaña DAX)** | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8. Predeterminado: Off.                                                                                                                                                |
| **Botón de grosor del marcador** | Alterna la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por slice en `Slice{N}_MarkerWidth`.                                                                                                                         |
| **Botón de bordes del filtro** | Botón de alternancia. Alterna las líneas del borde del filtro en la banda pasante del espectro. Se conserva por slice en `Slice{N}_FilterEdgesHidden`. Predeterminado: mostradas.                                                  |
| **Alternancia de colapso**    | Colapsa el panel VFO a una tira compacta de solo frecuencia. En modo colapsado, desplazarse en cualquier lugar de la tira sintoniza según el tamaño de paso actual. Se conserva por slice en `SliceFlagCollapsed_{N}`.               |

## Controles de la pestaña DSP

La pestaña DSP contiene botones de alternancia para algoritmos de reducción de ruido y filtrado suministrados por la radio, además de botones de inicio del lado del cliente. Los siguientes botones están disponibles en la cuadrícula DSP del panel VFO:

| Botón | Descripción |
|---|---|
| **NR** | Reducción de ruido. |
| **NB** | Eliminador de ruido. |
| **ANF** | Filtro de muesca automático. |
| **APF** | Filtro de pico de audio. Visible solo cuando el slice está en modo CW. |
| **NR2 / NR4 / RN2 / BNR / MNR / DFNR / NRL / NRS / RNN / NRF** | Varios algoritmos de reducción de ruido. La disponibilidad del botón depende de la serie de radio y la compilación. Clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| **ADSP** | Botón pulsador. Abre el diálogo de configuración de AetherDSP (NR2/NR4/DFNR/RN2/BNR/MNR del lado del cliente). Mismo punto de entrada que el menú de Configuración (v0.9.8). Tiene estilo de alternancia DSP del lado de la radio pero no es marcable. |
| **AetherVoice** | Botón pulsador. Alterna la tira de canales de audio Aetherial — el conjunto unificado de DSP TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

Todos los botones DSP del lado de la radio están desactivados por defecto.

### Control deslizante de nivel DSP

Cuando uno o más algoritmos DSP del lado de la radio que admiten un control de nivel están activos, aparece un control deslizante de nivel debajo de la cuadrícula de botones DSP. La etiqueta del control deslizante muestra el nombre del algoritmo habilitado más recientemente que admita nivelación (por ejemplo, **NR**, **NB**, **ANF**, **NRL**, **NRS**, **NRF** o **ANFL**). La lectura numérica adyacente muestra el valor actual.

- Arrastre el control deslizante para establecer el nivel del algoritmo objetivo (0-100).
- El control deslizante se reorienta automáticamente cuando habilita un algoritmo de nivelación diferente.
- Cuando no hay ningún algoritmo de nivelación activo, la fila del control deslizante se atenúa pero permanece en su posición para que la cuadrícula de botones no se desplace.
- En v0.9.8, el control deslizante ahora está presente al inicio para cualquier DSP que se haya guardado como habilitado en el perfil de la radio, sin necesidad de alternancia manual.

### Acciones de clic derecho en botones DSP

Haga clic derecho en cualquiera de los siguientes botones para abrir el diálogo de configuración de AetherDSP para ese algoritmo:
- **NR2**, **NR4**, **MNR**, **DFNR** (accesible a través del botón ADSP)

## Fila de información RADE

Cuando RADE (Radio Aided Direction Finding Engine) está activo, aparece una fila de información debajo de la pantalla de frecuencia y encima del S-meter. Muestra:

| Elemento | Descripción |
|---|---|
| **Callsign** | El indicativo de la estación que RADE está rastreando. |
| **SNR** | Relación señal/ruido para la estación rastreada. |
| **Offset** | Desplazamiento de frecuencia desde la frecuencia central del slice. |

La fila de información RADE está oculta cuando RADE está inactivo. Esta función solo está disponible en compilaciones creadas con soporte RADE.

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Insignia TX** | TX (rojo), oculto | Se muestra cuando este slice es el slice transmisor activo. |
| **Insignia SPLIT** | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente al slice receptor activo. |

## Selección de antena

Los botones de antena RX y TX muestran la antena actualmente seleccionada para cada ruta. Haga clic en cualquier botón para abrir un menú de selecciones de antena disponibles.

### Menú de antena RX

- Utiliza la lista de antenas RX dedicada del slice cuando está disponible (por ejemplo, en radios que proporcionan puertos de antena RX separados por slice).
- Recurre a la lista global de antenas cuando no hay una lista específica del slice disponible.
- Cada elemento del menú muestra una etiqueta legible con los números de antena extraídos del identificador sin procesar.
- Los tooltips muestran el identificador de antena sin procesar.

### Menú de antena TX

- Filtra automáticamente los puertos de solo RX.
- Utiliza las opciones de antena TX dedicadas del slice cuando están disponibles.
- La detección de antena TX busca identificadores que comiencen con "ANT", "TX" o "XVTR", y excluye identificadores que comiencen con "RX".
- Cada elemento del menú muestra una etiqueta legible con los números de antena extraídos del identificador sin procesar.
- Los tooltips muestran el identificador de antena sin procesar.

## Entrada de frecuencia en bandas XVTR

Cuando opera en bandas de transvertor (XVTR), la lógica de entrada de frecuencia se adapta automáticamente:

- **Conveniencia de banda de 3 dígitos**: En bandas de 2m/70cm (rango de 100-999 MHz), un número entero como 1446 se interpreta como 144.6 MHz. El decimal se inserta después del tercer dígito.
- **Bandas de microondas**: Para bandas de 23cm y superiores (1000+ MHz), un número entero se trata directamente como la frecuencia en MHz (ej., 1296 significa 1296 MHz, no 129.6 MHz).
- **Entrada explícita en MHz en bandas no XVTR**: Si escribe una frecuencia en MHz que está por encima de 54 MHz (por ejemplo, escribiendo "146.520"), AetherSDR ahora detecta la entrada explícita en MHz y trata el valor como MHz en lugar de intentar el análisis de respaldo en kHz/Hz. Esto permite la entrada directa de frecuencia para bandas VHF/UHF incluso cuando el perfil de la radio no informa una antena XVTR.
- La frecuencia máxima permitida es 50000 MHz para bandas XVTR y para entradas explícitas en MHz por encima de 54 MHz. Para todas las demás entradas, el máximo es 54 MHz.

## Detalles del análisis de entrada de frecuencia

Cuando escribe un valor de frecuencia, AetherSDR lo analiza de la siguiente manera:

- **Puntos en la entrada**: Múltiples puntos (ej., "14.225.000") se normalizan a un solo punto decimal. Luego, el valor se interpreta como MHz.
- **Valores ≤ 54 MHz (bandas HF)**:
  - Los valores > 54000 se tratan como Hz y se dividen por 1,000,000.
  - Los valores > 54 se tratan como kHz y se dividen por 1000.
  - Los valores ≤ 54 se tratan directamente como MHz.
- **Valores > 54 MHz (bandas VHF/UHF/SHF)**:
  - Si escribió explícitamente MHz (incluyendo un punto decimal o usando el formato "14.225.000"), el valor se usa directamente como MHz.
  - Si escribió un número entero, se aplica el análisis de conveniencia de banda de 3 dígitos (ver arriba).
  - El valor máximo permitido es 50000 MHz.

## Consejos

- Si el panel está colapsado a la tira de solo frecuencia, haga clic en cualquier lugar para expandirlo y que la **Pantalla de frecuencia** sea accesible para la entrada directa.
- La rueda del ratón también sintoniza el slice cuando el puntero está sobre la **Pantalla de frecuencia**, avanzando según el tamaño de paso actual del slice. En macOS, los eventos de desplazamiento inercial se ignoran para evitar sintonizaciones no deseadas después de que finalice un gesto. En modo colapsado, desplazarse en cualquier lugar de la tira sintoniza según el tamaño de paso.
- Cuando el slice está bloqueado, la rueda del ratón no sintoniza y muestra brevemente una superposición **LOCKED**.
- Haga clic derecho en la insignia del slice para cambiar su color.

## Solución de problemas

- **Escribir no tiene efecto o aparece la superposición LOCKED** — El slice está bloqueado. Desbloquéelo antes de ingresar una frecuencia.
- **El panel VFO no está visible** — Haga clic en la bandera marcadora VFO del slice deseado en la pantalla del espectro para abrir el panel.
- **Escribí una frecuencia VHF pero se interpretó incorrectamente** — Use la entrada explícita en MHz incluyendo un punto decimal (ej., "146.520" en lugar de "146520"). AetherSDR ahora detecta esto y trata el valor como MHz.
- **Faltan los botones NR2, NR4, MNR, BNR, DFNR o RN2 en la pestaña DSP** — Estos módulos del lado del cliente se movieron fuera del panel VFO en v0.9.7. Actívelos desde el menú de superposición del espectro, el botón ADSP en la pestaña DSP o el applet AetherDSP.
- **El control deslizante de nivel DSP está atenuado y no responde a los clics** — El control deslizante está inactivo cuando ningún algoritmo DSP del lado de la radio que admita nivelación está habilitado actualmente. Active NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el control deslizante.
- **El control deslizante de nivel DSP falta al inicio aunque un DSP estuviera habilitado en el perfil guardado de la radio** — Este problema se solucionó en v0.9.8. Actualice a la versión más reciente.
- **La fila de información RADE no aparece** — Verifique que su compilación incluya soporte RADE. La fila solo se compila cuando `HAVE_RADE` está definido.
- **El menú de antena muestra etiquetas duplicadas o confusas** — El menú ahora utiliza etiquetas legibles extraídas de los identificadores de antena sin procesar. El identificador sin proces
