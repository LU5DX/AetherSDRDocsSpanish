# Habilitar el desplazamiento RIT o XIT desde el panel VFO

RIT (Sintonización Incremental del Receptor) y XIT (Sintonización Incremental del Transmisor) permiten desplazar la frecuencia de recepción o transmisión en un pequeño margen sin mover el VFO principal. Esto es útil para contactos en frecuencias divididas o para compensar una estación que está ligeramente fuera de la frecuencia de sintonía.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO para la porción de espectro (slice) de destino debe estar abierto y expandido. Si está colapsado a una franja que solo muestra la frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla de espectro para la porción de espectro (slice) que desea ajustar. El panel VFO aparecerá anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el desplazamiento del receptor, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el desplazamiento RIT actual.
4. Para habilitar el desplazamiento del transmisor, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el desplazamiento XIT actual.
5. Con RIT o XIT activo, coloque el puntero del ratón sobre el botón correspondiente y gire la rueda del ratón para ajustar el desplazamiento. Cada paso de la rueda cambia el desplazamiento en 10 Hz.
6. Para deshabilitar RIT o XIT, vuelva a hacer clic en el botón activo.

## Función de cada control

| Control                              | Tipo              | Valor predeterminado | Notas                                                                     |
|--------------------------------------|-------------------|----------------------|---------------------------------------------------------------------------|
| Botón de antena RX                   | Botón pulsador    |                      | Abre el menú de selección de antena para la antena receptora de esta porción de espectro (slice). |
| Botón de antena TX                   | Botón pulsador    |                      | Abre el menú de selección de antena para la antena transmisora de esta porción de espectro (slice). |
| Indicador de frecuencia              | Indicador         |                      | Muestra la frecuencia actual de la porción de espectro (slice). Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y pulse Enter o Tab. |
| Etiqueta de ancho de filtro          | Indicador         |                      | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de ajuste preestablecido del filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de información. |
| Control deslizante de ganancia AF (pestaña Audio) | Control deslizante | 100       | Establece el nivel de salida de audio para esta porción de espectro (slice). No se conserva: refleja el estado en vivo de la radio. |
| Control deslizante de paneo (pestaña Audio) | Control deslizante | 50        | Establece el paneo estéreo izquierda/derecha para esta porción de espectro (slice). 50 = centro. |
| Botón de silencio (pestaña Audio)    | Botón de alternancia | desactivado | Silencia la salida de audio para esta porción de espectro (slice) sin cambiar el ajuste de ganancia AF. |
| Botón + control deslizante de squelch (pestaña Audio) | Botón de alternancia | desactivado | Activa el squelch para esta porción de espectro (slice). El control deslizante adyacente establece el umbral. |
| Combo AGC (pestaña Audio)            | Cuadro combinado  | FAST                | Establece la velocidad de ataque/liberación del AGC para esta porción de espectro (slice). |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia | desactivado | Activa el algoritmo de reducción de ruido correspondiente para esta porción de espectro (slice). La disponibilidad de los botones depende de la serie de radio y la compilación. |
| Botón ADSP (pestaña DSP)             | Botón pulsador    |                      | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). |
| Botón AetherVoice (pestaña DSP)      | Botón pulsador    |                      | Alterna la Canaleta de Audio Aetherial — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |
| Combo Mode (pestaña Mode)            | Cuadro combinado  | USB                  | Establece el modo de demodulación para esta porción de espectro (slice). |
| Botones de ajuste preestablecido de filtro (pestaña Mode) | Botón pulsador |                      | Aplica un ancho de filtro preestablecido guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en FilterPresets. |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | Botón de alternancia | desactivado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX)     | Cuadro combinado  | Off                  | Asigna un canal de audio DAX a esta porción de espectro (slice). |
| Botón de grosor del marcador         | Botón pulsador    | 1 px                 | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por porción de espectro (slice). |
| Botón de bordes de filtro            | Botón de alternancia | mostrado           | Alterna las líneas de borde del filtro en la banda pasante del espectro. Se conserva por porción de espectro (slice). |
| Alternancia de colapso               | Botón de alternancia | expandido          | Colapsa el panel VFO a una franja compacta que solo muestra la frecuencia. Se conserva por porción de espectro (slice). |
| Insignia TX                          | Indicador         |                      | Muestra TX (rojo) cuando esta porción de espectro (slice) es la porción de espectro (slice) de transmisión activa. Oculto en caso contrario. |
| Insignia SPLIT                       | Indicador         |                      | Muestra SPLIT (ámbar) cuando TX está asignada a una porción de espectro (slice) diferente a la porción de espectro (slice) de recepción activa. Oculto en caso contrario. |

