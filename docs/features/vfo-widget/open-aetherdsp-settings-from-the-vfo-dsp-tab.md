# Panel VFO

El Panel VFO es un panel de control flotante por segmento (slice) anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes más utilizados por segmento — modo, preajustes de filtro, selección de antena, ganancia de AF, paneo, silenciador (squelch), AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. El panel se puede contraer a una tira compacta que solo muestra la frecuencia.

## Abrir el Panel VFO

1. En la pantalla del espectro, haga clic en la bandera del marcador VFO (el pequeño triángulo o bandera en la parte superior de la línea del marcador VFO).
2. El Panel VFO se abre como una ventana flotante anclada al marcador.

## Controles

El Panel VFO está organizado en pestañas: Audio, DSP, Mode, X/RIT y DAX. Las etiquetas de las pestañas ahora se muestran como `QPushButton` para accesibilidad de teclado y un estilo de enfoque consistente. Haga clic derecho en la etiqueta de la pestaña **Audio** para silenciar directamente.

### Controles comunes (siempre visibles)

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón de antena RX | Botón | Abre el menú de selección de antena para la antena receptora de este segmento. Muestra la lista de antenas RX específica del segmento cuando está disponible; de lo contrario, utiliza la lista de antenas del radio. |
| Botón de antena TX | Botón | Abre el menú de selección de antena para la antena transmisora de este segmento. Filtra los puertos de antena solo RX. Muestra la lista de antenas TX específica del segmento cuando está disponible; de lo contrario, utiliza la lista de antenas del radio. |
| Indicador de frecuencia | Indicador | Muestra la frecuencia actual del segmento. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba los MHz y presione Enter o Tab. Cuando el segmento está bloqueado, muestra una superposición "BLOQUEADO" y evita la entrada directa de frecuencia. En bandas XVTR, la entrada de enteros simples en el rango de 100-999 MHz inserta un decimal después del tercer dígito (por ejemplo, 1446 → 144.6). Accesibilidad: el texto de frecuencia se anuncia mediante `QAccessibleValueChangeEvent` cuando cambia. |
| Etiqueta de ancho de filtro | Indicador | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como la única fuente fiable, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital. |
| Distintivo TX | Indicador | Se muestra (rojo) cuando este segmento es el segmento de transmisión activo. Oculto en caso contrario. |
| Distintivo SPLIT | Indicador | Se muestra (ámbar) cuando la TX está asignada a un segmento diferente al segmento receptor activo. Oculto en caso contrario. El texto del distintivo puede ser "SWAP" para indicar operación en división (split); al hacer clic se realiza un intercambio. Se ha aumentado la opacidad del distintivo para una mejor visibilidad. |
| Botón de grosor del marcador | Botón | Cambia el grosor de la línea del marcador VFO entre Apagado, 1 px y 3 px. El ajuste se conserva por segmento (`Slice{N}_MarkerWidth`). |
| Botón de bordes del filtro | Botón de conmutación | Alterna la visualización de las líneas de borde del filtro en la banda pasante del espectro. El ajuste se conserva por segmento (`Slice{N}_FilterEdgesHidden`). Valor predeterminado: mostrado. |
| Botón de contraer | Botón de conmutación | Contrae el panel VFO a una tira compacta que solo muestra la frecuencia. El ajuste se conserva por segmento (`SliceFlagCollapsed_{N}`). Valor predeterminado: expandido. |
| Distintivo del segmento | Indicador | Muestra la letra del segmento en un distintivo de color. Haga clic para abrir el menú contextual del segmento. |

