# Controles de RX (RxApplet)

El applet de Controles de RX proporciona controles de recepción por slice para modo, sintonización de frecuencia, selección de antenas RX/TX, ancho de filtro, AGC, ganancia/panorámica de AF, squelch, RIT/XIT y configuración de duplex para repetidoras FM.

## Bloquear el slice para evitar resintonizaciones accidentales

La función de bloqueo de sintonización evita que un slice responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin el riesgo de mover el VFO al hacer clic en el panadapter o al desplazar la rueda del mouse.

### Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles de RX requiere una conexión activa con la radio.
- El applet de Controles de RX debe estar visible. Si no lo está, haga clic en el botón de la bandeja RX en la barra lateral derecha para mostrarlo.

### Pasos

1. En el applet de Controles de RX, identifique la fila de encabezado que contiene la insignia del slice, el botón de bloqueo y los selectores de antena.
2. Si tiene más de un slice, haga clic en la pestaña del slice correspondiente (A hasta H) para seleccionar el slice que desea bloquear.
3. Haga clic en el botón 🔓 en la fila de encabezado. El icono cambia a 🔒 y se vuelve azul, confirmando que el slice está bloqueado.
4. Para desbloquear, haga clic en 🔒 nuevamente. El icono vuelve a 🔓 y el slice reanuda la respuesta a los cambios de frecuencia.

### Qué hace cada control

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonización en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los cambios de frecuencia. Haga clic nuevamente para desbloquear. |

### Consejos

- El estado de bloqueo se aplica por slice. Puede bloquear el slice A mientras el slice B permanece libremente sintonizable.
- El botón de bloqueo siempre está visible en la fila de encabezado independientemente del modo actual.
- Desde v0.9.3, los botones de pestaña del slice y la insignia del slice usan colores por slice administrados por SliceColorManager. Los colores son personalizables por slice y persisten entre sesiones. El mismo color se refleja en los botones de pestaña del slice, la insignia del slice, los widgets de VFO y las tiras de medidores.

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

