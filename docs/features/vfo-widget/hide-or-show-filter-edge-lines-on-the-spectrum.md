# Panel VFO

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por slice más utilizados — modo, presets de filtro, selección de antena, ganancia AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. El panel se colapsa a una franja compacta que solo muestra la frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El slice que desea ajustar debe tener un marcador VFO visible en la pantalla del espectro.

## Abrir el panel VFO

Haga clic en la etiqueta del marcador VFO en la pantalla del espectro para el slice objetivo. El panel VFO se abre anclado al marcador.

## Ocultar o mostrar las líneas de bordes de filtro en el espectro

1. Haga clic en la etiqueta del marcador VFO en la pantalla del espectro para el slice objetivo. El panel VFO se abre anclado al marcador.
2. Localice el **Filter edges button** en el panel VFO.
3. Haga clic en **Filter edges button** para alternar las líneas de bordes de filtro y ocultarlas. Haga clic nuevamente para restaurarlas.

El estado se guarda de inmediato. Cuando reabra AetherSDR, el ajuste se restaura al estado en que lo dejó para ese slice.

## Qué hace cada control

| Control | Predeterminado | Ajuste persistido | Comportamiento |
|---------|----------------|-------------------|----------------|
| **RX antenna button** | — | No persistido | Abre el menú de selección de antena para la antena receptora de este slice. |
| **TX antenna button** | — | No persistido | Abre el menú de selección de antena para la antena transmisora de este slice. |
| **Frequency display** | — | No persistido | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| **Filter width label** | — | No persistido | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de presets de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modos SSB/digitales. |
| **AF Gain slider (Audio tab)** | 100 | No persistido — refleja el estado en vivo de la radio | Establece el nivel de salida de audio para este slice. |
| **Pan slider (Audio tab)** | 50 | No persistido | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. |
| **Mute button (Audio tab)** | off | No persistido | Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. |
| **Squelch button + slider (Audio tab)** | off | No persistido | Activa el squelch para este slice. El control deslizante adyacente establece el umbral. |
| **AGC combo (Audio tab)** | FAST | No persistido | Establece la velocidad de ataque/liberación del AGC para este slice. |
| **Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF / MN (pestaña DSP)** | off | No persistido | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de la radio y de la compilación. El botón **MN** solo se muestra en radios que admiten filtrado de muesca manual. Haga clic derecho en NR2, NR4, MNR, DFNR o MN para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| **ADSP button (pestaña DSP)** | — | No persistido | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Con estilo similar a un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, eleva y enfoca el diálogo no modal de configuración de AetherDSP. |
| **AetherVoice button (pestaña DSP)** | — | No persistido | Alterna la Aetherial Audio Channel Strip — la suite DSP unificada de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |
| **Mode combo (pestaña Mode)** | USB | No persistido | Establece el modo de demodulación para este slice. |
| **Filter preset buttons (pestaña Mode)** | — | `FilterPresets` | Aplica un preset de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |
| **RIT / XIT buttons + labels (pestaña X/RIT)** | off | No persistido | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| **DAX channel combo (pestaña DAX)** | Off | No persistido | Asigna un canal de audio DAX a este slice. |
| **Marker thickness button** | 1 px | `Slice{N}_MarkerWidth` | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se persiste por slice. |
| **Filter edges button** | Mostrado (bordes visibles) | `Slice{N}_FilterEdgesHidden` | Alterna las líneas de bordes de filtro en la banda pasante del espectro. Se persiste por slice. |
| **Collapse toggle** | expandido | `SliceFlagCollapsed_{N}` | Colapsa el panel VFO a una franja compacta que solo muestra la frecuencia. Se persiste por slice. |

`{N}` es el número del slice. Cada slice almacena su propio valor de forma independiente.

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| **TX badge** | TX (rojo), oculto | Se muestra cuando este slice es el slice de transmisión activo. |
| **SPLIT badge** | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente del slice de recepción activo. |

## Consejos

