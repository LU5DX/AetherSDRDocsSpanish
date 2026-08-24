# Panel VFO

El Panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes más utilizados por slice — modo, presets de filtro, selección de antena, ganancia AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. El panel puede colapsarse a una franja compacta de solo frecuencia.

## Abrir el Panel VFO

1. En la pantalla del espectro, haga clic en el marcador de la bandera VFO (el pequeño triángulo o bandera en la parte superior de la línea del marcador VFO).
2. El Panel VFO se abre como una ventana flotante anclada al marcador.

## Controles

El Panel VFO está organizado en pestañas: Audio, DSP, Mode, X/RIT y DAX. Las etiquetas de las pestañas ahora se representan como `QPushButton` para accesibilidad mediante teclado y estilo de enfoque consistente. Haga clic derecho en la etiqueta de la pestaña **Audio** para alternar el silencio directamente.

### Controles comunes (siempre visibles)

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón de antena RX | Botón pulsador | Abre el menú de selección de antena para la antena receptora de este slice. Muestra la lista de antenas RX específica del slice cuando está disponible; de lo contrario, usa la lista de antenas del radio. |
| Botón de antena TX | Botón pulsador | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de antena solo RX. Muestra la lista de antenas TX específica del slice cuando está disponible; de lo contrario, usa la lista de antenas del radio. |
| Indicador de frecuencia | Indicador | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. Cuando el slice está bloqueado, muestra una superposición "LOCKED" y evita la entrada directa de frecuencia. En bandas XVTR, la entrada de números enteros en el rango de 100-999 MHz inserta un decimal después del tercer dígito (por ejemplo, 1446 → 144,6). Accesibilidad: el texto de frecuencia se anuncia mediante `QAccessibleValueChangeEvent` cuando cambia. |
| Etiqueta de ancho de filtro | Indicador | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preset de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital. |
| Insignia TX | Indicador | Se muestra (en rojo) cuando este slice es el slice transmisor activo. Se oculta de lo contrario. |
| Insignia SPLIT | Indicador | Se muestra (en ámbar) cuando TX está asignado a un slice diferente del slice receptor activo. Se oculta de lo contrario. El texto de la insignia puede ser "SWAP" para indicar operación en split; al hacer clic se realiza un intercambio. La opacidad de la insignia se ha incrementado para mejor visibilidad. |
| Botón de grosor del marcador | Botón pulsador | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. El ajuste se guarda por slice (`Slice{N}_MarkerWidth`). |
| Botón de bordes de filtro | Botón de alternancia | Alterna las líneas de borde del filtro en la banda de paso del espectro. El ajuste se guarda por slice (`Slice{N}_FilterEdgesHidden`). Valor predeterminado: mostrado. |
| Alternancia de colapso | Botón de alternancia | Colapsa el Panel VFO a una franja compacta de solo frecuencia. El ajuste se guarda por slice (`SliceFlagCollapsed_{N}`). Valor predeterminado: expandido. |
| Insignia de slice | Indicador | Muestra la letra del slice en una insignia de color. Haga clic para abrir el menú contextual del slice. |

### Pestaña Audio

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Control deslizante de ganancia AF | Control deslizante | 0-100 | Establece el nivel de salida de audio para este slice. Valor predeterminado: 100. No se guarda — refleja el estado en vivo del radio. |
| Control deslizante de paneo | Control deslizante | 0-100 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. Valor predeterminado: 50. El relleno del control deslizante se ancla desde el centro hacia afuera, con un punto de marca central visible en la ranura. |
| Botón de silencio | Botón de alternancia | On/Off | Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. Valor predeterminado: off. También accesible mediante clic derecho en la etiqueta de la pestaña Audio. |
| Botón + control deslizante de squelch | Botón de alternancia + control deslizante | 0-100 | Habilita el squelch para este slice. El control deslizante adyacente establece el umbral. Valor predeterminado: off. El squelch se desactiva automáticamente en modos digital, RTTY y CW. |
| Combinación AGC | Cuadro combinado | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este slice. Valor predeterminado: FAST. |

