# Panel VFO

El Panel VFO es un panel de control flotante por rebanada anclado al marcador VFO en la visualización del espectro. Proporciona acceso rápido a los ajustes por rebanada más utilizados — modo, preajustes de filtro, selección de antena, ganancia de AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. El panel puede colapsarse a una tira compacta solo de frecuencia.

## Abrir el Panel VFO

1. En la visualización del espectro, haga clic en la bandera del marcador VFO (el pequeño triángulo o bandera en la parte superior de la línea del marcador VFO).
2. El Panel VFO se abre como una ventana flotante anclada al marcador.

## Controles

El Panel VFO está organizado en pestañas: Audio, DSP, Mode, X/RIT y DAX.

### Controles comunes (siempre visibles)

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón antena RX | Botón pulsador | Abre el menú de selección de antena para la antena receptora de esta rebanada. |
| Botón antena TX | Botón pulsador | Abre el menú de selección de antena para la antena transmisora de esta rebanada. |
| Indicador de frecuencia | Indicador | Muestra la frecuencia actual de la rebanada. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | Indicador | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza un método de formato coherente para garantizar lecturas precisas. |
| Insignia TX | Indicador | Se muestra (en rojo) cuando esta rebanada es la rebanada de transmisión activa. Oculto en caso contrario. |
| Insignia SPLIT | Indicador | Se muestra (en ámbar) cuando la TX está asignada a una rebanada diferente a la rebanada receptora activa. Oculto en caso contrario. |
| Botón de grosor del marcador | Botón pulsador | Recorre la línea del marcador VFO entre Apagado, 1 px y 3 px. El ajuste se conserva por rebanada. |
| Botón de bordes de filtro | Botón de conmutación | Activa o desactiva las líneas de borde del filtro en la banda pasante del espectro. El ajuste se conserva por rebanada. Valor predeterminado: mostrado. |
| Conmutador de colapso | Botón de conmutación | Colapsa el panel VFO a una tira compacta solo de frecuencia. El ajuste se conserva por rebanada. Valor predeterminado: expandido. |

### Pestaña Audio

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Deslizador de ganancia AF | Deslizador | 0-100 | Ajusta el nivel de salida de audio para esta rebanada. Valor predeterminado: 100. No se conserva — refleja el estado en vivo de la radio. |
| Deslizador de paneo | Deslizador | 0-100 | Ajusta el paneo estéreo izquierdo/derecho para esta rebanada. 50 = centro. Valor predeterminado: 50. |
| Botón de silencio | Botón de conmutación | Act/Des | Silencia la salida de audio para esta rebanada sin cambiar el ajuste de ganancia AF. Valor predeterminado: desactivado. |
| Botón + deslizador de squelch | Botón de conmutación + deslizador | 0-100 | Activa el squelch para esta rebanada. El deslizador adjunto ajusta el umbral. Valor predeterminado: desactivado. El squelch se desactiva automáticamente en modos digital, RTTY y CW. |
| Cuadro combinado de AGC | Cuadro combinado | FAST, MED, SLOW, OFF | Ajusta la velocidad de ataque/liberación del AGC para esta rebanada. Valor predeterminado: FAST. |

### Pestaña DSP

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | Botón de conmutación | Activa el algoritmo de reducción de ruido correspondiente para esta rebanada. La disponibilidad de botones depende de la serie de radio y la compilación. Valor predeterminado: desactivado. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| Botón ADSP | Botón pulsador | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Al hacer clic, abre y enfoca el diálogo de configuración de AetherDSP no modal. |
| Botón AetherVoice | Botón pulsador | Activa o desactiva la tira de canales de audio de Aetherial — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

### Pestaña Mode

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Cuadro combinado de modo | Cuadro combinado | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Ajusta el modo de demodulación para esta rebanada. Valor predeterminado: USB. |
| Botones de preajuste de filtro | Botón pulsador | N/A | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. |

### Pestaña X/RIT

| Control | Tipo | Descripción |
|---------|------|-------------|
| Botón + etiqueta RIT | Botón de conmutación + indicador | Activa la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. Valor predeterminado: desactivado. |
| Botón + etiqueta XIT | Botón de conmutación + indicador | Activa la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. Valor predeterminado: desactivado. |

### Pestaña DAX

| Control | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| Cuadro combinado de canal DAX | Cuadro combinado | Off, 1-8 | Asigna un canal de audio DAX a esta rebanada. Valor predeterminado: Off. |

## Comportamiento del Squelch

El squelch se desactiva automáticamente en modos digital, RTTY y CW:
- **Digital y RTTY**: El audio alimenta decodificadores externos a través de DAX; el squelch no es significativo y puede bloquear señales FSK débiles.
- **CW**: La radio bloquea el squelch en un nivel fijo y rechaza cambios desde el cliente.

Al cambiar a un modo donde el squelch está desactivado mientras el squelch está activo, el sistema guarda el estado del squelch y lo apaga. Al volver a un modo donde el squelch está permitido, se restaura el estado anterior del squelch.

## Abrir la Configuración de AetherDSP desde la pestaña DSP del VFO

Abra el diálogo de configuración de AetherDSP desde la pestaña DSP del Panel VFO para ajustar parámetros avanzados de reducción de ruido para los algoritmos NR2, NR4, DFNR o MNR.

### Antes de empezar

- Debe haber una rebanada activa y conectada a una radio.
- El Panel VFO debe estar abierto para la rebanada que desea configurar (haga clic en la bandera del marcador VFO en la visualización del espectro).

### Pasos

1. En el Panel VFO, haga clic en la etiqueta de la pestaña **DSP** para mostrar los controles de reducción de ruido.
2. Haga clic en el botón **ADSP**.  
   El diálogo de configuración de AetherDSP se abre como una ventana no modal; puede permanecer abierta mientras continúa operando la radio.

Alternativamente, puede hacer clic derecho en cualquiera de los botones de conmutación NR2, NR4, MNR o DFNR en la pestaña DSP para abrir el diálogo de configuración de AetherDSP para ese algoritmo específico.

### Consejos

- El diálogo de configuración de AetherDSP también se puede abrir desde `Settings > AetherDSP Settings...` en el menú principal.
- Hacer clic derecho en un botón de reducción de ruido (NR2, NR4, MNR o DFNR) abre el diálogo centrado en los controles de ese algoritmo.

### Relacionado

- [Activar la reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
