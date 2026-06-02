# Panel VFO

El Panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a las configuraciones más utilizadas por slice — modo, preselecciones de filtro, selección de antena, ganancia AF, paneo, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. El panel se puede colapsar a una tira compacta que solo muestra la frecuencia.

## Abrir el Panel VFO

1. En la pantalla del espectro, haga clic en la bandera del marcador VFO (el pequeño triángulo o bandera en la parte superior de la línea del marcador VFO).
2. El Panel VFO se abre como una ventana flotante anclada al marcador.

## Controles

El Panel VFO está organizado en pestañas: Audio, DSP, Modo, X/RIT y DAX.

### Controles Comunes (siempre visibles)

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón de antena RX | Botón pulsador | Abre el menú de selección de antena para la antena de recepción de este slice. Muestra la lista de antenas RX específica del slice cuando está disponible; recurre a la lista de antenas del radio en caso contrario. |
| Botón de antena TX | Botón pulsador | Abre el menú de selección de antena para la antena de transmisión de este slice. Filtra los puertos de antena solo RX. Muestra la lista de antenas TX específica del slice cuando está disponible; recurre a la lista de antenas del radio en caso contrario. |
| Indicador de frecuencia | Indicador | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. Cuando el slice está bloqueado, muestra una superposición "LOCKED" e impide la entrada directa de frecuencia. En bandas XVTR, la entrada de números enteros simples en el rango 100-999 MHz inserta un decimal después del tercer dígito (p. ej., 1446 → 144.6). |
| Etiqueta de ancho de filtro | Indicador | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Modo. Utiliza un método de formato coherente para garantizar lecturas precisas. |
| Insignia TX | Indicador | Se muestra (roja) cuando este slice es el slice de transmisión activo. Oculta en caso contrario. |
| Insignia SPLIT | Indicador | Se muestra (ámbar) cuando TX está asignado a un slice diferente al slice de recepción activo. Oculta en caso contrario. |
| Botón de grosor de marcador | Botón pulsador | Recorre la línea del marcador VFO entre Apagado, 1 px y 3 px. La configuración se conserva por slice. |
| Botón de bordes de filtro | Botón de alternancia | Alterna las líneas de borde del filtro en la banda de paso del espectro. La configuración se conserva por slice. Valor predeterminado: mostrado. |
| Alternancia de colapso | Botón de alternancia | Colapsa el panel VFO a una tira compacta que solo muestra la frecuencia. La configuración se conserva por slice. Valor predeterminado: expandido. |
| Insignia de slice | Indicador | Muestra la letra del slice en una insignia de color. Haga clic para abrir el menú contextual del slice. |

### Pestaña Audio

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Deslizador de ganancia AF | Deslizador | 0-100 | Establece el nivel de salida de audio para este slice. Valor predeterminado: 100. No se conserva — refleja el estado en vivo del radio. |
| Deslizador de paneo | Deslizador | 0-100 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. Valor predeterminado: 50. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central visible en la ranura. |
| Botón de silencio | Botón de alternancia | Activado/Desactivado | Silencia la salida de audio para este slice sin cambiar la configuración de ganancia AF. Valor predeterminado: desactivado. |
| Botón + deslizador de silenciador | Botón de alternancia + deslizador | 0-100 | Activa el silenciador para este slice. El deslizador adyacente establece el umbral. Valor predeterminado: desactivado. El silenciador se desactiva automáticamente en modos digital, RTTY y CW. |
| Cuadro combinado AGC | Cuadro combinado | RÁPIDO, MEDIO, LENTO, APAGADO | Establece la velocidad de ataque/liberación del AGC para este slice. Valor predeterminado: RÁPIDO. |

### Pestaña DSP

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | Botón de alternancia | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de radio y la compilación. Valor predeterminado: desactivado. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón ADSP | Botón pulsador | Abre el cuadro de diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Configuración. Al hacer clic, abre y enfoca el cuadro de diálogo de Configuración de AetherDSP no modal. |
| Botón AetherVoice | Botón pulsador | Alterna la Tira de Canal de Audio de Aetherial — el conjunto DSP unificado de TX/RX. Abarca 2 columnas en la cuadrícula DSP de 4 columnas. |

### Pestaña Modo

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Cuadro combinado de modo | Cuadro combinado | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este slice. Valor predeterminado: USB. |
| Botones de preselección de filtro | Botón pulsador | N/A | Aplica una preselección de ancho de filtro guardada. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón + etiqueta RIT | Botón de alternancia + indicador | Activa la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. Valor predeterminado: desactivado. |
| Botón + etiqueta XIT | Botón de alternancia + indicador | Activa la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. Valor predeterminado: desactivado. |

