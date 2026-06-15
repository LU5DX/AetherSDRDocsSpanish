# Bloquear el slice para evitar una re-sintonización accidental

La función de bloqueo de sintonía evita que un slice responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin el riesgo de mover el VFO al hacer clic en el panadapter o al desplazar la rueda del ratón.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión de radio activa.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX de la barra lateral derecha para mostrarlo.

## Pasos

1. En el applet RX Controls, identifique la fila del encabezado que contiene la insignia del slice, el botón de bloqueo y los selectores de antena.
2. Si tiene más de un slice, haga clic en la pestaña del slice correspondiente (A a H) para seleccionar el slice que desea bloquear.
3. Haga clic en el botón 🔓 en la fila del encabezado. El icono cambia a 🔒 y se vuelve azul, confirmando que el slice está bloqueado.
4. Para desbloquear, haga clic en 🔒 nuevamente. El icono vuelve a 🔓 y el slice vuelve a responder a los cambios de frecuencia.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento                                                                                                                  |
|---------|----------------------|---------------------------------------------------------------------------------------------------------------------------------|
| 🔓 / 🔒 | 🔓 (desbloqueado)    | Alterna el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los cambios de frecuencia. Vuelva a hacer clic para desbloquear. |

## Consejos

- El estado de bloqueo se aplica por slice. Puede bloquear el slice A mientras el slice B permanece libremente sintonizable.
- El botón de bloqueo siempre está visible en la fila del encabezado, independientemente del modo actual.
- Desde la v0.9.3, los botones de las pestañas de los slices y la insignia del slice usan colores por slice gestionados por SliceColorManager. Los colores son personalizables por slice y persisten entre sesiones. El mismo color se refleja en los botones de las pestañas de los slices, la insignia del slice, los widgets VFO y las tiras de medidores.

## Comportamiento de las pestañas de los slices al reconectar (v0.9.5.1)

