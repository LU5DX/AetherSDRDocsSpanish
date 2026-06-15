# Habilitar el desplazamiento RIT o XIT desde el panel VFO

RIT (Receiver Incremental Tuning) y XIT (Transmitter Incremental Tuning) le permiten desplazar la frecuencia de recepción o transmisión en un pequeño valor sin mover el VFO principal. Esto es útil para trabajar contactos en split o para compensar una estación que está ligeramente fuera de la frecuencia marcada.

## Antes de empezar

- AetherSDR debe estar conectado al equipo. El panel VFO requiere una conexión activa con el equipo.
- El panel VFO para el slice de destino debe estar abierto y expandido. Si está colapsado en la tira de solo frecuencia, haga clic en cualquier parte para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en el espectro del slice que desea ajustar. El panel VFO aparece anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el desplazamiento del receptor, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el desplazamiento RIT actual.
4. Para habilitar el desplazamiento del transmisor, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el desplazamiento XIT actual.
5. Con RIT o XIT activo, coloque el puntero del ratón sobre el botón correspondiente y gire la rueda del ratón para ajustar el desplazamiento. Cada paso de la rueda cambia el desplazamiento en 10 Hz.
6. Para deshabilitar RIT o XIT, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control                              | Tipo               | Valor predeterminado | Notas                                                                |
|--------------------------------------|--------------------|----------------------|----------------------------------------------------------------------|
| Botón de antena RX                   | Botón pulsador     |                      | Abre el menú de selección de antena para la antena receptora de este slice. |
| Botón de antena TX                   | Botón pulsador     |                      | Abre el menú de selección de antena para la antena transmisora de este slice. |
| Indicador de frecuencia              | Indicador          |                      | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro          | Indicador          |                      | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad. |
| Deslizador de ganancia AF (pestaña Audio) | Deslizador       | 100                  | Establece el nivel de salida de audio para este slice. No se persiste: refleja el estado en vivo del equipo. |
| Deslizador de paneo (pestaña Audio)  | Deslizador         | 50                   | Establece el paneo estéreo izquierda/derecha para este slice. 50 = centro. |
| Botón Silenciar (pestaña Audio)      | Botón de alternancia | desactivado        | Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. |
| Botón + deslizador de squelch (pestaña Audio) | Botón de alternancia | desactivado | Activa el squelch para este slice. El deslizador adyacente establece el umbral. |
| Combo AGC (pestaña Audio)            | Cuadro combinado   | FAST                | Establece la velocidad de ataque/liberación del AGC para este slice. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia | desactivado | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie del equipo y la compilación. |
| Botón ADSP (pestaña DSP)             | Botón pulsador     |                      | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). |
| Botón AetherVoice (pestaña DSP)      | Botón pulsador     |                      | Alterna la tira de canal de audio Aetherial, el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |
| Combo Mode (pestaña Mode)            | Cuadro combinado   | USB                  | Establece el modo de demodulación para este slice. |
| Botones preestablecidos de filtro (pestaña Mode) | Botón pulsador |                      | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se persiste en FilterPresets. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Botón de alternancia | desactivado | Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX)     | Cuadro combinado   | Off                  | Asigna un canal de audio DAX a este slice. |
| Botón de grosor del marcador         | Botón pulsador     | 1 px                 | Recorre la línea del marcador VFO entre Desactivado, 1 px y 3 px. Se persiste por slice. |
| Botón de bordes del filtro           | Botón de alternancia | mostrado           | Alterna las líneas de borde del filtro en la banda pasante del espectro. Se persiste por slice. |
| Alternar colapso                     | Botón de alternancia | expandido           | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se persiste por slice. |
| Distintivo TX                        | Indicador          |                      | Muestra TX (rojo) cuando este slice es el slice transmisor activo. Oculto en caso contrario. |
| Distintivo SPLIT                     | Indicador          |                      | Muestra SPLIT (ámbar) cuando TX está asignado a un slice diferente al slice receptor activo. Oculto en caso contrario. |

**Botón de antena RX** — Abre un menú de selección de antena para la antena receptora de este slice. El menú ahora utiliza la propiedad `rxAntennaList()` por slice cuando está disponible, recurriendo a la lista global de antenas. Los elementos del menú muestran una etiqueta legible junto con el identificador interno de la antena.

