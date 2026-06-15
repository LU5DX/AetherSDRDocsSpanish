# Panel VFO

El Panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por slice más utilizados — modo, preajustes de filtro, selección de antena, ganancia AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. El panel puede colapsarse a una tira compacta que solo muestra la frecuencia.

## Abrir el Panel VFO

1. En la pantalla del espectro, haga clic en la bandera del marcador VFO (el triángulo pequeño o bandera en la parte superior de la línea del marcador VFO).
2. El Panel VFO se abre como una ventana flotante anclada al marcador.

## Controles

El Panel VFO está organizado en pestañas: Audio, DSP, Mode, X/RIT y DAX. Las etiquetas de las pestañas se representan ahora como `QPushButton` para accesibilidad mediante teclado y estilo de enfoque coherente. Haga clic derecho en la etiqueta de la pestaña **Audio** para activar/desactivar el silencio directamente.

### Controles comunes (siempre visibles)

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón de antena RX | Push button | Abre el menú de selección de antena para la antena receptora de este slice. Muestra la lista de antenas RX específica del slice cuando está disponible; de lo contrario, utiliza la lista de antenas del radio. |
| Botón de antena TX | Push button | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de antena solo RX. Muestra la lista de antenas TX específica del slice cuando está disponible; de lo contrario, utiliza la lista de antenas del radio. |
| Indicador de frecuencia | Indicator | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. Cuando el slice está bloqueado, muestra una superposición "LOCKED" e impide la entrada directa de frecuencia. En bandas XVTR, la entrada de un número entero en el rango de 100-999 MHz inserta un decimal después del tercer dígito (ej., 1446 → 144.6). Accesibilidad: el texto de frecuencia se anuncia mediante `QAccessibleValueChangeEvent` cuando cambia. |
| Etiqueta de ancho de filtro | Indicator | Muestra el ancho de banda actual del filtro. Haga clic para alternar entre los botones de preajuste de filtro en la pestaña Mode. Utiliza un método de formato coherente para garantizar lecturas precisas. |
| Insignia TX | Indicator | Se muestra (en rojo) cuando este slice es el slice transmisor activo. Oculto en caso contrario. |
| Insignia SPLIT | Indicator | Se muestra (en ámbar) cuando la TX está asignada a un slice diferente al slice receptor activo. Oculto en caso contrario. El texto de la insignia puede ser "SWAP" para indicar operación en división; al hacer clic se realiza un intercambio. La opacidad de la insignia se ha incrementado para una mejor visibilidad. |
| Botón de grosor del marcador | Push button | Alterna la línea del marcador VFO entre Apagado, 1 px y 3 px. El ajuste se conserva por slice. |
| Botón de bordes del filtro | Toggle button | Alterna las líneas de borde del filtro en la banda pasante del espectro. El ajuste se conserva por slice. Valor predeterminado: mostrado. |
| Alternar colapso | Toggle button | Colapsa el panel VFO a una tira compacta que solo muestra la frecuencia. El ajuste se conserva por slice. Valor predeterminado: expandido. |
| Insignia del slice | Indicator | Muestra la letra del slice en una insignia de color. Haga clic para abrir el menú contextual del slice. |

### Pestaña Audio

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Deslizador de ganancia AF | Slider | 0-100 | Establece el nivel de salida de audio para este slice. Valor predeterminado: 100. No se conserva — refleja el estado en vivo del radio. |
| Deslizador de paneo | Slider | 0-100 | Establece el paneo estéreo izquierda/derecha para este slice. 50 = centro. Valor predeterminado: 50. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central visible en la ranura. |
| Botón de silencio | Toggle button | On/Off | Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. Valor predeterminado: apagado. También accesible mediante clic derecho en la etiqueta de la pestaña Audio. |
| Botón + deslizador de squelch | Toggle button + slider | 0-100 | Activa el squelch para este slice. El deslizador adyacente establece el umbral. Valor predeterminado: apagado. El squelch se desactiva automáticamente en modos digital, RTTY y CW. |
| Combinación AGC | Combo box | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este slice. Valor predeterminado: FAST. |

### Pestaña DSP

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | Toggle button | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie y compilación del radio. Valor predeterminado: apagado. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón ADSP | Push button | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Al hacer clic, eleva y enfoca el diálogo de Configuración de AetherDSP no modal. |
| Botón AetherVoice | Push button | Activa/desactiva la Tira de Canales de Audio Aetherial — el conjunto unificado de DSP TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

### Pestaña Mode

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Combinación de modo | Combo box | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este slice. Valor predeterminado: USB. |
| Botones de preajuste de filtro | Push button | N/A | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón + etiqueta RIT | Toggle button + indicator | Activa la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. Valor predeterminado: apagado. |
| Botón + etiqueta XIT | Toggle button + indicator | Activa la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. Valor predeterminado: apagado. |