Cuando la radio se desconecta o el número de slices disponibles cambia, AetherSDR ahora elimina todos los botones de pestaña de slice generados y restaura automáticamente la insignia estática del slice (`clearSliceButtons()`, #2254). Al reconectar, la fila de pestañas se reconstruye para coincidir con el nuevo número de slices. Si el número no ha cambiado, los botones existentes se reutilizan sin reconstrucción.

Las conexiones de señal entre el grupo de botones de slice y el controlador `sliceActivationRequested` están protegidas para que reconectar a la radio no acumule controladores de señal duplicados.

## Formato de almacenamiento de preajustes de filtro (v0.9.5.1)

Los preajustes de filtro guardados para un modo determinado (clave de configuración `FilterPresets`) ahora admiten dos formatos de almacenamiento:

- **Solo ancho** — un entero simple que representa el ancho de banda del filtro en Hz (por ejemplo, `2700`). Este es el formato heredado y sigue funcionando.
- **Lo:Hi** — un par separado por dos puntos de compensaciones de borde inferior y superior en Hz (por ejemplo, `-1400:1300`). Este formato preserva una banda de paso asimétrica exactamente como la configuró al arrastrar los bordes del widget de banda de paso del filtro.

Cuando hace clic derecho en un botón de preajuste de filtro para guardar el ancho actual, AetherSDR escribe la forma `lo:hi` cuando la banda de paso es asimétrica (#2259). Los preajustes guardados en el formato antiguo de solo ancho se leen y se aplican como bandas de paso centradas, exactamente como antes.

Se almacenan y muestran hasta seis preajustes por modo en el applet de Controles de RX. Los botones se ocultan para los modos FM, NFM y DFM.

## Ancho de filtro por pasos (v0.9.8)

El sistema de preajustes de ancho de filtro ahora admite un método `stepFilterWidth()` que recorre la lista de preajustes por modo. Esto permite accesos rápidos de ampliar/estrechar que producen geometría de bordes correcta para el modo en todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB).

Cuando aplica una operación de ampliar o estrechar:

- AetherSDR encuentra el preajuste de ancho más cercano que coincida con la banda de paso actual del filtro.
- Luego selecciona el siguiente preajuste más ancho o más estrecho de la lista por modo.
- El preajuste se aplica mediante `applyFilterPreset()`, que usa las compensaciones de borde correctas para el modo actual.

Esto garantiza que ampliar o estrechar un filtro siempre se mantenga dentro de los valores de preajuste apropiados para el modo y produzca la geometría de banda de paso correcta.

## Formato de ancho de filtro (v0.9.8)

El método `formatFilterWidth()` ahora es una función estática pública, compartida con el panel de VFO (`VfoWidget`). Esto garantiza que tanto el applet de Controles de RX como el panel de VFO muestren lecturas idénticas de ancho de filtro. El método utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto (#2197).

## Comportamiento de squelch en modos NT y RTTY (v26.5.1)

El squelch está deshabilitado en el modo NT, el modo RTTY y los modos digitales existentes (`DIGU`, `DIGL`). Esto evita que el squelch bloquee señales FSK débiles y recorte caracteres, lo que rompería la decodificación (#2504). Si el squelch estaba activo cuando cambió a RTTY o a un modo digital, AetherSDR lo desactiva automáticamente y guarda el estado para poder restaurarlo cuando salga del modo. El botón y el control deslizante de squelch permanecen deshabilitados mientras el modo está activo.

## Activación del modo RADE (v26.5.2.1)

RADE ("Reverse Adaptive Digital Enhancement" o un modo digital específico) es una etiqueta de modo solo del lado del cliente. Cuando selecciona RADE en el cuadro combinado de modos, AetherSDR establece el modo inmediatamente en el slice, pero la radio devuelve el modo subyacente real (DIGL o DIGU) en la siguiente actualización de estado. Debido a esto, la propiedad interna `mode()` del slice nunca será `"RADE"` después de que la radio responda.

Al cambiar del modo RADE a cualquier otro modo:

- AetherSDR verifica si el modo del slice era `"RADE"` antes de emitir la señal de desactivación `radeActivated(false)`.
- Debido a que la radio reemplaza RADE con DIGL/DIGU, `mode() == "RADE"` nunca es verdadero en el momento del cambio. Esto significa que la señal de desactivación no se emite al cambiar de RADE.

Para activar el modo RADE desde código (por ejemplo, mediante el cuadro combinado de VFO, la carga de perfil al iniciar o `MainWindow::activateRADE`), AetherSDR llama a la ruta de activación RADE interna directamente en lugar de depender del cambio de valor del cuadro combinado de modos. Use el botón `Activate RADE` en el menú de modos o el sistema de perfiles para habilitar RADE.

## Persistencia del umbral manual de squelch (v26.5.2.1)

El control deslizante de nivel de squelch ahora persiste el último valor manual elegido por el usuario entre sesiones. Esto es necesario porque el modo de squelch automático puede sobrescribir el `squelchLevel` en el slice con valores sugeridos por el algoritmo, y la radio no preserva la preferencia manual del operador entre ciclos de modo o lanzamientos de la aplicación.

AetherSDR almacena el umbral manual en la configuración de la aplicación bajo la clave `LastManualSquelchLevel`. El valor se limita al rango válido de 0–100. En el primer lanzamiento, el valor predeterminado es 20.

Cuando habilita el squelch y ajusta el control deslizante, el nuevo valor se guarda inmediatamente. Cuando inicia una nueva sesión, el control deslizante vuelve al último nivel manual guardado en lugar del predeterminado.

## Modo NT

La versión 0.9.3 añade el modo `NT` junto a los modos digitales existentes (`DIGU`, `DIGL`). Se comporta de manera idéntica a otros modos digitales en los siguientes aspectos:

- **Preajustes de filtro** — NT comparte el conjunto de preajustes de filtro DIG (100–2000 Hz). La etiqueta de ancho de filtro se actualiza en consecuencia.
- **Cálculo de ancho de filtro** — La visualización del ancho de filtro mide la compensación del borde superior, igual que USB y DIGU.
- **Squelch** — El botón SQL y el control deslizante de squelch están deshabilitados en el modo NT. Debido a que el audio se enruta a través de DAX en los modos digitales, el squelch no es significativo. Si el squelch estaba activo cuando cambió al modo NT, AetherSDR lo desactiva automáticamente y lo restaura cuando sale del modo NT.

## Mejoras en la selección de antena (v26.5.2.1)

Los cuadros combinados de antena RX y TX ahora usan las listas de antena por slice cuando están disponibles, en lugar de depender únicamente de la lista global de antenas de la radio. Esto proporciona opciones de antena más precisas, especialmente para slices en diferentes panadapters.

### Menú de antena RX

- Cuando el slice proporciona una `rxAntennaList()`, el menú muestra solo esos puertos de antena.
- Si el slice no proporciona una lista, se usa la `ant_list` global del estado del panadapter como respaldo.
- Cada acción del menú almacena el nombre del puerto de antena en la propiedad de datos de la acción, lo que garantiza una selección correcta incluso cuando las etiquetas de visualización difieren de los nombres de puerto.
- Los tooltips y las sugerencias de estado muestran el nombre del puerto de antena sin procesar para mayor claridad.

### Menú de antena TX

- El menú de antena TX se completa mediante una función auxiliar `txAntennaOptions()`.
- Esta función recopila antenas capaces de TX tanto de la lista global de antenas como de fuentes adicionales.
- Los puertos de antena solo RX (aquellos que comienzan con `RX` sin distinguir mayúsculas) se excluyen del menú.
- Los puertos de antena con prefijos `ANT`, `TX` o la cadena exacta `XVTR` se consideran tokens de respaldo capaces de TX.

### Formato de visualización

Ambos menús de antena ahora usan una función auxiliar `antennaMenuLabel()` para formatear las etiquetas de visualización. La etiqueta incluye el nombre del puerto de antena seguido de información del rango de frecuencia entre paréntesis cuando está disponible, lo que facilita identificar qué antena seleccionar para una banda determinada.

## Formato de insignia de slice (v26.5.2.1)

La etiqueta de insignia de slice ahora admite renderizado de texto enriquecido (HTML). Esto permite que la letra del slice incluya formato, como caracteres en superíndice o subíndice, cuando la identidad del slice lo requiera (#2606). La insignia continúa usando el mismo esquema de color por slice y el tamaño fijo de 20x20 píxeles que antes.

## Mejoras en la entrada de frecuencia (v26.5.3)

El sistema de entrada de frecuencia ahora usa `FrequencyEntryParser::normalizedMhzText()` para el análisis y `FrequencyEntryParser::isExplicitMhzEntry()` para detectar entradas explícitas en MHz. Esto proporciona un manejo más robusto del formato de frecuencia y la detección de entradas.

### Entradas explícitas en MHz

Cuando ingresa un valor de frecuencia mayor que 54.0 MHz en el campo de edición de frecuencia, AetherSDR verifica si es una entrada explícita en MHz. Si se detecta que la entrada está explícitamente en MHz (por ejemplo, `146.520` o `446.000`), la radio permite sintonizar hasta 50,000 MHz, lo que permite el acceso directo a las bandas VHF/UHF/SHF sin requerir una antena XVTR. Esto es particularmente útil para ingresar frecuencias de las bandas de 2 m, 70 cm o superiores directamente.

### Normalización de frecuencia de entrada

La función `normalizedMhzText()` limpia el texto de frecuencia ingresado eliminando puntos superfluos y caracteres de formato. Esto garantiza que entradas como `14.250.000` (con puntos de agrupación de dígitos) se analicen correctamente como `14.250000` MHz.

### Conveniencia de banda de 3 dígitos

Para slices XVTR (o cuando la frecuencia está por encima de 54 MHz), el sistema aplica la lógica de conveniencia de banda de 3 dígitos: una entrada como `1446` se interpreta como 144.6 MHz (para la banda de 2 m), mientras que las entradas para bandas de 23 cm/microondas (por ejemplo, `1296`) se tratan como valores directos en MHz. Esta lógica solo se aplica cuando la entrada no es una entrada explícita en MHz.

### Escape para cancelar (v0.9.0)

Presionar Escape mientras el editor de frecuencia está activo cancela la edición, restaura la frecuencia anterior y cierra el editor (Corregido en v0.9.0, #1954).

## Comportamiento del botón de silencio (v26.5.3)

El botón de silencio (🔊 / 🔇) ahora usa discriminación de clic simple basada en temporizador. Esto proporciona una detección de doble clic más confiable para silenciar/activar el sonido de todos los slices propios.

### Clic simple

Un clic simple inicia un temporizador configurado al intervalo de doble clic de la plataforma (~400 ms). Cuando el temporizador expira, el estado de silencio del slice actual se alterna.

### Doble clic

Un doble clic cancela inmediatamente el temporizador de clic simple y emite `muteAllToggled`, que silencia o activa el sonido de todos los slices propiedad del cliente actual. La segunda pulsación de la secuencia de doble clic no produce una señal `clicked()` separada porque el filtro de eventos intercepta el evento `MouseButtonDblClick` y devuelve verdadero, evitando que `QAbstractButton::mouseDoubleClickEvent` se ejecute.

### Actualización del icono

El icono del botón de silencio (🔊 o 🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio mediante `SliceModel::audioMuteChanged`. Esto garantiza que el icono siempre refleje el estado autoritativo de la radio, según lo requiere la Política de Configuración Autoritativa de la Radio (#2489).

### Persistencia del estado

El estado de silencio NO se guarda ni se restaura al reconectar. La radio es siempre la fuente de verdad para el estado de silencio de audio.

## Marca central del control deslizante L/R (v26.6.1)

El control deslizante de panorámica L/R ahora dibuja un pequeño punto de marca central en la ranura. Esto proporciona una referencia visual para la posición neutra (centro), lo que facilita identificar cuándo la panorámica está centrada.

###