Cuando la radio se desconecta o el número de slices disponibles cambia, AetherSDR ahora elimina todos los botones de pestañas de slices generados y restaura automáticamente la insignia de slice estática (`clearSliceButtons()`, #2254). Al reconectar, la fila de pestañas se reconstruye para coincidir con el nuevo número de slices. Si el número no ha cambiado, los botones existentes se reutilizan sin reconstrucción.

Las conexiones de señal entre el grupo de botones de slices y el controlador `sliceActivationRequested` están protegidas para que la reconexión a la radio no acumule controladores de señal duplicados.

## Formato de almacenamiento de presets de filtro (v0.9.5.1)

Los presets de filtro guardados para un modo determinado (clave de configuración `FilterPresets`) ahora admiten dos formatos de almacenamiento:

- **Solo ancho** — un número entero que representa el ancho de banda del filtro en Hz (por ejemplo, `2700`). Este es el formato heredado y sigue funcionando.
- **Lo:Hi** — un par separado por dos puntos de los desplazamientos del borde inferior y superior en Hz (por ejemplo, `-1400:1300`). Este formato conserva una banda de paso asimétrica exactamente como la configuró arrastrando los bordes del widget de la banda de paso del filtro.

Cuando hace clic derecho en un botón de preset de filtro para guardar el ancho actual, AetherSDR escribe el formato `lo:hi` cuando la banda de paso es asimétrica (#2259). Los presets guardados en el formato antiguo de solo ancho se leen y se aplican como bandas de paso centradas, exactamente como antes.

Se almacenan y muestran hasta seis presets por modo en el applet RX Controls. Los botones están ocultos para los modos FM, NFM y DFM.

## Ancho de filtro por pasos (v0.9.8)

El sistema de presets de ancho de filtro ahora admite un método `stepFilterWidth()` que recorre la lista de presets por modo. Esto permite atajos de ampliación/reducción que producen una geometría de bordes correcta para el modo en todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB).

Cuando aplica una operación de ampliación o reducción:

- AetherSDR encuentra el preset de ancho más cercano que coincida con la banda de paso del filtro actual.
- Luego selecciona el preset siguiente más ancho o más estrecho de la lista por modo.
- El preset se aplica a través de `applyFilterPreset()`, que utiliza los desplazamientos de borde correctos para el modo actual.

Esto garantiza que ampliar o reducir un filtro siempre se mantenga dentro de los valores de preset apropiados para el modo y produzca la geometría de banda de paso correcta.

## Formato de ancho de filtro (v0.9.8)

El método `formatFilterWidth()` ahora es una función estática pública, compartida con el panel VFO (`VfoWidget`). Esto garantiza que tanto el applet RX Controls como el panel VFO muestren lecturas de ancho de filtro idénticas. El método utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto (#2197).

## Comportamiento del squelch en modos NT y RTTY (v26.5.1)

El squelch está deshabilitado en el modo NT, el modo RTTY y los modos digitales existentes (`DIGU`, `DIGL`). Esto evita que el squelch bloquee señales FSK débiles y elimine caracteres, lo que interrumpiría la decodificación (#2504). Si el squelch estaba activo cuando cambió a RTTY o a un modo digital, AetherSDR lo desactiva automáticamente y guarda el estado para que pueda restaurarse cuando salga del modo. El botón y el deslizador del squelch permanecen deshabilitados mientras el modo está activo.

## Activación del modo RADE (v26.5.2.1)

RADE ("Reverse Adaptive Digital Enhancement" o un modo digital específico) es una etiqueta de modo solo del lado del cliente. Cuando selecciona RADE en el cuadro combinado de modos, AetherSDR establece el modo inmediatamente en el slice, pero la radio devuelve el modo real subyacente (DIGL o DIGU) en la siguiente actualización de estado. Debido a esto, la propiedad `mode()` interna del slice nunca será `"RADE"` después de que la radio responda.

Al cambiar del modo RADE a cualquier otro modo:

- AetherSDR verifica si el modo del slice era `"RADE"` antes de emitir la señal de desactivación `radeActivated(false)`.
- Debido a que la radio reemplaza RADE con DIGL/DIGU, `mode() == "RADE"` nunca es verdadero en el momento del cambio. Esto significa que la señal de desactivación no se emite al salir del modo RADE.

Para activar el modo RADE desde el código (por ejemplo, a través del combo VFO, la carga de perfil al inicio, o `MainWindow::activateRADE`), AetherSDR llama a la ruta de activación RADE interna directamente en lugar de confiar en el cambio de valor del combo de modo. Use el botón `Activate RADE` en el menú de modo o el sistema de perfiles para habilitar RADE.

## Persistencia del umbral de squelch manual (v26.5.2.1)

El deslizador del nivel de squelch ahora conserva el último valor manual elegido por el usuario entre sesiones. Esto es necesario porque el modo de squelch automático puede sobrescribir `squelchLevel` en el slice con valores sugeridos por el algoritmo, y la radio no conserva la preferencia manual del operador entre ciclos de modo o inicios de aplicación.

AetherSDR almacena el umbral manual en la configuración de la aplicación bajo la clave `LastManualSquelchLevel`. El valor se limita al rango válido de 0 a 100. En el primer inicio, el valor predeterminado es 20.

Cuando habilita el squelch y ajusta el deslizador, el nuevo valor se guarda inmediatamente. Cuando inicia una nueva sesión, el deslizador vuelve al último nivel manual guardado, no al valor predeterminado.

## Modo NT

La versión 0.9.3 agrega el modo `NT` junto con los modos digitales existentes (`DIGU`, `DIGL`). Se comporta de manera idéntica a otros modos digitales en los siguientes aspectos:

- **Presets de filtro** — NT comparte el conjunto de presets de filtro DIG (100–2000 Hz). La etiqueta de ancho de filtro se actualiza en consecuencia.
- **Cálculo del ancho de filtro** — La visualización del ancho de filtro mide el desplazamiento del borde superior, igual que USB y DIGU.
- **Squelch** — El botón SQL y el deslizador de squelch están deshabilitados en el modo NT. Debido a que el audio se enruta a través de DAX en los modos digitales, el squelch no tiene sentido. Si el squelch estaba activo cuando cambió al modo NT, AetherSDR lo desactiva automáticamente y lo restaura cuando sale del modo NT.

## Mejoras en la selección de antena (v26.5.2.1)

Los cuadros combinados de antena RX y TX ahora utilizan las listas de antenas por slice cuando están disponibles, en lugar de depender únicamente de la lista global de antenas de la radio. Esto proporciona opciones de antena más precisas, especialmente para slices en diferentes panadapters.

### Menú de antena RX

- Cuando el slice proporciona una `rxAntennaList()`, el menú muestra solo esos puertos de antena.
- Si el slice no proporciona una lista, se utiliza la `ant_list` global del estado del panadapter como respaldo.
- Cada acción del menú almacena el nombre del puerto de la antena en la propiedad de datos de la acción, lo que garantiza una selección correcta incluso cuando las etiquetas mostradas difieren de los nombres de los puertos.
- Los tooltips y las sugerencias de estado muestran el nombre del puerto de antena sin procesar para mayor claridad.

### Menú de antena TX

- El menú de antena TX se completa mediante una función auxiliar `txAntennaOptions()`.
- Esta función recopila antenas capaces de TX tanto de la lista global de antenas como de cualquier fuente adicional.
- Los puertos de antena solo RX (aquellos que comienzan con `RX` sin distinción de mayúsculas y minúsculas) se excluyen del menú.
- Los puertos de antena con los prefijos `ANT`, `TX` o la cadena exacta `XVTR` se consideran tokens de respaldo capaces de TX.

### Formato de visualización

Ambos menús de antena ahora usan una función auxiliar `antennaMenuLabel()` para formatear las etiquetas mostradas. La etiqueta incluye el nombre del puerto de la antena seguido de la información del rango de frecuencia entre paréntesis cuando está disponible, lo que facilita la identificación de qué antena seleccionar para una banda determinada.

## Formato de la insignia del slice (v26.5.2.1)

La etiqueta de la insignia del slice ahora admite renderizado de texto enriquecido (HTML). Esto permite que la letra del slice incluya formato, como caracteres en superíndice o subíndice, cuando la identidad del slice lo requiere (#2606). La insignia continúa usando el mismo esquema de color por slice y el tamaño fijo de 20x20 píxeles que antes.

## Mejoras en la entrada de frecuencia (v26.5.3)

El sistema de entrada de frecuencia ahora usa `FrequencyEntryParser::normalizedMhzText()` para el análisis y `FrequencyEntryParser::isExplicitMhzEntry()` para detectar entradas explícitas en MHz. Esto proporciona un manejo más robusto del formato de frecuencia y la detección de entrada.

### Entradas explícitas en MHz

Cuando ingresa un valor de frecuencia superior a 54.0 MHz en el campo de edición de frecuencia, AetherSDR verifica si es una entrada explícita en MHz. Si la entrada se detecta como explícitamente en MHz (por ejemplo, `146.520` o `446.000`), la radio permite sintonizar hasta 50,000 MHz, lo que permite el acceso directo a las bandas VHF/UHF/SHF sin requerir una antena XVTR. Esto es particularmente útil para ingresar frecuencias de las bandas de 2m, 70cm o superiores directamente.

### Normalización de la frecuencia de entrada

La función `normalizedMhzText()` limpia el texto de frecuencia ingresado eliminando puntos y caracteres de formato superfluos. Esto asegura que entradas como `14.250.000` (con puntos de agrupación de dígitos) se analicen correctamente como `14.250000` MHz.

### Conveniencia de banda de 3 dígitos

Para slices XVTR (o cuando la frecuencia está por encima de 54 MHz), el sistema aplica la lógica de conveniencia de banda de 3 dígitos: una entrada como `1446` se interpreta como 144.6 MHz (para la banda de 2m), mientras que las entradas para bandas de 23cm/microondas (por ejemplo, `1296`) se tratan como valores directos en MHz. Esta lógica solo se aplica cuando la entrada no es una entrada explícita en MHz.

### Escape para cancelar (v0.9.0)

Presionar Escape mientras el editor de frecuencia está activo cancela la edición, restaura la frecuencia anterior y descarta el editor (Corregido en v0.9.0, #1954).

## Comportamiento del botón de silencio (v26.5.3)

El botón de silencio (🔊 / 🔇) ahora usa discriminación de clic único basada en temporizador. Esto proporciona una detección de doble clic más confiable para silenciar/activar el sonido de todos los slices propios.

### Clic único

Un clic único inicia un temporizador configurado al intervalo de doble clic de la plataforma (~400 ms). Cuando el temporizador expira, el estado de silencio del slice actual se alterna.

### Doble clic

Un doble clic cancela inmediatamente el temporizador de clic único y emite `muteAllToggled`, que silencia o reactiva el sonido de todos los slices propiedad del cliente actual. La segunda pulsación de la secuencia de doble clic no produce una señal `clicked()` separada porque el filtro de eventos intercepta el evento `MouseButtonDblClick` y devuelve verdadero, impidiendo que se ejecute `QAbstractButton::mouseDoubleClickEvent`.

### Actualización del icono

El icono del botón de silencio (🔊 o 🔇) se actualiza solo cuando la radio reconoce el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`. Esto asegura que el icono siempre refleje el estado autoritativo de la radio, según lo requiere la Política de Configuración Autoritativa de la Radio (#2489).

### Persistencia del estado

El estado de silencio NO se guarda ni se restaura al reconectar. La radio es siempre la fuente de verdad para el estado de silencio de audio.

## Marca central del deslizador panorámico L/R (v26.6.1)

El deslizador panorámico L/R ahora dibuja un pequeño punto de marca central en la ranura. Esto proporciona una referencia visual para la posición neutral (centro), lo que facilita la identificación de cuándo el paneo está centrado.

### Cómo funciona el relleno

El relleno del deslizador está anclado desde el centro hacia afuera:

- Cuando el mango está a la izquierda del centro, la sección de subpágina entre el mango y el centro se pinta en el color de acento.
- Cuando el mango está a la derecha del centro, la sección de subpágina entre el centro y el mango se pinta en el color de acento, y la sección