- El ajuste de bordes de filtro es por slice. Ocultar los bordes de filtro en el slice 0 no afecta al slice 1 ni a ningún otro slice.
- Si ha colapsado el panel VFO a la vista solo de frecuencia, expándalo primero haciendo clic en la franja colapsada para acceder al **Filter edges button**.
- El panel VFO usa un widget `TabStack` personalizado que informa solo la sugerencia de tamaño de la pestaña actual, evitando una brecha visual al cambiar entre pestañas de diferentes alturas.
- Las etiquetas de pestañas en el panel VFO se implementan como `QPushButton`, lo que las hace navegables por teclado con Tab. Use Tab para mover el foco entre pestañas y luego presione Enter o Espacio para activar la pestaña seleccionada. Haga clic derecho en la pestaña del altavoz (primera pestaña) para alternar el silencio de audio directamente.
- La sintonización con la rueda del ratón respeta el ajuste de inversión de la rueda del ratón de InteractionSettings. Active el ajuste de inversión de la rueda del ratón en Preferences para invertir la dirección del desplazamiento en la sintonización de frecuencia VFO.
- La pantalla de frecuencia usa `FreqLineEdit` para la entrada directa de frecuencia, con una sugerencia que muestra "MHz (p. ej. 14.225)". La entrada directa de frecuencia se cancela cuando el slice se bloquea. La sintonización con la rueda del ratón en un VFO bloqueado notifica al usuario que la sintonización está bloqueada. La pantalla de frecuencia muestra una superposición **LOCKED** cuando el VFO del slice está bloqueado.
- En bandas XVTR, los números enteros simples de 4 o más dígitos con el slice en el rango de 100-999 MHz insertan automáticamente un decimal después del tercer dígito (p. ej., 1446 → 144.6). Por encima de 1000 MHz, los números enteros simples se tratan como el valor directo en MHz. Entrada de frecuencia máxima: 50000 MHz.
- El squelch se desactiva para modos RTTY además de los modos digitales y CW. Esto evita que el squelch bloquee señales FSK débiles enviadas a decodificadores externos a través de DAX.
- Haga clic derecho en la franja de frecuencia colapsada para añadir un spot DX para la frecuencia VFO del slice. El spot se añade en la frecuencia real del VFO, no en la frecuencia ajustada por pasos del cursor.
- El botón DSP **MN** (muesca manual) aparece solo cuando la radio conectada informa soporte de muesca manual. En radios sin esta capacidad, el botón está oculto.

## Historial de versiones

- En v0.9.8, el **Filter width label** ahora usa `RxApplet::formatFilterWidth` como única fuente de verdad para formatear el ancho de banda del filtro, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modos SSB/digitales.
- En v0.9.8, varios botones de reducción de ruido que estaban anteriormente en la pestaña DSP (NR2, RN2, BNR, NR4, MNR y DFNR) se han movido fuera del panel VFO. Esos algoritmos ahora se alternan desde el menú superpuesto del espectro y el applet AetherDSP.
- En v0.9.8, los botones de alternancia DSP (NB, NR, ANF, NRL, NRS, NRF, ANFL) ahora empujan y extraen automáticamente la pila compartida de controles deslizantes de nivel DSP cuando llegan cambios de estado desde la radio.
- En v26.5.1, el squelch se desactiva para modos RTTY.
- En v26.5.2.1, los menús de antena RX y TX usan la lista de antenas por slice informada por la radio cuando está disponible. El menú de antena TX filtra los puertos de antena solo de RX. El máximo de entrada de frecuencia para bandas XVTR se aumentó a 50000 MHz.
- En v26.5.3, el panel VFO usa un widget `TabStack` personalizado. La pantalla de frecuencia muestra la superposición "LOCKED" cuando el VFO del slice está bloqueado.
- En v26.6.1, los controles deslizantes usan tokens de color conscientes del tema. El control deslizante de paneo usa un relleno anclado al centro. El panel VFO asignó su propio ámbito de contenedor de tematización (`spectrum/vfo`).
- En v26.6.3, las etiquetas de pestañas se implementaron como `QPushButton` para navegación por teclado. La sintonización con la rueda del ratón respeta el ajuste de inversión de la rueda del ratón. La pantalla de frecuencia usa `FreqLineEdit`. Se mejoró el soporte de accesibilidad.
- En v26.7.4, la sombra del panel VFO se renderiza con un widget `FlagShadow` dedicado, manteniendo la sombra separada de las repeticiones de los medidores en vivo para evitar volver a desenfocar toda la etiqueta a la velocidad de animación.
- En v26.8.4, se añadió el botón de alternancia DSP **MN** (muesca manual) a la pestaña DSP, que se muestra solo en radios que admiten filtrado de muesca manual. Cada botón de alternancia DSP ahora tiene un nombre de objeto estable para compatibilidad con el puente de automatización. Hacer clic derecho en la franja de frecuencia colapsada añade un spot DX para la frecuencia VFO del slice, usando la frecuencia real del VFO en lugar de la frecuencia ajustada por pasos del cursor.

## Relacionado

- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
- [VFO Panel overview](overview.md)
