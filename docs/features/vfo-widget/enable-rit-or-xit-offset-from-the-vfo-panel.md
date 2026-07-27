# Habilitar el desplazamiento RIT o XIT desde el panel VFO

RIT (Receiver Incremental Tuning) y XIT (Transmitter Incremental Tuning) le permiten desplazar la frecuencia de recepción o transmisión en un pequeño valor de compensación sin mover el VFO principal. Esto es útil para contactos en frecuencias divididas o para compensar una estación que está ligeramente fuera de su frecuencia de sintonía.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO para el segmento objetivo debe estar abierto y expandido. Si está contraído a la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en el marcador VFO en la pantalla del espectro para el segmento que desea ajustar. El panel VFO aparece anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el desplazamiento del receptor, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el desplazamiento RIT actual.
4. Para habilitar el desplazamiento del transmisor, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el desplazamiento XIT actual.
5. Con RIT o XIT activos, coloque el puntero del ratón sobre el botón correspondiente y gire la rueda del ratón para ajustar el desplazamiento. Cada paso de desplazamiento cambia el desplazamiento en 10 Hz.
6. Para deshabilitar RIT o XIT, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control                              | Tipo              | Predeterminado | Notas                                                                 |
|--------------------------------------|-------------------|----------------|-----------------------------------------------------------------------|
| Botón de antena RX                   | Botón pulsador    |                | Abre el menú de selección de antena para la antena de recepción de este segmento. |
| Botón de antena TX                   | Botón pulsador    |                | Abre el menú de selección de antena para la antena de transmisión de este segmento. |
| Indicador de frecuencia              | Indicador         |                | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro          | Indicador         |                | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza RxApplet::formatFilterWidth como fuente única de verdad. |
| Control deslizante de ganancia AF (pestaña Audio) | Control deslizante | 100      | Establece el nivel de salida de audio para este segmento. No se conserva: refleja el estado en vivo de la radio. |
| Control deslizante de paneo (pestaña Audio) | Control deslizante | 50         | Establece el paneo estéreo izquierdo/derecho para este segmento. 50 = centro. |
| Botón de silencio (pestaña Audio)    | Botón de alternancia | desactivado | Silencia la salida de audio para este segmento sin cambiar la configuración de ganancia AF. |
| Botón + control deslizante de squelch (pestaña Audio) | Botón de alternancia | desactivado | Habilita el squelch para este segmento. El control deslizante adyacente establece el umbral. |
| Combo AGC (pestaña Audio)            | Cuadro combinado   | RÁPIDO      | Establece la velocidad de ataque/liberación del AGC para este segmento. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia | desactivado | Habilita el algoritmo de reducción de ruido correspondiente para este segmento. La disponibilidad de botones depende de la serie de radio y la compilación. |
| Botón ADSP (pestaña DSP)             | Botón pulsador    |                | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). |
| Botón AetherVoice (pestaña DSP)      | Botón pulsador    |                | Alterna la tira de canales de audio Aetherial, el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |
| Combo Mode (pestaña Mode)            | Cuadro combinado   | USB           | Establece el modo de demodulación para este segmento. |
| Botones de preajuste de filtro (pestaña Mode) | Botón pulsador    |                | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Botón de alternancia | desactivado | Habilita la sintonía incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX)     | Cuadro combinado   | Desactivado   | Asigna un canal de audio DAX a este segmento. |
| Botón de grosor del marcador         | Botón pulsador    | 1 px         | Cambia la línea del marcador VFO entre Desactivado, 1 px y 3 px. Se conserva por segmento. |
| Botón de bordes del filtro           | Botón de alternancia | mostrado     | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se conserva por segmento. |
| Alternancia de contracción           | Botón de alternancia | expandido    | Contrae el panel VFO a una tira compacta de solo frecuencia. Se conserva por segmento. |
| Distintivo TX                        | Indicador         |                | Muestra TX (rojo) cuando este segmento es el segmento de transmisión activo. Oculto en caso contrario. |
| Distintivo SPLIT                     | Indicador         |                | Muestra SPLIT (ámbar) cuando TX está asignado a un segmento diferente al segmento de recepción activo. Oculto en caso contrario. |

**Botón de antena RX** — Abre un menú de selección de antena para la antena de recepción de este segmento. El menú ahora utiliza la propiedad `rxAntennaList()` por segmento cuando está disponible, recurriendo a la lista de antenas global. Los elementos del menú muestran una etiqueta legible junto al identificador interno de la antena.