### Pestaña DSP

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | Botón de alternancia | Habilita el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie del radio y la compilación. Valor predeterminado: off. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón MN | Botón de alternancia | Habilita el filtro de muesca manual para este slice. Solo se muestra en radios que admiten filtrado de muesca manual. Valor predeterminado: off. Oculto de lo contrario. |
| Botón ADSP | Botón pulsador | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Al hacer clic, eleva y enfoca el diálogo de Configuración de AetherDSP sin modo. No marcable; con estilo similar a una alternancia DSP del lado del radio. |
| Botón AetherVoice | Botón pulsador | Alterna la Aetherial Audio Channel Strip — la suite DSP TX/RX unificada. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

### Pestaña Mode

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Combinación de modo | Cuadro combinado | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este slice. Valor predeterminado: USB. |
| Botones de preset de filtro | Botón pulsador | N/A | Aplica un preset guardado de ancho de filtro. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se guarda en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón + etiqueta RIT | Botón de alternancia + indicador | Habilita la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. Valor predeterminado: off. |
| Botón + etiqueta XIT | Botón de alternancia + indicador | Habilita la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. Valor predeterminado: off. |

### Pestaña DAX

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Combinación de canal DAX | Cuadro combinado | Off, 1-8 | Asigna un canal de audio DAX a este slice. Valor predeterminado: Off. |

## Comportamiento de Entrada de Frecuencia

### Entrada Directa de Frecuencia

1. Haga clic una vez en el indicador de frecuencia. El indicador cambia a un campo editable que muestra la frecuencia actual.
2. Escriba la frecuencia deseada y presione Enter o Tab para aplicarla. El sistema analiza la entrada de forma flexible:
   - **Entrada en MHz**: Escriba un valor en MHz (por ejemplo, "14.225", "14.225.000", "14225", "14225.0"). Los puntos más allá del primero se eliminan automáticamente.
   - **Entrada en kHz**: En bandas HF, los números enteros sin punto mayores de 54000 se tratan como Hz; de lo contrario, se tratan como kHz. Por ejemplo, "14225" se convierte en 14,225 MHz (interpretación en kHz), mientras que "14225000" se convierte en 14,225 MHz (interpretación en Hz).
   - **Entrada en banda XVTR**: En bandas XVTR, se aceptan valores superiores a 54 MHz. Un número entero en el rango de 100-999 inserta un decimal después del tercer dígito (por ejemplo, "1446" → 144,6 MHz).

El campo de edición de frecuencia ahora usa `FreqLineEdit` con texto de sugerencia "MHz (e.g. 14.225)" en lugar de texto de marcador de posición.

### Entrada Explícita en MHz

Cuando escribe explícitamente un valor con decimal y supera los 54 MHz, el sistema lo trata como un valor en MHz en lugar de intentar la conversión Hz/kHz. Esto permite la entrada directa de frecuencias VHF/UHF/SHF en MHz sin ambigüedad.

### Comportamiento con Slice Bloqueado

Cuando un slice está bloqueado en frecuencia:
- El indicador de frecuencia muestra una superposición "LOCKED".
- Hacer clic en el indicador de frecuencia no inicia la entrada directa.
- La sintonización con la rueda del ratón está bloqueada, incluso en modo colapsado.
- Una notificación audible indica que se bloqueó el intento de sintonización.

## Comportamiento de la Rueda del Ratón

La dirección de sintonización con la rueda del ratón respeta el ajuste **Reverse mouse wheel** en la configuración de Interacción. Cuando está habilitado, la dirección de sintonización se invierte, y la dirección de zoom en el panadapter también se invierte. El ajuste `reverseMouseWheel()` se verifica en el `wheelEvent` del widget VFO.

## Comportamiento del Squelch

El squelch se desactiva automáticamente en modos digital, RTTY y CW:
- **Digital y RTTY**: El audio se alimenta a decodificadores externos mediante DAX; el squelch no es significativo y puede bloquear señales FSK débiles.
- **CW**: El radio bloquea el squelch activado en un nivel fijo y rechaza cambios del cliente.

