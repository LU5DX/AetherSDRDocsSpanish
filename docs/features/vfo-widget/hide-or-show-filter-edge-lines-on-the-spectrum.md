# Panel de VFO

El panel de VFO es un panel de control flotante por segmento anclado al marcador de VFO en la pantalla del espectro. Proporciona acceso rápido a las configuraciones más utilizadas por segmento — modo, preselecciones de filtro, selección de antena, ganancia de AF, paneo, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación de DAX — sin salir de la vista del espectro. El panel se contrae a una tira compacta que solo muestra la frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El segmento que desea ajustar debe tener un marcador de VFO visible en la pantalla del espectro.

## Abrir el panel de VFO

Haga clic en la bandera del marcador de VFO en la pantalla del espectro para el segmento deseado. El panel de VFO se abre anclado al marcador.

## Ocultar o mostrar las líneas de borde del filtro en el espectro

1. Haga clic en la bandera del marcador de VFO en la pantalla del espectro para el segmento deseado. El panel de VFO se abre anclado al marcador.
2. Localice el **botón de bordes de filtro** en el panel de VFO.
3. Haga clic en el **botón de bordes de filtro** para alternar la ocultación de las líneas de borde del filtro. Vuelva a hacer clic para restaurarlas.

El estado se guarda inmediatamente. Cuando reinicie AetherSDR, la configuración se restaurará al estado en que la dejó para ese segmento.

## Qué hace cada control

| Control | Valor predeterminado | Configuración persistente | Comportamiento |
|---------|---------------------|---------------------------|----------------|
| **Botón de antena RX** | — | No persistente | Abre el menú de selección de antena para la antena receptora de este segmento. |
| **Botón de antena TX** | — | No persistente | Abre el menú de selección de antena para la antena transmisora de este segmento. |
| **Pantalla de frecuencia** | — | No persistente | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| **Etiqueta de ancho de filtro** | — | No persistente | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Modo. Utiliza `RxApplet::formatFilterWidth` como fuente única de información, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital. |
| **Deslizador de ganancia AF (pestaña Audio)** | 100 | No persistente — refleja el estado en vivo de la radio | Establece el nivel de salida de audio para este segmento. |
| **Deslizador de paneo (pestaña Audio)** | 50 | No persistente | Establece el paneo estéreo izquierdo/derecho para este segmento. 50 = centro. |
| **Botón de silencio (pestaña Audio)** | desactivado | No persistente | Silencia la salida de audio de este segmento sin cambiar la configuración de ganancia AF. |
| **Botón + deslizador de silenciador (pestaña Audio)** | desactivado | No persistente | Activa el silenciador para este segmento. El deslizador adyacente establece el umbral. |
| **Combo AGC (pestaña Audio)** | RÁPIDO | No persistente | Establece la velocidad de ataque/liberación del AGC para este segmento. |
| **Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP)** | desactivado | No persistente | Activa el algoritmo de reducción de ruido correspondiente para este segmento. La disponibilidad de los botones depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| **Botón ADSP (pestaña DSP)** | — | No persistente | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú Ajustes. Con estilo de un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| **Botón AetherVoice (pestaña DSP)** | — | No persistente | Alterna la tira de canal de audio Aetherial, el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |
| **Combo Modo (pestaña Modo)** | USB | No persistente | Establece el modo de demodulación para este segmento. |
| **Botones de preselección de filtro (pestaña Modo)** | — | `FilterPresets` | Aplica una preselección de ancho de filtro guardada. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |
| **Botones + etiquetas RIT / XIT (pestaña X/RIT)** | desactivado | No persistente | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en incrementos de 10 Hz. |
| **Combo de canal DAX (pestaña DAX)** | Desactivado | No persistente | Asigna un canal de audio DAX a este segmento. |
| **Botón de grosor del marcador** | 1 px | `Slice{N}_MarkerWidth` | Alterna la línea del marcador de VFO entre Apagado, 1 px y 3 px. Se persiste por segmento. |
| **Botón de bordes de filtro** | Mostrado (bordes visibles) | `Slice{N}_FilterEdgesHidden` | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se persiste por segmento. |
| **Alternar contracción** | expandido | `SliceFlagCollapsed_{N}` | Contrae el panel de VFO a una tira compacta que solo muestra la frecuencia. Se persiste por segmento. |

`{N}` es el número de segmento. Cada segmento almacena su propio valor de forma independiente.

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| **Insignia TX** | TX (rojo), oculta | Se muestra cuando este segmento es el segmento de transmisión activo. |
| **Insignia SPLIT** | SPLIT (ámbar), oculta | Se muestra cuando TX está asignado a un segmento diferente al segmento receptor activo. |