### Pestaña Audio

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Deslizador de ganancia AF | Deslizador | 0-100 | Establece el nivel de salida de audio para este segmento. Valor predeterminado: 100. No se conserva — refleja el estado en vivo del radio. |
| Deslizador de paneo | Deslizador | 0-100 | Establece el paneo estéreo izquierda/derecha para este segmento. 50 = centro. Valor predeterminado: 50. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central visible en la ranura. |
| Botón de silencio | Botón de conmutación | On/Off | Silencia la salida de audio para este segmento sin cambiar el ajuste de ganancia AF. Valor predeterminado: apagado. También accesible mediante clic derecho en la etiqueta de la pestaña Audio. |
| Botón + deslizador de silenciador | Botón de conmutación + deslizador | 0-100 | Activa el silenciador para este segmento. El deslizador adyacente establece el umbral. Valor predeterminado: apagado. El silenciador se desactiva automáticamente en modos digital, RTTY y CW. |
| Combobox AGC | Combobox | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este segmento. Valor predeterminado: FAST. |

### Pestaña DSP

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | Botón de conmutación | Activa el algoritmo de reducción de ruido correspondiente para este segmento. La disponibilidad de los botones depende de la serie de radio y la compilación. Valor predeterminado: apagado. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón ADSP | Botón | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú Settings. Al hacer clic, abre y enfoca el diálogo de Configuración de AetherDSP no modal. No es marcable; tiene el estilo de un conmutador DSP del lado del radio. |
| Botón AetherVoice | Botón | Activa la Tira de Canal de Audio Aetherial (Aetherial Audio Channel Strip), la suite DSP unificada de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

### Pestaña Mode

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Combobox de modo | Combobox | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este segmento. Valor predeterminado: USB. |
| Botones de preajuste de filtro | Botón | N/A | Aplica un ancho de filtro preajustado guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón + etiqueta RIT | Botón de conmutación + indicador | Activa la sintonización incremental del receptor. La etiqueta muestra el desfase actual; la rueda del ratón ajusta en pasos de 10 Hz. Valor predeterminado: apagado. |
| Botón + etiqueta XIT | Botón de conmutación + indicador | Activa la sintonización incremental del transmisor. La etiqueta muestra el desfase actual; la rueda del ratón ajusta en pasos de 10 Hz. Valor predeterminado: apagado. |

### Pestaña DAX

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Combobox de canal DAX | Combobox | Off, 1-8 | Asigna un canal de audio DAX a este segmento. Valor predeterminado: Off. |

## Comportamiento de entrada de frecuencia

### Entrada directa de frecuencia

1. Haga clic una vez en la pantalla de frecuencia. La pantalla cambia a un campo editable que muestra la frecuencia actual.
2. Escriba la frecuencia deseada y presione Enter o Tab para aplicarla. El sistema analiza la entrada de manera flexible:
   - **Entrada en MHz**: Escriba un valor en MHz (por ejemplo, "14.225", "14.225.000", "14225", "14225.0"). Los puntos posteriores al primero se eliminan automáticamente.
   - **Entrada en kHz**: En bandas de HF, los enteros simples mayores a 54000 se tratan como Hz; de lo contrario, se tratan como kHz. Por ejemplo, "14225" se convierte en 14.225 MHz (interpretación en kHz), mientras que "14225000" se convierte en 14.225 MHz (interpretación en Hz).
   - **Entrada en banda XVTR**: En bandas XVTR, se aceptan valores superiores a 54 MHz. Un entero simple en el rango de 100-999 inserta un decimal después del tercer dígito (por ejemplo, "1446" → 144.6 MHz).

El campo de edición de frecuencia ahora utiliza `FreqLineEdit` con texto de sugerencia "MHz (e.g. 14.225)" en lugar de texto de marcador de posición.

### Entrada explícita en MHz

Cuando escribe explícitamente un valor con decimal y supera los 54 MHz, el sistema lo trata como un valor en MHz en lugar de intentar una conversión Hz/kHz. Esto permite la entrada directa de frecuencias de VHF/UHF/SHF en MHz sin ambigüedad.

### Comportamiento del segmento bloqueado

