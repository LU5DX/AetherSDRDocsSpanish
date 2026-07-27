# Sintonice la radio escribiendo una frecuencia en el panel VFO

La introducción directa de frecuencia le permite saltar a una frecuencia exacta sin tener que hacer clic en el panadapter. Escriba un valor en MHz en la pantalla de frecuencia del panel VFO y presione Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El panel VFO para el slice de destino debe estar abierto. Si no está visible, haga clic en la bandera marcadora VFO de ese slice en la pantalla del espectro.
- El slice no debe estar bloqueado. Un slice bloqueado ignora los comandos de sintonización.

## Pasos

1. Haga clic una vez en la **Frequency display**. La pantalla entra en modo de introducción directa.
2. Escriba la frecuencia deseada en MHz.
3. Presione **Enter** o **Tab** para aplicar. El slice se resintoniza inmediatamente.

### Qué sucede cuando empieza a escribir en un slice bloqueado

Si hace clic en la **Frequency display** mientras el slice está bloqueado, AetherSDR sale inmediatamente del modo de introducción directa sin aplicar la frecuencia. La pantalla muestra brevemente una superposición **LOCKED** y el slice permanece en su frecuencia actual. Desbloquee el slice primero y luego introduzca la frecuencia.

## Qué hace cada control

| Control                        | Comportamiento                                                                                                                                                                                                 |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Botón de antena RX**         | Abre el menú de selección de antena para la antena receptora de este slice. Los elementos del menú utilizan la lista de antenas RX dedicadas del slice cuando está disponible; de lo contrario, recurren a la lista global de antenas. Se puede hacer clic derecho. |
| **Botón de antena TX**         | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de antena de solo RX. Los elementos del menú utilizan las opciones de antena TX dedicadas del slice cuando están disponibles. Se puede hacer clic derecho. |
| **Frequency display**          | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la introducción directa; escriba MHz y presione Enter o Tab para aplicar. Utiliza `FreqLineEdit` para mayor accesibilidad. Desplace la rueda del ratón sobre la pantalla para sintonizar paso a paso hacia arriba o hacia abajo según el tamaño de paso actual. |
| **Insignia del slice (Slice badge)** | Muestra la letra del slice (p. ej., A, B, C) en una insignia de color. Admite formato de texto enriquecido para renderizado HTML (#2606). Al hacer clic derecho se abre el selector de color del slice. |
| **Etiqueta de ancho de filtro** | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de ajuste preestablecido del filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| **Deslizador de ganancia AF (pestaña Audio)** | Establece el nivel de salida de audio para este slice. Valor predeterminado: 100. Rango: 0-100. No se persiste: refleja el estado en vivo de la radio. |
| **Deslizador de paneo (pestaña Audio)** | Establece el paneo estéreo izquierdo/derecho para este slice. Valor predeterminado: 50. Rango: 0-100. 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, mostrando un punto de marca central en la ranura en la posición neutra. |
| **Botón de silencio (pestaña Audio)** | Botón de alternancia. Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. Valor predeterminado: desactivado. Haga clic derecho en la etiqueta de la pestaña Audio para alternar el silencio directamente. |
| **Botón y deslizador de squelch (pestaña Audio)** | Botón de alternancia. Activa el squelch para este slice. El deslizador adyacente establece el umbral. Valor predeterminado: desactivado. Rango: 0-100. |
| **Combo AGC (pestaña Audio)**  | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF. Valor predeterminado: FAST. |
| **Combo de modo (pestaña Mode)** | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. Valor predeterminado: USB. |
| **Botones de ajuste preestablecido de filtro (pestaña Mode)** | Aplica un ajuste preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se pueden configurar bordes lo/hi personalizados por ranura mediante clic derecho. Se persiste en `FilterPresets`. |
| **Botones y etiquetas RIT/XIT (pestaña X/RIT)** | Botones de alternancia. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. Valor predeterminado: desactivado. |
| **Combo de canal DAX (pestaña DAX)** | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8. Valor predeterminado: Off. |
| **Botón de grosor del marcador** | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se persiste por slice en `Slice{N}_MarkerWidth`. |
| **Botón de bordes del filtro** | Botón de alternancia. Alterna las líneas de borde del filtro en la banda pasante del espectro. Se persiste por slice en `Slice{N}_FilterEdgesHidden`. Valor predeterminado: mostrado. |
| **Alternancia de colapso** | Colapsa el panel VFO a una tira compacta de solo frecuencia. En modo colapsado, desplazar el ratón en cualquier lugar de la tira sintoniza según el tamaño de paso actual. Se persiste por slice en `SliceFlagCollapsed_{N}`. |

## Controles de la pestaña DSP

La pestaña DSP contiene botones de alternancia para los algoritmos de reducción de ruido y filtrado proporcionados por la radio, además de botones de inicio del lado del cliente. Los siguientes botones están disponibles en la cuadrícula DSP del panel VFO:

| Botón | Descripción |
|---|---|
| **NR** | Reducción de ruido. |
| **NB** | Eliminador de ruido. |
| **ANF** | Filtro de muesca automático. |
| **APF** | Filtro de pico de audio. Visible solo cuando el slice está en modo CW. |
| **NR2 / NR4 / RN2 / BNR / MNR / DFNR / NRL / NRS / RNN / NRF** | Varios algoritmos de reducción de ruido. La disponibilidad de los botones depende de la serie de la radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| **ADSP** | Botón pulsador. Abre el diálogo de configuración de AetherDSP (NR2/NR4/DFNR/RN2/BNR/MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Tiene el estilo de una alternancia DSP del lado de la radio pero no es verificable. |
| **AetherVoice** | Botón pulsador. Alterna la tira de canales de audio Aetherial: el conjunto DSP unificado de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

Todos los botones DSP del lado de la radio están desactivados de forma predeterminada.

### Deslizador de nivel DSP

Cuando uno o más algoritmos DSP del lado de la radio que admiten un control de nivel están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra el nombre del algoritmo habilitado más recientemente que admita nivelación (por ejemplo, **NR**, **NB**, **ANF**, **NRL**, **NRS**, **NRF** o **ANFL**). La lectura numérica adyacente muestra el valor actual.

- Arrastre el deslizador para establecer el nivel del algoritmo objetivo (0-100).
- El deslizador se reorienta automáticamente cuando habilita un algoritmo nivelado diferente.
- Cuando no hay ningún algoritmo nivelado activo, la fila del deslizador se atenúa pero permanece en su posición para que la cuadrícula de botones no se desplace.
- En v0.9.8, el deslizador ahora está presente al inicio para cualquier DSP que se haya guardado como habilitado en el perfil de la radio, sin necesidad de alternancia manual.

### Acciones de clic derecho en los botones DSP

Haga clic derecho en cualquiera de los siguientes botones para abrir el diálogo de configuración de AetherDSP para ese algoritmo:
- **NR2**, **NR4**, **MNR**, **DFNR** (accesible a través del botón ADSP)

## S-meter y Smart Meter

El panel VFO muestra un S-meter debajo de la pantalla de frecuencia (o debajo de la fila de información RADE, si RADE está activo). El S-meter utiliza un enfoque apilado, con un widget espaciador que se adapta a la altura del medidor.

Cuando la función Smart Meter está habilitada (a través de `SmartMeterEnabled` en `DisplaySettings`), el S-meter se reemplaza por un `SmartMtrWidget`. Este widget mantiene una relación de aspecto para impulsar la altura general de la tira a través de `heightForWidth()`. La sombra de elevación para la bandera VFO se renderiza mediante un widget `FlagShadow` separado para evitar volver a desenfocar en las repintadas del medidor en vivo.

- **S-meter**: Muestra la intensidad de la señal en unidades S y dB sobre S9. El widget espaciador evita cambios de diseño cuando varía la altura del medidor.
- **Smart Meter**: Un medidor gráfico con escalas y promediado configurables. Actívelo en `DisplaySettings`. El medidor controla la altura de la tira del panel VFO para mantener su relación de aspecto.

## Controles de filtro adaptativo

Cuando la función **Adaptive Filters** está disponible (por ejemplo, para KiwiSDR o ciertos modos DSP), `AdaptiveFilterControls` se muestran debajo del área de modos/ajustes preestablecidos de filtro. Estos controles permiten el ajuste en tiempo real de los parámetros del filtro adaptativo y están integrados en el diseño del panel VFO.

## Barra de pestañas

El panel VFO utiliza una barra de pestañas con las siguientes etiquetas: **Audio** (predeterminada), **Mode**, **DSP**, **X/RIT** y **DAX**. Haga clic en una etiqueta de pestaña para cambiar al contenido de esa pestaña.

- Las etiquetas de las pestañas ahora se implementan como botones `QPushButton` con soporte de foco de teclado. Use Tab/Shift+Tab para navegar entre las pestañas.
- La pestaña activa se resalta con un subrayado cian (`#00b4d8`). Las pestañas inactivas tienen un subrayado transparente y usan el color atenuado `#6888a0`.
- Haga clic derecho en la etiqueta de la pestaña **Audio** para alternar el silencio del slice actual.

## Fila de información RADE

Cuando RADE (Radio Aided Direction Finding Engine) está activo, aparece una fila de información debajo de la pantalla de frecuencia y encima del S-meter. Muestra:

| Elemento | Descripción |
|---|---|
| **Callsign** | El indicativo de la estación que RADE está rastreando. |
| **SNR** | Relación señal/ruido para la estación rastreada. |
| **Offset** | Desplazamiento de frecuencia desde la frecuencia central del slice. |

La fila de información RADE se oculta cuando RADE está inactivo. Esta función solo está disponible en compilaciones creadas con soporte RADE.

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Insignia TX** | TX (rojo), oculto | Se muestra cuando este slice es el slice transmisor activo. |
| **Insignia SPLIT** | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente al slice receptor activo. El texto de la insignia cambia a **SWAP** cuando se puede intercambiar el par dividido. |

La insignia SPLIT utiliza un contraste mejorado para una mejor visibilidad: color predeterminado `rgba(255,255,255,120)`, color al pasar el ratón `rgba(255,255,255,180)`.

## Selección de antena

Los botones de antena RX y TX muestran la antena seleccionada actualmente para cada ruta. Haga clic en cualquier botón para abrir un menú de selecciones de antena disponibles.

### Menú de antena RX

- Utiliza la lista de antenas RX dedicadas del slice cuando está disponible (por ejemplo, en radios que proporcionan puertos de antena RX separados por slice).
- Recurre a la lista global de antenas cuando no hay una lista específica del slice disponible.
- Cada elemento del menú muestra una etiqueta legible por humanos con los números de antena extraídos del identificador original.
- Los tooltips muestran el identificador de antena original.

### Menú de antena TX

- Filtra automáticamente los puertos de antena de solo RX.
- Utiliza las opciones de antena TX dedicadas del slice cuando están disponibles.
- La detección de antena TX busca identificadores que comiencen con "ANT", "TX" o "XVTR", y excluye los identificadores que comienzan con "RX".
- Cada elemento del menú muestra una etiqueta legible por humanos con los números de antena extraídos del identificador original.
- Los tooltips muestran el identificador de antena original.

## Introducción de frecuencia en bandas XVTR

Cuando se opera en bandas de transvertor (XVTR), la lógica de introducción de frecuencia se adapta automáticamente:

- **Comodidad de banda de 3 dígitos**: En bandas de 2m/70cm (rango de 100-999 MHz), un número entero simple como 1446 se interpreta como 144,6 MHz. El decimal se inserta después del tercer dígito.
- **Bandas de microondas**: Para bandas de 23 cm y superiores (1000+ MHz), un número entero simple se trata directamente como la frecuencia en MHz (p. ej., 1296 significa 1296 MHz, no 129,6 MHz).
- **Introducción explícita de MHz en bandas no XVTR**: Si escribe una frecuencia en MHz que está por encima de 54 MHz (por ejemplo, escribiendo "146.520"), AetherSDR ahora detecta la introducción explícita de MHz y trata el valor como MHz en lugar de intentar el análisis de respaldo de kHz/Hz. Esto permite la introducción directa de frecuencia para bandas VHF/UHF incluso cuando el perfil de la radio no informa una antena XVTR.
- La frecuencia máxima permitida es 50000 MHz para bandas XVTR y para introducciones explícitas de MHz por encima de 54 MHz. Para todas las demás introducciones, el máximo es 54 MHz.

## Detalles del análisis de introducción de frecuencia

Cuando escribe un valor de frecuencia, AetherSDR lo analiza de la siguiente manera:

- **Puntos en la entrada**: Varios puntos (p. ej., "14.225.000") se normalizan a un único punto decimal. Luego, el valor se interpreta como MHz.
- **Valores ≤ 54 MHz (bandas HF)**:
  - Los valores > 54000 se tratan como Hz y se dividen por 1.000.000.
  - Los valores > 54 se tratan como kHz y se dividen por 1000.
  - Los valores ≤ 54 se tratan directamente como MHz.
- **Valores > 54 MHz (bandas VHF/UHF
