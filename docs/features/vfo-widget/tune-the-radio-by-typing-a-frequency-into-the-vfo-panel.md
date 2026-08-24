# Sintonice la radio escribiendo una frecuencia en el panel VFO

La entrada directa de frecuencia le permite saltar a una frecuencia exacta sin hacer clic en el panadapter. Escriba un valor en MHz en la pantalla de frecuencia del panel VFO y presione Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El panel VFO para el slice de destino debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO de ese slice en la pantalla del espectro.
- El slice no debe estar bloqueado. Un slice bloqueado ignora los comandos de sintonización.

## Pasos

1. Haga clic una vez en la **Frequency display**. La pantalla entra en modo de entrada directa.
2. Escriba la frecuencia deseada en MHz.
3. Presione **Enter** o **Tab** para aplicar. El slice se resintoniza inmediatamente.

### Qué sucede cuando comienza a escribir en un slice bloqueado

Si hace clic en la **Frequency display** mientras el slice está bloqueado, AetherSDR sale inmediatamente del modo de entrada directa sin aplicar la frecuencia. La pantalla muestra una superposición breve de **LOCKED**, y el slice permanece en su frecuencia actual. Desbloquee el slice primero y luego escriba la frecuencia.

## Qué hace cada control

| Control                        | Comportamiento                                                                                                                                                                                                 |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RX antenna button**          | Abre el menú de selección de antena para la antena receptora de este slice. Los elementos del menú usan la lista de antenas RX dedicada del slice cuando está disponible; de lo contrario, usan la lista global de antenas. Disponible con clic derecho. |
| **TX antenna button**          | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de antena solo de RX. Los elementos del menú usan las opciones de antena TX dedicadas del slice cuando están disponibles. Disponible con clic derecho. |
| **Frequency display**          | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa; escriba el valor en MHz y presione Enter o Tab para aplicar. Usa `FreqLineEdit` para mayor accesibilidad. Desplace la rueda del mouse sobre la pantalla para sintonizar paso a paso hacia arriba o hacia abajo según el tamaño de paso actual. |
| **Slice badge**                | Muestra la letra del slice (p. ej., A, B, C) en una insignia de color. Admite formato de texto enriquecido para renderizado HTML (#2606). El clic derecho abre el selector de color del slice. |
| **Filter width label**         | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de filtro preestablecidos en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0,1 kHz que afectaba las lecturas en modos SSB/digitales (#2197, v0.9.8). |
| **AF Gain slider (Audio tab)** | Establece el nivel de salida de audio para este slice. Predeterminado: 100. Rango: 0-100. No se guarda: refleja el estado en vivo de la radio. |
| **Pan slider (Audio tab)**     | Establece el balance estéreo izquierdo/derecho para este slice. Predeterminado: 50. Rango: 0-100. 50 = centro. El relleno del control deslizante se ancla desde el centro hacia afuera, mostrando un punto de marca central en la ranura en la posición neutral. |
| **Mute button (Audio tab)**    | Botón de alternancia. Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. Predeterminado: apagado. Haga clic derecho en la etiqueta de la pestaña Audio para alternar el silencio directamente. |
| **Squelch button + slider (Audio tab)** | Botón de alternancia. Activa el squelch para este slice. El control deslizante adyacente establece el umbral. Predeterminado: apagado. Rango: 0-100. El control deslizante usa `setManualSquelch` para el control manual del umbral. |
| **AGC combo (Audio tab)**      | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF. Predeterminado: FAST. |
| **Mode combo (Mode tab)**      | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. Predeterminado: USB. |
| **Filter preset buttons (Mode tab)** | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en ese espacio. Se pueden configurar bordes lo/hi personalizados por espacio mediante clic derecho. Se guarda en `FilterPresets`. |
| **RIT / XIT buttons + labels (X/RIT tab)** | Botones de alternancia. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda del mouse ajusta en pasos de 10 Hz. Predeterminado: apagado. |
| **DAX channel combo (DAX tab)** | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8. Predeterminado: Off. |
| **Marker thickness button**    | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se guarda por slice en `Slice{N}_MarkerWidth`. |
| **Filter edges button**        | Botón de alternancia. Alterna las líneas de borde del filtro en la banda pasante del espectro. Se guarda por slice en `Slice{N}_FilterEdgesHidden`. Predeterminado: visible. |
| **Collapse toggle**            | Colapsa el panel VFO a una tira compacta solo de frecuencia. En modo colapsado, desplazarse en cualquier parte de la tira sintoniza según el tamaño de paso actual. Haga clic derecho en modo colapsado para añadir un spot usando la frecuencia exacta del VFO (corrige #4455). Se guarda por slice en `SliceFlagCollapsed_{N}`. |

## Controles de la pestaña DSP

La pestaña DSP contiene botones de alternancia para los algoritmos de reducción de ruido y filtrado proporcionados por la radio, además de botones de lanzamiento del lado del cliente. Los siguientes botones están disponibles en la cuadrícula DSP del panel VFO:

| Botón | Descripción |
|---|---|
| **NR** | Reducción de ruido. |
| **NB** | Eliminador de ruido. |
| **ANF** | Filtro de muesca automático. |
| **MN** | Filtro de muesca manual. Se muestra solo cuando la radio informa soporte de muesca manual. |
| **APF** | Filtro de pico de audio. Visible solo cuando el slice está en modo CW. |
| **NR2 / NR4 / RN2 / BNR / MNR / DFNR / NRL / NRS / RNN / NRF** | Diversos algoritmos de reducción de ruido. La disponibilidad de botones depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| **ADSP** | Botón pulsador. Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Con estilo de alternancia DSP del lado de la radio pero sin posibilidad de marcado. |
| **AetherVoice** | Botón pulsador. Alterna la Aetherial Audio Channel Strip: la suite DSP unificada de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

Todos los botones DSP del lado de la radio están apagados de forma predeterminada.

### Control deslizante de nivel DSP

Cuando uno o más algoritmos DSP del lado de la radio que admiten control de nivel están activos, aparece un control deslizante de nivel debajo de la cuadrícula de botones DSP. La etiqueta del control deslizante muestra el nombre del algoritmo habilitado más recientemente que admite nivel (por ejemplo, **NR**, **NB**, **ANF**, **MN**, **NRL**, **NRS**, **NRF** o **ANFL**). La lectura numérica adyacente muestra el valor actual.

- Arrastre el control deslizante para establecer el nivel del algoritmo seleccionado (0-100).
- El control deslizante se redirige automáticamente cuando activa un algoritmo con nivel diferente.
- Cuando ningún algoritmo con nivel está activo, la fila del control deslizante se atenúa pero permanece en su posición para que la cuadrícula de botones no se desplace.
- En v0.9.8, el control deslizante ahora está presente al iniciar para cualquier DSP que se haya guardado como habilitado en el perfil de la radio, sin necesidad de alternarlo manualmente.

### Acciones de clic derecho en botones DSP

Haga clic derecho en cualquiera de los siguientes botones para abrir el diálogo de configuración de AetherDSP para ese algoritmo:
- **NR2**, **NR4**, **MNR**, **DFNR** (accesible mediante el botón ADSP)

## Controles de tono FM

Cuando el slice está en modo **FM**, **NFM** o **DFM**, el panel VFO proporciona controles de tono FM. Estos controles están ocultos en otros modos. Los controles de tono FM no se muestran para el modo **DSTR**.

## S-meter y Smart Meter

El panel VFO muestra un S-meter debajo de la pantalla de frecuencia (o debajo de la fila de información RADE, si RADE está activo). El S-meter usa un enfoque apilado, con un widget espaciador que se adapta a la altura del medidor.

Cuando la función Smart Meter está habilitada (mediante `SmartMeterEnabled` en `DisplaySettings`), el S-meter se reemplaza por un `SmartMtrWidget`. Este widget mantiene una relación de aspecto para determinar la altura total de la tira mediante `heightForWidth()`. La sombra de elevación para la bandera VFO se renderiza con un widget `FlagShadow` separado para evitar re-desenfocar en los repintados en vivo del medidor.

- **S-meter**: Muestra la intensidad de la señal en unidades S y dB sobre S9. El widget espaciador evita cambios de diseño cuando varía la altura del medidor.
- **Smart Meter**: Un medidor gráfico con escalas y promediado configurables. Actívelo en `DisplaySettings`. El medidor controla la altura de la tira del panel VFO para mantener su relación de aspecto.

## Controles de filtro adaptativo

Cuando la función **Adaptive Filters** está disponible (por ejemplo, para KiwiSDR o ciertos modos DSP), se muestran `AdaptiveFilterControls` debajo del área de preajustes de modo/filtro. Estos controles permiten el ajuste en tiempo real de los parámetros del filtro adaptativo y están integrados en el diseño del panel VFO.

## Barra de pestañas

El panel VFO usa una barra de pestañas con las siguientes etiquetas: **Audio** (predeterminada), **Mode**, **DSP**, **X/RIT** y **DAX**. Haga clic en una etiqueta de pestaña para cambiar al contenido de esa pestaña.

- Las etiquetas de pestaña ahora se implementan como botones `QPushButton` con soporte de enfoque de teclado. Use Tab/Shift+Tab para navegar entre pestañas.
- La pestaña activa se resalta con un subrayado cian (`#00b4d8`). Las pestañas inactivas tienen un subrayado transparente y usan el color atenuado `#6888a0`.
- Haga clic derecho en la etiqueta de la pestaña **Audio** para alternar el silencio del slice actual.

## Fila de información RADE

Cuando RADE (Radio Aided Direction Finding Engine) está activo, aparece una fila de información debajo de la pantalla de frecuencia y encima del S-meter. Muestra:

| Elemento | Descripción |
|---|---|
| **Callsign** | El indicativo de la estación que RADE está rastreando. |
| **SNR** | Relación señal/ruido para la estación rastreada. |
| **Offset** | Desfase de frecuencia desde la frecuencia central del slice. |

La fila de información RADE se oculta cuando RADE está inactivo. Esta función solo está disponible en compilaciones creadas con soporte RADE.

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **TX badge** | TX (rojo), oculto | Se muestra cuando este slice es el slice transmisor activo. |
| **SPLIT badge** | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente del slice receptor activo. El texto de la insignia cambia a **SWAP** cuando el par dividido se puede intercambiar. |

La insignia SPLIT usa mayor contraste para mejor visibilidad: color predeterminado `rgba(255,255,255,120)`, color al pasar el cursor `rgba(255,255,255,180)`.

## Selección de antena

Los botones de antena RX y TX muestran la antena seleccionada actualmente para cada ruta. Haga clic en cualquiera de los botones para abrir un menú de selecciones de antena disponibles.

### Menú de antena RX

- Usa la lista de antenas RX dedicada del slice cuando está disponible (por ejemplo, en radios que proporcionan puertos de antena RX separados por slice).
- Recurre a la lista global de antenas cuando no hay una lista específica del slice disponible.
- Cada elemento del menú muestra una etiqueta legible con los números de antena extraídos del identificador sin procesar.
- Los tooltips muestran el identificador de antena sin procesar.

### Menú de antena TX

- Filtra automáticamente los puertos de antena solo de RX.
- Usa las opciones de antena TX dedicadas del slice cuando están disponibles.
- La detección de antena TX busca identificadores que comiencen con "ANT", "TX" o "XVTR", y excluye los identificadores que comiencen con "RX".
- Cada elemento del menú muestra una etiqueta legible con los números de antena extraídos del identificador sin procesar.
- Los tooltips muestran el identificador de antena sin procesar.

## Entrada de frecuencia en bandas XVTR

Cuando opera en bandas de transverter (XVTR), la lógica de entrada de frecuencia se adapta automáticamente:

- **Conveniencia de banda de 3 dígitos**: En bandas de 2 m/70 cm (rango de 100-999 MHz), un entero simple como 1446 se interpreta como 144,6 MHz. El decimal se inserta después del tercer dígito.
- **Bandas de microondas**: Para bandas de 23 cm y superiores (1000+ MHz), un entero simple se trata como la frecuencia en MHz directamente (p. ej., 1296 significa 1296 MHz, no 129,6 MHz).
- **Entrada explícita en MHz en bandas no XVTR**: Si escribe una frecuencia en MHz superior a 54 MHz (por ejemplo, escribir "146.520"), AetherSDR ahora detecta la entrada explícita en MHz y trata el valor como MHz en lugar de intentar el análisis de respaldo en kHz/Hz. Esto permite la entrada directa de frecuencia para bandas VHF/UHF incluso cuando el perfil de la radio no informa una antena XVTR.
- La frecuencia máxima permitida es 50000 MHz para bandas XVTR y para entradas explícitas en MHz superiores a 54 MHz. Para todas las demás entradas, el máximo es 54 MHz.

## Detalles del análisis de entrada de frecuencia

Cuando escribe un valor de frecuencia, AetherSDR lo analiza de la siguiente manera:

- **Puntos en la entrada**: Múltiples puntos (p. ej., "14.225.000") se normalizan a un solo punto decimal. El valor se interpreta entonces como MHz.
- **Valores ≤ 54 MHz (bandas HF)**:
  - Valores > 54000 se tratan como Hz y se dividen por 1.000.000.
  - Valores > 54 se tratan como kHz y se dividen por 1000.
  -