### Pestaña DAX

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Cuadro combinado de canal DAX | Cuadro combinado | Apagado, 1-8 | Asigna un canal de audio DAX a este slice. Valor predeterminado: Apagado. |

## Comportamiento de Entrada de Frecuencia

### Entrada Directa de Frecuencia

1. Haga clic en el indicador de frecuencia una vez. El indicador cambia a un campo editable que muestra la frecuencia actual.
2. Escriba la frecuencia deseada y presione Enter o Tab para aplicarla. El sistema analiza la entrada de manera flexible:
   - **Entrada en MHz**: Escriba un valor en MHz (p. ej., "14.225", "14.225.000", "14225", "14225.0"). Los puntos más allá del primero se eliminan automáticamente.
   - **Entrada en kHz**: En bandas HF, los números enteros simples mayores de 54000 se tratan como Hz; de lo contrario, se tratan como kHz. Por ejemplo, "14225" se convierte en 14.225 MHz (interpretación en kHz), mientras que "14225000" se convierte en 14.225 MHz (interpretación en Hz).
   - **Entrada en banda XVTR**: En bandas XVTR, se aceptan valores superiores a 54 MHz. Un número entero simple en el rango 100-999 inserta un decimal después del tercer dígito (p. ej., "1446" → 144.6 MHz).

### Entrada Explícita en MHz

Cuando escribe explícitamente un valor con decimal y supera los 54 MHz, el sistema lo trata como un valor en MHz en lugar de intentar la conversión Hz/kHz. Esto permite la entrada directa de frecuencias VHF/UHF/SHF en MHz sin ambigüedad.

### Comportamiento con Slice Bloqueado

Cuando un slice tiene la frecuencia bloqueada:
- El indicador de frecuencia muestra una superposición "LOCKED".
- Al hacer clic en el indicador de frecuencia no se inicia la entrada directa.
- La sintonización con la rueda de desplazamiento está bloqueada, incluso en modo colapsado.
- Una notificación audible indica que el intento de sintonización fue bloqueado.

## Comportamiento del Silenciador

El silenciador se desactiva automáticamente en modos digital, RTTY y CW:
- **Digital y RTTY**: El audio alimenta decodificadores externos a través de DAX; el silenciador no es significativo y puede bloquear señales FSK débiles.
- **CW**: El radio bloquea el silenciador en un nivel fijo y rechaza los cambios del cliente.

Al cambiar a un modo donde el silenciador está desactivado mientras está activo, el sistema guarda el estado del silenciador y lo apaga. Al volver a un modo donde el silenciador está permitido, se restaura el estado anterior del silenciador.

## Comportamiento del Deslizador de Paneo

El deslizador de paneo en la pestaña Audio utiliza un relleno anclado al centro. Cuando el control está a la izquierda del centro, la ranura se rellena desde el control hasta el centro en color de acento; cuando el control está en el centro o a la derecha, el relleno no se muestra. Un pequeño punto de marca central siempre es visible en la ranura para que pueda ver la posición neutral de un vistazo.

## Abrir Configuración de AetherDSP desde la Pestaña DSP del VFO

Abra el cuadro de diálogo de Configuración de AetherDSP desde la pestaña DSP del Panel VFO para ajustar parámetros avanzados de reducción de ruido para los algoritmos NR2, NR4, DFNR o MNR.

### Antes de comenzar

- Debe haber un slice activo y conectado a un radio.
- El Panel VFO debe estar abierto para el slice que desea configurar (haga clic en la bandera del marcador VFO en la pantalla del espectro).

### Pasos

1. En el Panel VFO, haga clic en la etiqueta de la pestaña **DSP** para mostrar los controles de reducción de ruido.
2. Haga clic en el botón **ADSP**.  
   Se abre el cuadro de diálogo de Configuración de AetherDSP como una ventana no modal; puede permanecer abierta mientras continúa operando el radio.

Alternativamente, puede hacer clic derecho en cualquiera de los botones de alternancia NR2, NR4, MNR o DFNR en la pestaña DSP para abrir el cuadro de diálogo de Configuración de AetherDSP para ese algoritmo específico.

### Consejos

- El cuadro de diálogo de Configuración de AetherDSP también se puede abrir desde `Settings > AetherDSP Settings...` en el menú principal.
- Al hacer clic derecho en un botón de reducción de ruido (NR2, NR4, MNR o DFNR) se abre el cuadro de diálogo enfocado en los controles de ese algoritmo.

### Relacionados

- [Habilitar la reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
- Bloqueo de frecuencia