## Consejos

- La configuración de bordes de filtro es por segmento. Ocultar los bordes de filtro en el segmento 0 no afecta al segmento 1 ni a ningún otro segmento.
- Si ha contraído el panel de VFO a la vista solo de frecuencia, expándalo primero haciendo clic en la tira contraída para acceder al **botón de bordes de filtro**.
- El panel de VFO utiliza un widget `TabStack` personalizado que informa solo la sugerencia de tamaño de la pestaña actual, evitando un espacio visual al cambiar entre pestañas de diferentes alturas.
- Las etiquetas de las pestañas en el panel de VFO están implementadas como `QPushButton`, lo que las hace navegables por teclado con Tab. Use Tab para mover el foco entre pestañas, luego presione Enter o Espacio para activar la pestaña seleccionada. Haga clic derecho en la pestaña del altavoz (primera pestaña) para alternar el silencio de audio directamente.
- La sintonización con la rueda del ratón respeta la configuración de inversión de la rueda del ratón de InteractionSettings. Active la configuración de inversión de la rueda del ratón en Preferencias para invertir la dirección de desplazamiento para la sintonización de frecuencia del VFO.
- La pantalla de frecuencia utiliza `FreqLineEdit` para la entrada directa de frecuencia, con una sugerencia que muestra "MHz (ej. 14.225)". La entrada directa de frecuencia se cancela cuando el segmento se bloquea. La sintonización con la rueda del ratón en un VFO bloqueado notifica al usuario que la sintonización está bloqueada. La pantalla de frecuencia muestra una superposición "BLOQUEADO" cuando el VFO del segmento está bloqueado.
- En bandas XVTR, los números enteros simples de 4 o más dígitos con el segmento en el rango de 100-999 MHz insertan automáticamente un decimal después del tercer dígito (ej., 1446 → 144.6). Por encima de 1000 MHz, los números enteros simples se tratan como el valor directo en MHz. Entrada de frecuencia máxima: 50000 MHz.
- El silenciador está desactivado para modos RTTY, además de los modos digital y CW. Esto evita que el silenciador bloquee señales FSK débiles enviadas a decodificadores externos a través de DAX.

## Historial de versiones

- En v0.9.8, la **etiqueta de ancho de filtro** ahora utiliza `RxApplet::formatFilterWidth` como fuente única de información para formatear el ancho de banda del filtro, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital.
- En v0.9.8, varios botones de reducción de ruido que estaban previamente en la pestaña DSP (NR2, RN2, BNR, NR4, MNR y DFNR) se han movido fuera del panel de VFO. Esos algoritmos ahora se activan desde el menú superpuesto del espectro y el applet AetherDSP.
- En v0.9.8, los botones de alternancia DSP (NB, NR, ANF, NRL, NRS, NRF, ANFL) ahora insertan y extraen automáticamente la pila de deslizadores de nivel DSP compartida cuando llegan cambios de estado desde la radio.
- En v26.5.1, el silenciador está desactivado para modos RTTY.
- En v26.5.2.1, los menús de antena RX y TX utilizan la lista de antenas por segmento reportada por la radio cuando está disponible. El menú de antena TX filtra los puertos de antena solo RX. La entrada máxima de frecuencia para bandas XVTR se incrementó a 50000 MHz.
- En v26.5.3, el panel de VFO utiliza un widget `TabStack` personalizado. La pantalla de frecuencia muestra la superposición "BLOQUEADO" cuando el VFO del segmento está bloqueado.
- En v26.6.1, los controles deslizantes utilizan tokens de color que reconocen el tema. El deslizador de paneo utiliza un relleno anclado al centro. El panel de VFO asignó su propio ámbito de contenedor de tematización (`spectrum/vfo`).
- En v26.6.3, las etiquetas de las pestañas se implementaron como `QPushButton` para la navegación por teclado. La sintonización con la rueda del ratón respeta la configuración de inversión de la rueda del ratón. La pantalla de frecuencia utiliza `FreqLineEdit`. Se mejoró el soporte de accesibilidad.
- En v26.7.4, la sombra del panel de VFO se renderiza mediante un widget `FlagShadow` dedicado, manteniendo la sombra separada de las repintadas en vivo del medidor para evitar volver a desenfocar toda la bandera a la velocidad de animación.

## Relacionados

- [Cambiar el grosor de la línea del marcador de VFO](change-the-vfo-marker-line-thickness.md)
- [Contraer el panel de VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel de VFO](overview.md)
