# Panel VFO

El Panel VFO es un panel de control flotante por slice, anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por slice más utilizados (modo, preajustes de filtro, selección de antena, ganancia de AF, panorámica, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX) sin salir de la vista del espectro. El panel puede contraerse a una tira compacta que solo muestra la frecuencia.

## Abrir el Panel VFO

1. En la pantalla del espectro, haga clic en la bandera del marcador VFO (el pequeño triángulo o bandera en la parte superior de la línea del marcador VFO).
2. El Panel VFO se abre como una ventana flotante anclada al marcador.

## Controles

El Panel VFO está organizado en pestañas: Audio, DSP, Mode, X/RIT y DAX.

### Controles comunes (siempre visibles)

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón de antena RX | Botón pulsador | Abre el menú de selección de antena para la antena receptora de este slice. Muestra la lista de antenas RX específicas del slice cuando está disponible; si no, recurre a la lista de antenas del radio. |
| Botón de antena TX | Botón pulsador | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de antena solo RX. Muestra la lista de antenas TX específicas del slice cuando está disponible; si no, recurre a la lista de antenas del radio. |
| Indicador de frecuencia | Indicador | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, la entrada de un número entero en el rango de 100-999 MHz inserta un decimal después del tercer dígito (ej: 1446 → 144.6). |
| Etiqueta de ancho de filtro | Indicador | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza un método de formato coherente para garantizar lecturas precisas. |
| Insignia TX | Indicador | Se muestra (rojo) cuando este slice es el slice transmisor activo. Oculto en caso contrario. |
| Insignia SPLIT | Indicador | Se muestra (ámbar) cuando TX está asignada a un slice diferente al slice receptor activo. Oculto en caso contrario. |
| Botón de grosor del marcador | Botón pulsador | Recorre la línea del marcador VFO entre Apagado, 1 px y 3 px. La configuración se conserva por slice. |
| Botón de bordes del filtro | Botón de alternancia | Alterna la visualización de las líneas de borde del filtro en la banda pasante del espectro. La configuración se conserva por slice. Valor predeterminado: mostrado. |
| Alternancia de contracción | Botón de alternancia | Contrae el panel VFO a una tira compacta que solo muestra la frecuencia. La configuración se conserva por slice. Valor predeterminado: expandido. |
| Insignia de slice | Indicador | Muestra la letra del slice en una insignia de color. Haga clic para abrir el menú contextual del slice. |

### Pestaña Audio

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Deslizador de ganancia AF | Deslizador | 0-100 | Establece el nivel de salida de audio para este slice. Valor predeterminado: 100. No se conserva: refleja el estado en vivo del radio. |
| Deslizador de panorámica | Deslizador | 0-100 | Establece la panorámica estéreo izquierda/derecha para este slice. 50 = centro. Valor predeterminado: 50. |
| Botón de silencio | Botón de alternancia | Activado/Desactivado | Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. Valor predeterminado: desactivado. |
| Botón + deslizador de silenciador | Botón de alternancia + deslizador | 0-100 | Activa el silenciador para este slice. El deslizador adyacente establece el umbral. Valor predeterminado: desactivado. El silenciador se desactiva automáticamente en modos digital, RTTY y CW. |
| Cuadro combinado AGC | Cuadro combinado | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este slice. Valor predeterminado: FAST. |

### Pestaña DSP

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | Botón de alternancia | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie del radio y la compilación. Valor predeterminado: desactivado. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| Botón ADSP | Botón pulsador | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú Settings. Al hacer clic, abre y enfoca el diálogo de configuración de AetherDSP no modal. |
| Botón AetherVoice | Botón pulsador | Alterna el Canal de Audio Aetherial (Aetherial Audio Channel Strip), el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

### Pestaña Mode

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Cuadro combinado de modo | Cuadro combinado | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este slice. Valor predeterminado: USB. |
| Botones de preajuste de filtro | Botón pulsador | N/A | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. |

### Pestaña X/RIT

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón + etiqueta RIT | Botón de alternancia + indicador | Activa la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. Valor predeterminado: desactivado. |
| Botón + etiqueta XIT | Botón de alternancia + indicador | Activa la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. Valor predeterminado: desactivado. |

### Pestaña DAX

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Cuadro combinado de canal DAX | Cuadro combinado | Off, 1-8 | Asigna un canal de audio DAX a este slice. Valor predeterminado: Off. |

## Comportamiento del silenciador

El silenciador se desactiva automáticamente en modos digital, RTTY y CW:
- **Digital y RTTY**: El audio alimenta decodificadores externos a través de DAX; el silenciador no tiene sentido y puede bloquear señales FSK débiles.
- **CW**: El radio bloquea el silenciador en un nivel fijo y rechaza los cambios del cliente.

Al cambiar a un modo donde el silenciador está desactivado mientras está activo, el sistema guarda el estado del silenciador y lo apaga. Al volver a un modo donde el silenciador está permitido, se restaura el estado anterior del silenciador.

## Abrir la configuración de AetherDSP desde la pestaña DSP del VFO

Abra el diálogo de configuración de AetherDSP desde la pestaña DSP del Panel VFO para ajustar parámetros avanzados de reducción de ruido para los algoritmos NR2, NR4, DFNR o MNR.

### Antes de comenzar

- Debe haber un slice activo y conectado a un radio.
- El Panel VFO debe estar abierto para el slice que desea configurar (haga clic en la bandera del marcador VFO en la pantalla del espectro).

### Pasos

1. En el Panel VFO, haga clic en la etiqueta de la pestaña **DSP** para mostrar los controles de reducción de ruido.
2. Haga clic en el botón **ADSP**.  
   Se abre el diálogo de configuración de AetherDSP como una ventana no modal; puede permanecer abierto mientras continúa operando el radio.

Alternativamente, puede hacer clic derecho en cualquiera de los botones de alternancia NR2, NR4, MNR o DFNR en la pestaña DSP para abrir el diálogo de configuración de AetherDSP para ese algoritmo específico.

### Consejos

- El diálogo de configuración de AetherDSP también se puede abrir desde `Settings > AetherDSP Settings...` en el menú principal.
- Hacer clic derecho en un botón de reducción de ruido (NR2, NR4, MNR o DFNR) abre el diálogo centrado en los controles de ese algoritmo.

### Relacionado

- [Habilitar la reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