**Botón de antena TX** — Abre un menú de selección de antena para la antena de transmisión de este segmento. El menú filtra los puertos de antena de solo RX. Utiliza el helper `txAntennaOptions()` para determinar las antenas de transmisión válidas. Los elementos del menú muestran una etiqueta legible junto al identificador interno de la antena.

**Botón de grosor del marcador** — Cambia la línea del marcador VFO entre Desactivado, 1 px y 3 px. Se conserva por segmento.

**Botón de bordes del filtro** — Alterna las líneas de borde del filtro en la banda de paso del espectro. Se conserva por segmento.

**Alternancia de contracción** — Contrae el panel VFO a una tira compacta de solo frecuencia. Se conserva por segmento.

**Distintivo TX** — Se muestra cuando este segmento es el segmento de transmisión activo. Muestra un indicador TX rojo.

**Distintivo SPLIT** — Se muestra cuando TX está asignado a un segmento diferente al segmento de recepción activo. Muestra un indicador SPLIT ámbar.

**Botones + etiquetas RIT / XIT** — Habilita la sintonía incremental del receptor (RIT) o del transmisor (XIT) para este segmento. Cuando está activo, la etiqueta junto a cada botón muestra el valor de desplazamiento actual. Gire la rueda del ratón sobre el botón para ajustar el desplazamiento en pasos de 10 Hz. Ninguna de las configuraciones se conserva; el estado refleja el estado en vivo de la radio.