**Botón de antena TX** — Abre un menú de selección de antena para la antena transmisora de este slice. El menú filtra los puertos de antena solo de RX. Utiliza el auxiliar `txAntennaOptions()` para determinar las antenas transmisoras válidas. Los elementos del menú muestran una etiqueta legible junto con el identificador interno de la antena.

**Botón de grosor del marcador** — Recorre la línea del marcador VFO entre Desactivado, 1 px y 3 px. Se persiste por slice.

**Botón de bordes del filtro** — Alterna las líneas de borde del filtro en la banda pasante del espectro. Se persiste por slice.

**Alternar colapso** — Colapsa el panel VFO a una tira compacta de solo frecuencia. Se persiste por slice.

**Distintivo TX** — Se muestra cuando este slice es el slice transmisor activo. Muestra un indicador TX rojo.

**Distintivo SPLIT** — Se muestra cuando TX está asignado a un slice diferente al slice receptor activo. Muestra un indicador SPLIT ámbar.

**Botones + etiquetas RIT / XIT** — Activan la sintonización incremental del receptor (RIT) o transmisor (XIT) para este slice. Cuando están activos, la etiqueta junto a cada botón muestra el valor de desplazamiento actual. Gire la rueda del ratón sobre el botón para ajustar el desplazamiento en pasos de 10 Hz. Ninguno de los ajustes se persiste; el estado refleja el estado en vivo del equipo.