Al cambiar a un modo donde el squelch está desactivado mientras el squelch está activo, el sistema guarda el estado del squelch y lo apaga. Al volver a un modo donde el squelch está permitido, se restaura el estado anterior del squelch.

El control de squelch se ha dividido en métodos explícitos — `setManualSquelch()` para control manual y manejo separado para modos de squelch automático — aclarando la distinción entre umbrales establecidos por el usuario y squelch automático gestionado por el radio.

## Comportamiento del Control Deslizante de Paneo

El control deslizante de paneo en la pestaña Audio utiliza un relleno anclado al centro. Cuando el control está a la izquierda del centro, la ranura se rellena desde el control hasta el centro en color de acento; cuando el control está en el centro o a la derecha, el relleno no se muestra. Un pequeño punto de marca central siempre es visible en la ranura para que pueda ver la posición neutral de un vistazo.

## Sombra de Elevación de la Bandera VFO

La bandera VFO ahora tiene una sombra de elevación ligera renderizada por un widget dedicado `FlagShadow`. La sombra se mantiene separada del Panel VFO para que las repintadas de medidores en vivo (por ejemplo, actualizaciones del S-meter) no vuelvan a desenfocar toda la bandera a la velocidad de animación. El widget de sombra:
- Usa `WA_TransparentForMouseEvents` para no interceptar clics.
- Usa un algoritmo rápido de desenfoque de caja con búsquedas de alto rendimiento.
- Se adapta automáticamente a la relación de píxeles del dispositivo (DPR) para una renderización nítida en pantallas de alta densidad.
- Reconstruye la imagen de sombra solo cuando cambia la geometría de la bandera o la DPR, evitando uso innecesario de CPU.

## Abrir Configuración de AetherDSP desde la pestaña DSP del VFO

Abra el diálogo de Configuración de AetherDSP desde la pestaña DSP del Panel VFO para ajustar los parámetros avanzados de reducción de ruido para los algoritmos NR2, NR4, DFNR o MNR.

### Antes de comenzar

- Debe haber un slice activo y conectado a un radio.
- El Panel VFO debe estar abierto para el slice que desea configurar (haga clic en la bandera del marcador VFO en la pantalla del espectro).

### Pasos

1. En el Panel VFO, haga clic en la etiqueta de la pestaña **DSP** para mostrar los controles de reducción de ruido.
2. Haga clic en el botón **ADSP**.  
   El diálogo de Configuración de AetherDSP se abre como una ventana sin modo; puede permanecer abierta mientras continúa operando el radio.

Alternativamente, puede hacer clic derecho en cualquiera de los botones de alternancia NR2, NR4, MNR o DFNR en la pestaña DSP para abrir el diálogo de Configuración de AetherDSP para ese algoritmo específico.

### Consejos

- El diálogo de Configuración de AetherDSP también puede abrirse desde `Settings > AetherDSP Settings...` en el menú principal.
- Hacer clic derecho en un botón de reducción de ruido (NR2, NR4, MNR o DFNR) abre el diálogo enfocado en los controles de ese algoritmo.

### Relacionado

- [Habilitar reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
- Bloqueo de frecuencia

## Accesibilidad de los Botones DSP

Los botones de reducción de ruido de la pestaña DSP ahora usan nombres de objeto estables (por ejemplo, `dspNR2Btn`, `dspDFNRBtn`) para automatización y scripting. Estos nombres son separados de los nombres accesibles utilizados por los lectores de pantalla y se garantiza que no cambien con la reformulación del texto de la interfaz. Esto asegura que los scripts de automatización puedan dirigirse de forma fiable a las alternancias DSP.

## Clic Derecho en Modo Colapsado

Cuando el Panel VFO está colapsado a la franja compacta de solo frecuencia, hacer clic derecho en la etiqueta de frecuencia abre el menú contextual del slice usando la frecuencia real del VFO en lugar de la frecuencia del cursor ajustada al paso. Esto asegura que los informes de spots y otras acciones dependientes de la frecuencia usen la frecuencia sintonizada correcta.