**Botón de antena RX** — Abre un menú de selección de antena para la antena receptora de esta porción de espectro (slice). El menú ahora utiliza la propiedad `rxAntennaList()` por porción de espectro (slice) cuando está disponible, recurriendo a la lista global de antenas. Los elementos del menú muestran una etiqueta legible junto con el identificador interno de la antena.

**Botón de antena TX** — Abre un menú de selección de antena para la antena transmisora de esta porción de espectro (slice). El menú filtra los puertos de antena exclusivos de RX. Utiliza la función auxiliar `txAntennaOptions()` para determinar las antenas de transmisión válidas. Los elementos del menú muestran una etiqueta legible junto con el identificador interno de la antena.

**Botón de grosor del marcador** — Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por porción de espectro (slice).

**Botón de bordes de filtro** — Alterna las líneas de borde del filtro en la banda pasante del espectro. Se conserva por porción de espectro (slice).

**Alternancia de colapso** — Colapsa el panel VFO a una franja compacta que solo muestra la frecuencia. Se conserva por porción de espectro (slice).

**Insignia TX** — Se muestra cuando esta porción de espectro (slice) es la porción de espectro (slice) de transmisión activa. Muestra un indicador TX rojo.

**Insignia SPLIT** — Se muestra cuando TX está asignada a una porción de espectro (slice) diferente a la porción de espectro (slice) de recepción activa. Muestra un indicador SPLIT ámbar.

**Botones RIT / XIT + etiquetas** — Activan la sintonización incremental del receptor (RIT) o del transmisor (XIT) para esta porción de espectro (slice). Cuando están activos, la etiqueta al lado de cada botón muestra el valor de desplazamiento actual. Gire la rueda del ratón sobre el botón para ajustar el desplazamiento en pasos de 10 Hz. Ningún ajuste se conserva; el estado refleja el estado en vivo de la radio.