**Botón + deslizador de squelch (pestaña Audio)** — Activa el squelch para este slice. El deslizador adyacente establece el umbral. El squelch se desactiva automáticamente cuando el modo del slice es CW, digital o RTTY, porque en esos modos el audio alimenta decodificadores externos a través de DAX donde el squelch bloquearía señales FSK débiles (#2504). El botón y el deslizador se atenúan en esos modos.

## Consejos

- Los desplazamientos RIT y XIT son independientes. Puede activar ambos al mismo tiempo para desplazar recepción y transmisión de forma independiente.
- El ajuste con la rueda del ratón es de 10 Hz por paso. Para desplazamientos mayores, gire la rueda varias muescas.
- Cuando un slice está bloqueado, la sintonización con la rueda del ratón en el panel VFO está bloqueada. Aparece una notificación indicando que la sintonización está bloqueada por el bloqueo. La entrada directa de frecuencia también se cancela si estaba en curso cuando se aplica el bloqueo.

## Cambios en v26.6.3

### Botones de pestaña reemplazados por QPushButton

Las etiquetas de las pestañas en la barra de pestañas se han reemplazado de QLabel a QPushButton. Cada pestaña es ahora un botón plano, seleccionable, con soporte de enfoque por teclado. Presionar Tab recorre los botones de pestaña. Haga clic derecho en el botón de la pestaña Audio (altavoz) para alternar el silencio directamente sin abrir la pestaña.

### Anuncios de frecuencia accesibles

Cuando un lector de pantalla u otra herramienta de accesibilidad está activa, el indicador de frecuencia emite un evento de cambio de valor accesible cuando cambia la frecuencia. Se suprimen los anuncios duplicados: solo los textos de frecuencia distintos activan un nuevo anuncio.

### Soporte de sintonización inversa con rueda del ratón

La sintonización con la rueda del ratón ahora respeta la preferencia **Reverse mouse wheel** en `InteractionSettings`. Cuando está activada, desplazar la rueda hacia arriba disminuye la frecuencia y desplazarla hacia abajo la aumenta.

## Cambios en v26.6.1

### Deslizador de paneo con conciencia de tema

El deslizador de paneo en la pestaña Audio ahora utiliza un relleno anclado al centro. La ranura del deslizador se llena desde el centro hacia afuera: acento azul a la derecha del centro cuando el paneo es pesado a la derecha, y un color de fondo a la izquierda del centro. Cuando el paneo es pesado a la izquierda, la ranura se llena desde el centro hacia la izquierda en color de acento mientras que el lado derecho usa el color de fondo. Esto coincide con el comportamiento de un control de balance estéreo donde el cero significativo es el punto medio. Un pequeño punto de marca central todavía se pinta en la ranura en el punto medio.

### Soporte de tema para botones y distintivos

Todos los botones y distintivos del panel VFO ahora honran el tema actual. La hoja de estilo de los botones se ha actualizado para usar tokens de tema en lugar de colores fijos. Los siguientes tokens se declaran para cobertura de inspector:
- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

El panel VFO está registrado como un contenedor de tematización separado bajo el ámbito `spectrum/vfo`. Esto significa que las selecciones de color del tema se pueden aplicar específicamente al panel VFO sin afectar al resto de la visualización del espectro.

## Cambios en v26.5.3

### Comportamiento de sintonización con slice bloqueado

Cuando un slice está bloqueado, las siguientes interacciones de sintonización en el panel VFO ahora están bloqueadas:

- **Sintonización con rueda del ratón**: Desplazar la rueda del ratón sobre el panel VFO colapsado o expandido ya no cambia la frecuencia. Se muestra una notificación `tuneBlockedByLock`.
- **Entrada directa de frecuencia**: Si está escribiendo una frecuencia y el slice se bloquea, la entrada directa se cancela y la visualización vuelve a la frecuencia bloqueada.

La superposición de bloqueo (icono de candado) es gestionada centralmente por `SliceModel` y se borra automáticamente cuando el slice se desbloquea (#2983).

### Mejoras en la entrada directa de banda XVTR

Al ingresar una frecuencia directamente en el panel VFO, el analizador ahora maneja correctamente las entradas explícitas de MHz por encima de 54 MHz incluso cuando no está en una banda XVTR. Si escribe un valor en formato MHz (por ejemplo, `144.200`), se acepta hasta 50 000 MHz sin ser malinterpretado como kHz o Hz. La inserción de conveniencia de banda de 3 dígitos para enteros simples en bandas de 2m/70cm todavía se aplica solo cuando la frecuencia del slice está entre 100 MHz y 999 MHz.

### Optimización de altura de pestaña

La pila de pestañas del panel VFO ahora utiliza un widget `TabStack` personalizado que informa solo el tamaño preferido de la página actual. Anteriormente, cuando la pestaña DSP era más alta que la pestaña Mode (por ejemplo, cuando el contenedor de filtro digital era visible en modo DIGU/DIGL), el panel VFO asignaba un exceso de altura, causando un espacio vacío dentro de la pestaña Mode. Esto ahora está resuelto.

## Cambios en v26.5.2.1

### Manejo de frecuencia de banda XVTR

Cuando el slice está en una banda XVTR, la frecuencia máxima aceptada durante la entrada directa se ha incrementado de 450 MHz a 50 000 MHz para soportar bandas de microondas. El comportamiento de inserción de banda de 3 dígitos (insertar automáticamente un decimal después del tercer dígito para enteros simples en 2m/70cm) ahora solo se activa cuando la frecuencia del slice está entre 100 MHz y 999 MHz. Para bandas como 23 cm (1296 MHz), los enteros simples se interpretan directamente como la frecuencia en MHz.

### Mejoras en el menú de antena

Tanto los botones de antena RX como TX ahora muestran una etiqueta legible en el menú junto con el identificador interno de la antena. El menú utiliza `data()` internamente para la selección, coincidiendo con la cadena completa de la antena en lugar de la etiqueta mostrada. Los elementos del menú también incluyen texto de información sobre herramientas y texto de sugerencia de estado que muestra el identificador de antena sin procesar.

### Soporte de texto enriquecido para distintivos de slice

El distintivo de slice ahora soporta formato de texto enriquecido (`Qt::RichText`), permitiendo formato HTML en ciertos casos (#2606).

## Cambios en v26.5.1

### Squelch deshabilitado en modo RTTY

El botón y deslizador de squelch ahora se desactivan automáticamente cuando el slice está en modo RTTY, además de las restricciones de modo digital y CW existentes. Cuando el modo es RTTY, el botón de squelch se atenúa y no puede activarse, y el deslizador de squelch se atenúa y no puede ajustarse. Si el squelch estaba previamente activado, se desactiva automáticamente al cambiar al modo RTTY. Esto evita que el squelch bloquee señales FSK débiles que los decodificadores RTTY externos necesitan recibir a través de DAX (#2504).

## Cambios en v0.9.8

### Pestaña DSP — nuevos botones ADSP y AetherVoice

La **pestaña DSP** en el panel VFO ahora incluye dos nuevos botones de lanzamiento DSP del lado del cliente:

- **ADSP** — Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Este es un botón pulsador de una celda con estilo similar a las altern