Cuando un segmento está bloqueado en frecuencia:
- La pantalla de frecuencia muestra una superposición "BLOQUEADO".
- Hacer clic en la pantalla de frecuencia no inicia la entrada directa.
- La sintonización con la rueda del ratón está bloqueada, incluso en modo contraído.
- Una notificación audible indica que el intento de sintonización fue bloqueado.

## Comportamiento de la rueda del ratón

La dirección de sintonización con la rueda del ratón respeta el ajuste **Reverse mouse wheel** en los ajustes de Interaction. Cuando está activado, la dirección de sintonización se invierte, y la dirección del zoom en el panadapter también se invierte. El ajuste `reverseMouseWheel()` se verifica en el `wheelEvent` del widget VFO.

## Comportamiento del silenciador

El silenciador se desactiva automáticamente en modos digital, RTTY y CW:
- **Digital y RTTY**: El audio alimenta decodificadores externos a través de DAX; el silenciador no tiene sentido y puede bloquear señales FSK débiles.
- **CW**: El radio bloquea el silenciador activado a un nivel fijo y rechaza los cambios del cliente.

Al cambiar a un modo donde el silenciador está desactivado mientras está activo, el sistema guarda el estado del silenciador y lo apaga. Al volver a un modo donde el silenciador está permitido, se restaura el estado anterior del silenciador.

## Comportamiento del deslizador de paneo

El deslizador de paneo en la pestaña Audio utiliza un relleno pintado anclado al centro. Cuando el controlador está a la izquierda del centro, la ranura se rellena desde el controlador hasta el centro en color de acento; cuando el controlador está en el centro o a la derecha, no se muestra el relleno. Un pequeño punto de marca central es siempre visible en la ranura para que pueda ver la posición neutral de un vistazo.

## Sombra de elevación de la bandera VFO

La bandera VFO ahora tiene una sombra de elevación ligera renderizada por un widget `FlagShadow` dedicado. La sombra se mantiene separada del Panel VFO para que las repintadas en vivo del medidor (por ejemplo, las actualizaciones del S-meter) no vuelvan a desenfocar toda la bandera a la velocidad de animación. El widget de sombra:
- Utiliza `WA_TransparentForMouseEvents` para no interceptar los clics.
- Utiliza un algoritmo rápido de desenfoque de caja (box-blur) con búsquedas de alto rendimiento.
- Se adapta automáticamente a la relación de píxeles del dispositivo (DPR) para una representación nítida en pantallas de alta resolución.
- Reconstruye la imagen de la sombra solo cuando cambia la geometría de la bandera o el DPR, evitando el uso innecesario de CPU.

## Abrir AetherDSP Settings desde la pestaña DSP del VFO

Abra el diálogo de Configuración de AetherDSP desde la pestaña DSP del Panel VFO para ajustar los parámetros avanzados de reducción de ruido para los algoritmos NR2, NR4, DFNR o MNR.

### Antes de comenzar

- Debe haber un segmento activo y conectado a un radio.
- El Panel VFO debe estar abierto para el segmento que desea configurar (haga clic en la bandera del marcador VFO en la pantalla del espectro).

### Pasos

1. En el Panel VFO, haga clic en la etiqueta de la pestaña **DSP** para mostrar los controles de reducción de ruido.
2. Haga clic en el botón **ADSP**.  
   El diálogo de Configuración de AetherDSP se abre como una ventana no modal; puede permanecer abierta mientras continúa operando el radio.

Alternativamente, puede hacer clic derecho en cualquiera de los botones de conmutación NR2, NR4, MNR o DFNR en la pestaña DSP para abrir el diálogo de Configuración de AetherDSP para ese algoritmo específico.

### Consejos

- El diálogo de Configuración de AetherDSP también se puede abrir desde `Settings > AetherDSP Settings...` en el menú principal.
- Hacer clic derecho en un botón de reducción de ruido (NR2, NR4, MNR o DFNR) abre el diálogo enfocado en los controles de ese algoritmo.

### Relacionados

- [Habilitar la reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
- Bloqueo de frecuencia