**Botón + control deslizante de squelch (pestaña Audio)** — Habilita el squelch para este segmento. El control deslizante adyacente establece el umbral. El squelch se deshabilita automáticamente cuando el modo del segmento es CW, digital o RTTY, porque en esos modos el audio alimenta decodificadores externos a través de DAX donde el squelch bloquearía señales FSK débiles (#2504). El botón y el control deslizante se atenúan en esos modos.

## Consejos

- Los desplazamientos RIT y XIT son independientes. Puede habilitar ambos al mismo tiempo para desplazar la recepción y transmisión de forma independiente.
- El ajuste con la rueda del ratón es de 10 Hz por paso. Para desplazamientos mayores, gire la rueda varias muescas.
- Cuando un segmento está bloqueado, la sintonía con la rueda del ratón en el panel VFO está bloqueada. Aparece una notificación que indica que la sintonía está bloqueada por el bloqueo. La entrada directa de frecuencia también se cancela si estaba en progreso cuando se aplicó el bloqueo.

## Cambios en v26.7.4

### Renderizado de sombra de elevación

El marcador VFO ahora renderiza su sombra de elevación utilizando un widget `FlagShadow` dedicado, separado del `VfoWidget` principal. Esto significa que las repintadas de medidores en vivo dentro del marcador VFO no fuerzan que la sombra se vuelva a desenfocar a la velocidad de animación, lo que mejora la tasa de cuadros cuando un SmartMeter u otro widget de actualización en vivo está incrustado en el área del marcador VFO. La sombra utiliza un algoritmo de desenfoque de cuadro con una imagen almacenada en caché que se reconstruye solo cuando cambia el tamaño del widget o la relación de píxeles del dispositivo.

### Reenvío de altura-para-ancho para páginas de medidores

La pila de pestañas ahora reenvía `heightForWidth()` desde la página actual. Esto permite que una página que conserva una relación de aspecto (como un widget SmartMeter incrustado a través de `SmartMtrWidget`) impulse la altura de la tira; las páginas sin altura-para-ancho (como el espaciador del S-meter) no se ven afectadas.

### Controles de filtro adaptativo

El panel VFO ahora incluye soporte para controles de filtro adaptativo a través de la nueva clase `AdaptiveFilterControls`. Cuando la radio proporciona señales de filtro adaptativo (compatible con ciertas compilaciones de firmware FLEX-8600), el panel VFO muestra controles para configurar el comportamiento del filtro adaptativo por segmento.

## Cambios en v26.6.3

### Botones de pestaña reemplazados por QPushButton

Las etiquetas de las pestañas en la barra de pestañas se han reemplazado de QLabel a QPushButton. Cada pestaña ahora es un botón plano, seleccionable, con soporte de enfoque de teclado. Presionar Tab recorre los botones de las pestañas. El clic derecho en el botón de la pestaña Audio (altavoz) alterna el silencio directamente sin abrir la pestaña.

### Anuncios de frecuencia accesibles

Cuando un lector de pantalla u otra herramienta de accesibilidad está activa, el indicador de frecuencia emite un evento de cambio de valor accesible cuando la frecuencia cambia. Se suprimen los anuncios duplicados: solo los textos de frecuencia distintos activan un nuevo anuncio.

### Soporte de sintonía inversa con rueda del ratón

La sintonía con la rueda del ratón ahora respeta la preferencia **Reverse mouse wheel** en `InteractionSettings`. Cuando está habilitada, desplazarse hacia arriba disminuye la frecuencia y desplazarse hacia abajo la aumenta.

## Cambios en v26.6.1

### Control deslizante de paneo consciente del tema

El control deslizante de paneo en la pestaña Audio ahora utiliza un relleno anclado al centro. La ranura del control deslizante se rellena desde el centro hacia afuera: acento azul a la derecha del centro cuando el paneo es pesado a la derecha, y un color de fondo a la izquierda del centro. Cuando el paneo es pesado a la izquierda, la ranura se rellena desde el centro hacia la izquierda en color de acento mientras que el lado derecho utiliza el color de fondo. Esto coincide con el comportamiento de un control de balance estéreo donde el cero significativo es el punto medio. Todavía se dibuja un pequeño punto de marca central en la ranura en el punto medio.

### Soporte de tema para botones y distintivos

Todos los botones y distintivos del panel VFO ahora respetan el tema actual. La hoja de estilo de los botones se ha actualizado para usar tokens de tema en lugar de colores codificados. Los siguientes tokens se declaran para cobertura del inspector:
- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

El panel VFO está registrado como un contenedor de tematización separado bajo el ámbito `spectrum/vfo`. Esto significa que las selecciones de color del tema se pueden aplicar específicamente al panel VFO sin afectar al resto de la pantalla del espectro.

## Cambios en v26.5.3

### Comportamiento de sintonía de segmento bloqueado

Cuando un segmento está bloqueado, las siguientes interacciones de sintonía en el panel VFO ahora están bloqueadas:

- **Sintonía con rueda del ratón**: Desplazar la rueda del ratón sobre el panel VFO contraído o expandido ya no cambia la frecuencia. Se muestra una notificación `tuneBlockedByLock`.
- **Entrada directa de frecuencia**: Si está en medio de escribir una frecuencia y el segmento se bloquea, la entrada directa se cancela y la pantalla vuelve a la frecuencia bloqueada.

La superposición de bloqueo (icono de candado) es gestionada centralmente por `SliceModel` y se limpia automáticamente cuando el segmento se desbloquea (#2983).

### Mejoras en la entrada directa de banda XVTR

Al ingresar una frecuencia directamente en el panel VFO, el analizador ahora maneja correctamente las entradas explícitas de MHz por encima de 54 MHz incluso cuando no está en una banda XVTR. Si escribe un valor en formato MHz (por ejemplo, `144.200`), se acepta hasta 50,000 MHz sin ser malinterpretado como kHz o Hz. La inserción de conveniencia de banda de 3 dígitos para enteros simples en bandas de 2m/70cm solo se aplica cuando la frecuencia del segmento está entre 100 MHz y 999 MHz.

### Optimización de altura de pestaña

La pila de pestañas del panel VFO ahora utiliza un widget `TabStack` personalizado que informa solo el tamaño preferido de la página actual. Anteriormente, cuando la pestaña DSP era más alta que la pestaña Mode (por ejemplo, cuando el contenedor de filtro digital era visible en modo DIGU/DIGL), el panel VFO asignaba altura en exceso, causando un espacio dentro de la pestaña Mode. Esto ahora está resuelto.

## Cambios en v26.5.2.1

### Manejo de frecuencia de banda XVTR

Cuando el segmento está en una banda XVTR, la frecuencia máxima aceptada durante la entrada directa se ha incrementado de 450 MHz a 50,000 MHz para soportar bandas de microondas. El comportamiento de inserción de banda de 3 dígitos (insertar automáticamente un decimal después del tercer dígito para enteros simples en 2m/70cm) ahora solo se activa cuando la frecuencia del segmento está entre 100 MHz y 999 MHz. Para bandas como 23cm (1296 MHz), los enteros simples se interpretan como la frecuencia en MHz directamente.

### Mejoras en el menú de antena

T
