# Asignar un canal DAX desde el panel VFO

DAX (Digital Audio Exchange) enruta el audio recibido de un slice a un canal de audio con nombre en su computadora. Utilice este procedimiento para asignar o cambiar el canal DAX de cualquier slice directamente desde su panel VFO.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El puente de audio DAX debe estar en ejecución. Si no lo está, actívelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO del slice objetivo debe estar abierto y expandido. Si está colapsado a la franja de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO en la visualización del espectro para el slice que desea configurar. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **DAX** dentro del panel VFO.
3. Haga clic en el **combo de canal DAX** y seleccione un canal de la lista desplegable.
4. Para deshabilitar el enrutamiento DAX para este slice, seleccione **Off**.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Combo de canal DAX           | Off                                                                                                                                  | Off, 1–8                                                                                                                   |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un conmutador DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Abre la tira de canales de audio Aetherial: el conjunto unificado de DSP de TX/RX (v0.9.8).                                          | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

El combo de canal DAX asigna un canal de audio DAX al slice actual. Seleccionar un canal numerado enruta el audio recibido del slice a ese canal DAX. Seleccionar **Off** elimina la asignación. Esta configuración refleja el estado en vivo de la radio y no es persistida localmente por AetherSDR.

## Comportamiento del squelch por modo

El botón y el deslizador de squelch se deshabilitan automáticamente en modos donde el squelch no es significativo o no es compatible. A partir de v26.5.1:

- **El squelch está deshabilitado** en modos **Digital**, **RTTY** y **CW**.
  - **Digital / RTTY**: El audio alimenta decodificadores externos a través de DAX; el squelch no es significativo y puede bloquear señales FSK débiles (problema #2504).
  - **CW**: La radio bloquea el squelch activado a un nivel fijo y rechaza los cambios.
- Si el squelch estaba activado al cambiar a uno de estos modos, la radio lo apaga automáticamente. El estado guardado del squelch se conserva y se restaurará si vuelve a un modo compatible.

## Controles de la pestaña DSP

La pestaña DSP en el panel VFO contiene botones de reducción de ruido proporcionados por la radio y dos botones lanzadores del lado del cliente.

### Botones DSP del lado de la radio

Los siguientes botones DSP del lado de la radio aparecen en la cuadrícula de la pestaña DSP:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido impulsivo |
| ANF | Filtro de muesca automático |
| APF | Filtro de énfasis de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botones lanzadores del lado del cliente

Dos botones lanzadores del lado del cliente aparecen al final de la cuadrícula DSP:

| Botón | Comportamiento |
|---|---|
| **ADSP** | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Estilizado como un conmutador DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| **AetherVoice** | Activa/desactiva la tira de canales de audio Aetherial: el conjunto unificado de DSP de TX/RX. Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

### Conmutadores de reducción de ruido del lado del cliente

Los siguientes botones de reducción de ruido del lado del cliente aparecen en la pestaña DSP cuando están habilitados por la serie de radio y la compilación:

| Botón | Algoritmo |
|---|---|
| NR2 | Algoritmo de reducción de ruido del lado del cliente 2 |
| NR4 | Algoritmo de reducción de ruido del lado del cliente 4 |
| RN2 | Algoritmo de reducción de ruido del lado del cliente RN2 |
| MNR | Algoritmo de reducción de ruido del lado del cliente MNR |
| DFNR | Algoritmo de reducción de ruido del lado del cliente DFNR |
| BNR | Algoritmo de reducción de ruido del lado del cliente BNR |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo.

### Deslizador de nivel DSP

Una fila de deslizador de nivel compartida aparece debajo de la cuadrícula de botones. El deslizador ajusta la intensidad del botón DSP con nivel que se encendió más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El rango del deslizador es 0-100. Cuando ningún DSP con nivel está activo, o cuando solo RNN, ANFT o APF está encendido, la fila del deslizador está atenuada y no responde a la entrada. La fila permanece en su lugar en todo momento; no desplaza la cuadrícula de botones cuando cambia su objetivo.

Algoritmos que admiten el deslizador de nivel: NR, NB, ANF, NRL, NRS, NRF, ANFL.

A partir de v0.9.8, cuando un algoritmo DSP con nivel se habilita desde el perfil guardado de la radio al inicio, el deslizador de nivel se completa automáticamente sin necesidad de una activación manual.

### Etiqueta de ancho de filtro

La etiqueta de ancho de filtro muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. A partir de v0.9.8, esta etiqueta utiliza `RxApplet::formatFilterWidth` como la única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas de modo SSB/digital.

### Menús de antena RX y TX

El **botón de antena RX** abre un menú para seleccionar la antena receptora para este slice. El **botón de antena TX** abre un menú para seleccionar la antena transmisora. A partir de v26.5.2, estos menús utilizan la lista de antenas proporcionada por la radio del slice cuando está disponible, recurriendo a la lista de antenas global. Las opciones de antena TX excluyen automáticamente los puertos de antena solo RX. Cada elemento del menú muestra su nombre de antena original como información sobre herramienta.

### Controles del marcador

El **botón de grosor del marcador** recorre la línea del marcador VFO entre Off, 1 px y 3 px. La configuración se persiste por slice como `Slice{N}_MarkerWidth`.

El **botón de bordes del filtro** activa/desactiva las líneas del borde del filtro en la banda pasante del espectro. La configuración se persiste por slice como `Slice{N}_FilterEdgesHidden`.

### Conmutador de colapso

El **conmutador de colapso** colapsa el panel VFO a una franja compacta de solo frecuencia. La configuración se persiste por slice como `SliceFlagCollapsed_{N}`.

### Insignia del slice

La insignia del slice muestra la letra del slice. A partir de v26.5.2, la insignia admite formato de texto enriquecido, lo que permite caracteres especiales (problema #2606).

### Entrada de frecuencia

Haga clic en la visualización de frecuencia para comenzar la entrada directa de frecuencia. Escriba la frecuencia en MHz y presione Enter o Tab. A partir de v26.5.2, en bandas XVTR el rango de frecuencia se extiende a 50000.0 MHz. Para bandas de 2m/70cm (rango de 100-999 MHz), un número entero simple como 1446 se interpreta automáticamente como 144.6 MHz insertando un decimal después del tercer dígito. Para bandas de 23cm y microondas, un número entero simple representa MHz directamente.

A partir de v26.5.3, el análisis de entrada de frecuencia se mejora con un manejo consciente del contexto. Cuando ingresa explícitamente una frecuencia superior a 54 MHz (por ejemplo, escribiendo "144.225"), el analizador la trata correctamente como MHz incluso sin un slice XVTR, lo que permite la entrada directa de VHF/UHF. La función `FrequencyEntryParser::normalizedMhzText` normaliza formatos de entrada como "14.225.000" eliminando puntos adicionales. La función `FrequencyEntryParser::isExplicitMhzEntry` detecta cuando ha escrito un valor de MHz explícitamente. En bandas XVTR, la convención de banda de 3 dígitos (número entero simple como 1446 = 144.6 MHz) continúa funcionando.

Si intenta una entrada de frecuencia directa mientras el VFO está bloqueado, la entrada se cancela y se muestra la superposición BLOQUEADO en lugar de aceptar la nueva frecuencia (problema #2983). La visualización de frecuencia también indica cuando la sintonía está bloqueada por el bloqueo. La sintonía con la rueda del ratón en un VFO bloqueado desencadena la misma retroalimentación: el modelo de slice notifica `tuneBlockedByLock`, lo que cancela cualquier entrada de frecuencia en curso y vuelve a pintar el indicador BLOQUEADO.

### Mejoras en la entrada de frecuencia (v26.6.3)

A partir de v26.6.3, el campo de entrada de frecuencia utiliza un widget `FreqLineEdit` personalizado con texto de sugerencia mejorado. El texto de sugerencia dice "MHz (e.g. 14.225)". La visualización de frecuencia también proporciona anuncios de accesibilidad cuando la frecuencia cambia, lo que garantiza la compatibilidad con lectores de pantalla.

### Comportamiento del bloqueo VFO

El **botón Lock VFO** activa/desactiva el estado de bloqueo del VFO. Cuando está bloqueado:
- La sintonía con la rueda del ratón está bloqueada: el modelo de slice muestra retroalimentación a través de `tuneBlockedByLock`.
- La entrada de frecuencia directa se cancela al intentar comenzar o durante una entrada activa.
- La visualización de frecuencia muestra una superposición BLOQUEADO (símbolo 🔒) en lugar del valor de frecuencia durante los intentos de entrada directa.

Desbloquear limpia la superposición BLOQUEADO de forma centralizada en el SliceModel (problema #2983).

### Mejora en el diseño de pestañas

A partir de v26.5.3, la pila de pestañas del panel VFO utiliza un widget `TabStack` personalizado que informa solo el tamaño preferido de la pestaña actual. Esto corrige un espacio visual dentro de la pestaña Mode cuando la pestaña DSP es más alta (debido a que el digContainer es visible en los modos DIGU/DIGL). El contenido de la pestaña ya no asigna altura en exceso del máximo de todas las páginas.

### Mejoras en la navegación por pestañas (v26.6.3)

A partir de v26.6.3, las pestañas del panel VFO se implementan como widgets `QPushButton` en lugar de widgets `QLabel`. Este cambio proporciona soporte adecuado para el enfoque del teclado:

- Cada botón de pestaña es enfocable mediante la tecla Tab (política `Qt::TabFocus`).
- Las pestañas enfocadas muestran un contorno sutil en el borde inferior utilizando el color de la etiqueta de la pestaña.
- **Haga clic derecho en la pestaña de altavoz (primera pestaña)** para activar/desactivar el estado de silencio de audio directamente: un acceso directo conveniente para silenciar el slice sin abrir la pestaña Audio.

Los botones de pestaña utilizan un estilo plano y seleccionable con la misma apariencia visual que antes. La pestaña activa se estiliza con el color de acento (#00b4d8) y un borde inferior.

### Comportamiento del bloqueo VFO con la rueda del ratón (v26.6.3)

A partir de v26.6.3, la dirección de la rueda del ratón en el panel VFO respeta la configuración de **Reverse mouse wheel**. Si ha habilitado la rueda del ratón inversa en `Settings > Audio/Radio > Tuning`, al desplazar la rueda del ratón en el panel VFO se sintonizará en la dirección opuesta. Esta configuración se verifica a través del modelo `InteractionSettings` y se aplica a todos los eventos de rueda del panel VFO.

### Accesibilidad de la rueda del ratón (v26.6.3)

A partir de v26.6.3, el comportamiento de la rueda del ratón está completamente integrado con la configuración de `InteractionSettings`. Si invierte la rueda del ratón en la configuración, la dirección de desplazamiento del panel VFO se invierte en consecuencia. Esto se aplica a todos los eventos de rueda en el panel VFO, incluida el área de visualización de frecuencia y las etiquetas de compensación RIT/XIT.

### Mejoras de accesibilidad (v26.6.3)

A partir de v26.6.3, el panel VFO proporciona anuncios de accesibilidad para los cambios de frecuencia. Cuando la frecuencia cambia mientras un cliente de accesibilidad (lector de pantalla) está activo, se publica un evento `QAccessibleValueChangeEvent` para el widget de la etiqueta de frecuencia. Esto garantiza que los lectores de pantalla anuncien el nuevo valor de frecuencia. El temporizador de accesibilidad es de un solo disparo y se activa después de un breve retraso para evitar inundar la capa de accesibilidad durante la sintonía rápida.

### Tematización de deslizadores (v26.6.1)

A partir de v26.6.1, el panel VFO utiliza un estilo de deslizador temático en todas partes. El deslizador Pan se pinta con relleno anclado al centro: la sección de la ranura desde el control deslizante hasta el punto medio se rellena con el color de acento, mientras que el lado opuesto utiliza el color de fondo. Esto hace que la posición central (neutra) sea inmediatamente visible. El control deslizante se dibuja mediante el estilo Qt predeterminado.

Todos los demás deslizadores (AF Gain, umbral de squelch, nivel DSP) siguen las mismas reglas de