### Pestaña DAX

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Combinación de canal DAX | Combo box | Off, 1-8 | Asigna un canal de audio DAX a este slice. Valor predeterminado: Off. |

## Comportamiento de Entrada de Frecuencia

### Entrada Directa de Frecuencia

1. Haga clic una vez en el indicador de frecuencia. El indicador cambia a un campo editable que muestra la frecuencia actual.
2. Escriba la frecuencia deseada y presione Enter o Tab para aplicarla. El sistema analiza la entrada de manera flexible:
   - **Entrada en MHz**: Escriba un valor en MHz (ej., "14.225", "14.225.000", "14225", "14225.0"). Los puntos más allá del primero se eliminan automáticamente.
   - **Entrada en kHz**: En bandas HF, los números enteros mayores de 54000 se tratan como Hz; de lo contrario, se tratan como kHz. Por ejemplo, "14225" se convierte en 14.225 MHz (interpretación en kHz), mientras que "14225000" se convierte en 14.225 MHz (interpretación en Hz).
   - **Entrada en banda XVTR**: En bandas XVTR, se aceptan valores superiores a 54 MHz. Un número entero en el rango de 100-999 inserta un decimal después del tercer dígito (ej., "1446" → 144.6 MHz).

El campo de edición de frecuencia ahora utiliza `FreqLineEdit` con texto de sugerencia "MHz (e.g. 14.225)" en lugar de texto de marcador de posición.

### Entrada Explícita en MHz

Cuando escribe explícitamente un valor con un decimal y supera los 54 MHz, el sistema lo trata como un valor en MHz en lugar de intentar una conversión a Hz/kHz. Esto permite la entrada directa de frecuencias VHF/UHF/SHF en MHz sin ambigüedad.

### Comportamiento del Slice Bloqueado

Cuando un slice está bloqueado en frecuencia:
- El indicador de frecuencia muestra una superposición "LOCKED".
- Hacer clic en el indicador de frecuencia no inicia la entrada directa.
- La sintonización con la rueda del ratón está bloqueada, incluso en modo colapsado.
- Una notificación audible indica que el intento de sintonización fue bloqueado.

## Comportamiento de la Rueda del Ratón

La dirección de sintonización con la rueda del ratón respeta el ajuste **Reverse mouse wheel** en los ajustes de Interaction. Cuando está activado, la dirección de sintonización se invierte, y la dirección del zoom en el panadapter también se invierte. El ajuste `reverseMouseWheel()` se verifica en el `wheelEvent` del widget VFO.

## Comportamiento del Squelch

El squelch se desactiva automáticamente en modos digital, RTTY y CW:
- **Digital y RTTY**: El audio se alimenta a decodificadores externos a través de DAX; el squelch no es significativo y puede bloquear señales FSK débiles.
- **CW**: El radio bloquea el squelch a un nivel fijo y rechaza los cambios desde el cliente.

Al cambiar a un modo donde el squelch está desactivado mientras el squelch está activo, el sistema guarda el estado del squelch y lo desactiva. Al volver a un modo donde el squelch está permitido, se restaura el estado anterior del squelch.

## Comportamiento del Deslizador de Paneo

El deslizador de paneo en la pestaña Audio utiliza un pintado de relleno anclado al centro. Cuando el control está a la izquierda del centro, la ranura se rellena desde el control hasta el centro en color de acento; cuando el control está en el centro o a la derecha, no se muestra el relleno. Un pequeño punto de marca central siempre es visible en la ranura para que pueda ver la posición neutra de un vistazo.

## Abrir Configuración de AetherDSP desde la Pestaña DSP del VFO

Abra el diálogo de Configuración de AetherDSP desde la pestaña DSP del Panel VFO para ajustar parámetros avanzados de reducción de ruido para los algoritmos NR2, NR4, DFNR o MNR.

### Antes de comenzar

- Debe haber un slice activo y conectado a un radio.
- El Panel VFO debe estar abierto para el slice que desea configurar (haga clic en la bandera del marcador VFO en la pantalla del espectro).

### Pasos

1. En el Panel VFO, haga clic en la etiqueta de la pestaña **DSP** para mostrar los controles de reducción de ruido.
2. Haga clic en el botón **ADSP**.  
   El diálogo de Configuración de AetherDSP se abre como una ventana no modal; puede permanecer abierta mientras continúa operando el radio.

Alternativamente, puede hacer clic derecho en cualquiera de los botones de alternancia NR2, NR4, MNR o DFNR en la pestaña DSP para abrir el diálogo de Configuración de AetherDSP para ese algoritmo específico.

### Consejos

- El diálogo de Configuración de AetherDSP también se puede abrir desde `Settings > AetherDSP Settings...` en el menú principal.
- Hacer clic derecho en un botón de reducción de ruido (NR2, NR4, MNR o DFNR) abre el diálogo enfocado en los controles de ese algoritmo.

### Relacionado

- [Activar la reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
- Bloqueo de frecuencia