**Botón + control deslizante de squelch (pestaña Audio)** — Activa el squelch para esta porción de espectro (slice). El control deslizante adyacente establece el umbral. El squelch se desactiva automáticamente cuando el modo de la porción de espectro (slice) es CW, digital o RTTY, porque en esos modos el audio alimenta decodificadores externos a través de DAX, donde el squelch podría bloquear señales FSK débiles (#2504). El botón y el control deslizante se atenúan en esos modos.

## Consejos

- Los desplazamientos RIT y XIT son independientes. Puede activar ambos al mismo tiempo para desplazar la recepción y la transmisión de forma independiente.
- El ajuste con la rueda del ratón es de 10 Hz por paso. Para desplazamientos más grandes, gire la rueda varias muescas.
- Cuando una porción de espectro (slice) está bloqueada, la sintonización con la rueda del ratón en el panel VFO está bloqueada. Aparece una notificación que indica que la sintonización está bloqueada por el bloqueo. La entrada directa de frecuencia también se cancela si estaba en progreso cuando se aplica el bloqueo.

## Cambios en v26.6.1

### Control deslizante de paneo adaptado al tema

El control deslizante de paneo en la pestaña Audio ahora utiliza un relleno anclado al centro. La ranura del control deslizante se rellena desde el centro hacia afuera: en color de acento azul a la derecha del centro cuando el paneo está cargado a la derecha, y en un color de fondo a la izquierda del centro. Cuando el paneo está cargado a la izquierda, la ranura se rellena desde el centro hacia la izquierda en color de acento, mientras que el lado derecho utiliza el color de fondo. Esto coincide con el comportamiento de un control de balance estéreo donde el cero significativo es el punto medio. En la ranura, en el punto medio, todavía se dibuja un pequeño punto de marca central.

### Soporte de tema para botones e insignias

Todos los botones e insignias del panel VFO ahora respetan el tema actual. La hoja de estilo de los botones se ha actualizado para usar tokens de tema en lugar de colores fijos. Se declaran los siguientes tokens para cobertura de inspección:
- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

El panel VFO está registrado como un contenedor de tematización separado bajo el ámbito `spectrum/vfo`. Esto significa que las selecciones de color del tema se pueden aplicar específicamente al panel VFO sin afectar al resto de la pantalla de espectro.

## Cambios en v26.5.3

### Comportamiento de sintonización en porción de espectro (slice) bloqueada

Cuando una porción de espectro (slice) está bloqueada, las siguientes interacciones de sintonización en el panel VFO ahora están bloqueadas:

- **Sintonización con la rueda del ratón**: Girar la rueda del ratón sobre el panel VFO colapsado o expandido ya no cambia la frecuencia. Se muestra una notificación `tuneBlockedByLock`.
- **Entrada directa de frecuencia**: Si está en medio de escribir una frecuencia y la porción de espectro (slice) se bloquea, la entrada directa se cancela y la pantalla vuelve a la frecuencia bloqueada.

La superposición de bloqueo (icono de candado) es gestionada centralmente por `SliceModel` y se limpia automáticamente cuando la porción de espectro (slice) se desbloquea (#2983).

### Mejoras en la entrada directa en bandas XVTR

Al introducir una frecuencia directamente en el panel VFO, el analizador ahora gestiona correctamente las entradas explícitas de MHz por encima de 54 MHz, incluso cuando no se está en una banda XVTR. Si escribe un valor en formato MHz (p. ej., `144.200`), se acepta hasta 50 000 MHz sin ser malinterpretado como kHz o Hz. La inserción por conveniencia de banda de 3 dígitos para enteros simples en bandas de 2m/70cm sigue aplicándose solo cuando la frecuencia de la porción de espectro (slice) está entre 100 MHz y 999 MHz.

### Optimización de la altura de las pestañas

La pila de pestañas del panel VFO ahora utiliza un widget `TabStack` personalizado que informa solo el tamaño preferido de la página actual. Anteriormente, cuando la pestaña DSP era más alta que la pestaña Mode (por ejemplo, cuando el contenedor de filtro digital era visible en modo DIGU/DIGL), el panel VFO asignaba una altura excesiva, lo que provocaba un espacio vacío dentro de la pestaña Mode. Esto ahora está resuelto.

## Cambios en v26.5.2.1

### Gestión de frecuencia en bandas XVTR

Cuando la porción de espectro (slice) está en una banda XVTR, la frecuencia máxima aceptada durante la entrada directa se ha aumentado de 450 MHz a 50 000 MHz para admitir bandas de microondas. El comportamiento de inserción de banda de 3 dígitos (insertar automáticamente un decimal después del tercer dígito para enteros simples en las bandas de 2m/70cm) ahora solo se activa cuando la frecuencia de la porción de espectro (slice) está entre 100 MHz y 999 MHz. Para bandas como 23cm (1296 MHz), los enteros simples se interpretan directamente como la frecuencia en MHz.

### Mejoras en el menú de antena

Tanto los botones de antena RX como TX ahora muestran una etiqueta legible en el menú junto con el identificador interno de la antena. El menú utiliza `data()` internamente para la selección, coincidiendo con la cadena completa de la antena en lugar de la etiqueta mostrada. Los elementos del menú también incluyen texto de información sobre herramientas y de sugerencia de estado que muestra el identificador de antena sin procesar.

### Soporte de texto enriquecido para insignias de porción de espectro (slice)

La insignia de porción de espectro (slice) ahora admite formato de texto enriquecido (`Qt::RichText`), lo que permite el formateo HTML en ciertos casos (#2606).

## Cambios en v26.5.1

### Squelch deshabilitado en modo RTTY

El botón y el control deslizante de squelch ahora se desactivan automáticamente cuando la porción de espectro (slice) está en modo RTTY, además de las restricciones de modo digital y CW existentes. Cuando el modo es RTTY, el botón de squelch se atenúa y no se puede activar, y el control deslizante de squelch se atenúa y no se puede ajustar. Si el squelch estaba activado previamente, se desactiva automáticamente al cambiar al modo RTTY. Esto evita que el squelch bloquee las señales FSK débiles que los decodificadores RTTY externos necesitan recibir a través de DAX (#2504).

## Cambios en v0.9.8

###
