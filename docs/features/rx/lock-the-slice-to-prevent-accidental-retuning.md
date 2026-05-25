# Bloquear la franja para evitar cambios accidentales de sintonía

La función de bloqueo de sintonía evita que una franja responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin el riesgo de modificar el VFO al hacer clic en el panadapter o desplazar la rueda del mouse.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión de radio activa.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX de la barra lateral derecha para mostrarlo.

## Pasos

1. En el applet RX Controls, identifique la fila de encabezado que contiene la insignia de la franja, el botón de bloqueo y los selectores de antena.
2. Si tiene más de una franja, haga clic en la pestaña de franja correspondiente (A a H) para seleccionar la franja que desea bloquear.
3. Haga clic en el botón 🔓 en la fila de encabezado. El ífono cambia a 🔒 y se vuelve azul, confirmando que la franja está bloqueada.
4. Para desbloquear, haga clic en 🔒 nuevamente. El ícono vuelve a 🔓 y la franja reanuda la respuesta a los cambios de frecuencia.

## Función de cada control

| Control | Valor predeterminado | Comportamiento                                                                                                           |
|---------|----------------------|--------------------------------------------------------------------------------------------------------------------------|
| 🔓 / 🔒   | 🔓 (desbloqueado)    | Activa o desactiva el bloqueo de sintonía en la franja activa. Cuando está bloqueada (🔒), la franja ignora todos los cambios de frecuencia. Vuelva a hacer clic para desbloquear. |

## Consejos

- El estado de bloqueo se aplica por franja. Puede bloquear la franja A mientras la franja B permanece libremente sintonizable.
- El botón de bloqueo siempre está visible en la fila de encabezado, independientemente del modo actual.
- Desde la v0.9.3, los botones de pestaña de franja y la insignia de franja usan colores por franja gestionados por SliceColorManager. Los colores son personalizables por franja y persisten entre sesiones. El mismo color se refleja en los botones de pestaña de franja, la insignia de franja, los widgets de VFO y las tiras de medidor.

## Comportamiento de las pestañas de franja al reconectar (v0.9.5.1)

Cuando la radio se desconecta o el número de franjas disponibles cambia, AetherSDR ahora elimina todos los botones de pestaña de franja generados y restaura automáticamente la insignia de franja estática (`clearSliceButtons()`, #2254). Al reconectar, la fila de pestañas se reconstruye para coincidir con el nuevo número de franjas. Si el número no ha cambiado, los botones existentes se reutilizan sin reconstrucción.

Las conexiones de señal entre el grupo de botones de franja y el controlador `sliceActivationRequested` están protegidas para que la reconexión a la radio no acumule controladores de señal duplicados.

## Formato de almacenamiento de preselecciones de filtro (v0.9.5.1)

Las preselecciones de filtro guardadas para un modo determinado (clave de configuración `FilterPresets`) ahora admiten dos formatos de almacenamiento:

- **Solo ancho** — un número entero que representa el ancho de banda del filtro en Hz (por ejemplo, `2700`). Este es el formato heredado y sigue funcionando.
- **Lo:Hi** — un par de desplazamientos de borde inferior y borde superior en Hz separados por dos puntos (por ejemplo, `-1400:1300`). Este formato conserva una banda de paso asimétrica exactamente como la configuró arrastrando los bordes del widget de banda de paso del filtro.

Al hacer clic derecho en un botón de preselección de filtro para guardar el ancho actual, AetherSDR escribe la forma `lo:hi` cuando la banda de paso es asimétrica (#2259). Las preselecciones guardadas en el formato antiguo de solo ancho se leen y aplican como bandas de paso centradas, exactamente como antes.

Se almacenan y muestran hasta seis preselecciones por modo en el applet RX Controls. Los botones están ocultos para los modos FM, NFM y DFM.

## Ancho de filtro por pasos (v0.9.8)

El sistema de preselecciones de ancho de filtro ahora admite un método `stepFilterWidth()` que recorre la lista de preselecciones por modo. Esto permite accesos directos de ampliación/reducción que producen una geometría de bordes correcta para el modo en todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB).

Al aplicar una operación de ampliación o reducción:

- AetherSDR encuentra la preselección de ancho más cercana a la banda de paso del filtro actual.
- Luego selecciona la preselección siguiente más ancha o más estrecha de la lista por modo.
- La preselección se aplica a través de `applyFilterPreset()`, que utiliza los desplazamientos de borde correctos para el modo actual.

Esto garantiza que ampliar o reducir un filtro siempre se mantenga dentro de los valores de preselección apropiados para el modo y produzca la geometría de banda de paso correcta.

## Formato del ancho del filtro (v0.9.8)

El método `formatFilterWidth()` ahora es una función estática pública, compartida con el panel VFO (`VfoWidget`). Esto garantiza que tanto el applet RX Controls como el panel VFO muestren lecturas de ancho de filtro idénticas. El método utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto (#2197).

## Comportamiento del squelch en modo NT y RTTY (v26.5.1)

El squelch está deshabilitado en modo NT, modo RTTY y los modos digitales existentes (`DIGU`, `DIGL`). Esto evita que el squelch bloquee señales FSK débiles y recorte caracteres, lo que interrumpiría la decodificación (#2504). Si el squelch estaba activo al cambiar a RTTY o un modo digital, AetherSDR lo desactiva automáticamente y guarda el estado para que pueda restaurarse al salir del modo. El botón y el deslizador de squelch permanecen deshabilitados mientras el modo esté activo.

## Activación del modo RADE (v26.5.2.1)

RADE ("Reverse Adaptive Digital Enhancement" o un modo digital específico) es una etiqueta de modo solo del lado del cliente. Al seleccionar RADE en el cuadro combinado de modos, AetherSDR establece el modo inmediatamente en la franja, pero la radio devuelve el modo real subyacente (DIGL o DIGU) en la siguiente actualización de estado. Debido a esto, la propiedad interna `mode()` de la franja nunca será `"RADE"` después de que la radio responda.

Al cambiar del modo RADE a cualquier otro modo:

- AetherSDR verifica si el modo de la franja era `"RADE"` antes de emitir la señal de desactivación `radeActivated(false)`.
- Debido a que la radio reemplaza RADE con DIGL/DIGU, `mode() == "RADE"` nunca es verdadero en el momento del cambio. Esto significa que la señal de desactivación no se emite al cambiar de RADE.

Para activar el modo RADE desde el código (por ejemplo, a través del cuadro combinado VFO, la carga de perfil al inicio o `MainWindow::activateRADE`), AetherSDR llama directamente a la ruta de activación RADE interna en lugar de depender del cambio de valor del cuadro combinado de modos. Use el botón `Activate RADE` en el menú de modos o el sistema de perfiles para habilitar RADE.

## Persistencia del umbral de squelch manual (v26.5.2.1)

El deslizador de nivel de squelch ahora conserva el último valor manual elegido por el usuario entre sesiones. Esto es necesario porque el modo de squelch automático puede sobrescribir `squelchLevel` en la franja con valores sugeridos por el algoritmo, y la radio no conserva la preferencia manual del operador entre ciclos de modo o inicios de aplicación.

AetherSDR almacena el umbral manual en la configuración de la aplicación bajo la clave `LastManualSquelchLevel`. El valor se limita al rango válido de 0 a 100. En el primer inicio, el valor predeterminado es 20.

Al habilitar el squelch y ajustar el deslizador, el nuevo valor se guarda inmediatamente. Al iniciar una nueva sesión, el deslizador vuelve al último nivel manual guardado en lugar del valor predeterminado.

## Modo NT

La versión 0.9.3 agrega el modo `NT` junto a los modos digitales existentes (`DIGU`, `DIGL`). Se comporta de manera idéntica a otros modos digitales en los siguientes aspectos:

- **Preselecciones de filtro** — NT comparte el conjunto de preselecciones de filtro DIG (100–2000 Hz). La etiqueta de ancho de filtro se actualiza en consecuencia.
- **Cálculo del ancho de filtro** — La visualización del ancho de filtro mide el desplazamiento del borde superior, igual que USB y DIGU.
- **Squelch** — El botón SQL y el deslizador de squelch están deshabilitados en modo NT. Debido a que el audio se enruta a través de DAX en modos digitales, el squelch no tiene sentido. Si el squelch estaba activo al cambiar al modo NT, AetherSDR lo desactiva automáticamente y lo restaura al salir del modo NT.

## Mejoras en la selección de antena (v26.5.2.1)

Los cuadros combinados de antena RX y TX ahora utilizan las listas de antenas por franja cuando están disponibles, en lugar de depender únicamente de la lista global de antenas de la radio. Esto proporciona opciones de antena más precisas, especialmente para franjas en diferentes panadapters.

### Menú de antena RX

- Cuando la franja proporciona una `rxAntennaList()`, el menú muestra solo esos puertos de antena.
- Si la franja no proporciona una lista, se utiliza la `ant_list` global del estado del panadapter como alternativa.
- Cada acción del menú almacena el nombre del puerto de antena en la propiedad de datos de la acción, lo que garantiza una selección correcta incluso cuando las etiquetas de visualización difieren de los nombres de los puertos.
- La información sobre herramientas y las sugerencias de estado muestran el nombre del puerto de antena sin procesar para mayor claridad.

### Menú de antena TX

- El menú de antena TX se completa con una función auxiliar `txAntennaOptions()`.
- Esta función recopila antenas capaces de TX tanto de la lista global de antenas como de fuentes adicionales.
- Los puertos de antena solo RX (los que comienzan con `RX` sin distinción entre mayúsculas y minúsculas) se excluyen del menú.
- Los puertos de antena con prefijos `ANT`, `TX` o la cadena exacta `XVTR` se consideran tokens alternativos capaces de TX.

### Formato de visualización

Ambos menús de antena ahora utilizan una función auxiliar `antennaMenuLabel()` para formatear las etiquetas de visualización. La etiqueta incluye el nombre del puerto de antena seguido de información del rango de frecuencia entre paréntesis cuando está disponible, lo que facilita la identificación de qué antena seleccionar para una banda determinada.

## Formato de la insignia de franja (v26.5.2.1)

La etiqueta de la insignia de franja ahora admite representación de texto enriquecido (HTML). Esto permite que la letra de la franja incluya formato, como caracteres en superíndice o subíndice, cuando la identidad de la franja lo requiera (#2606). La insignia continúa usando el mismo esquema de color por franja y el tamaño fijo de 20x20 píxeles que antes.

## Mejoras en la entrada de frecuencia (v26.5.3)

El sistema de entrada de frecuencia ahora utiliza `FrequencyEntryParser::normalizedMhzText()` para el análisis y `FrequencyEntryParser::isExplicitMhzEntry()` para detectar entradas explícitas en MHz. Esto proporciona un manejo más robusto del formato de frecuencia y la detección de entrada.

### Entradas explícitas en MHz

Al ingresar un valor de frecuencia superior a 54.0 MHz en el campo de edición de frecuencia, AetherSDR verifica si se trata de una entrada explícita en MHz. Si la entrada se detecta como explícitamente en MHz (por ejemplo, `146.520` o `446.000`), la radio permite sintonizar hasta 50,000 MHz, lo que permite el acceso directo a las bandas VHF/UHF/SHF sin necesidad de una antena XVTR. Esto es particularmente útil para ingresar frecuencias de las bandas de 2m, 70cm o superiores directamente.

### Normalización de frecuencia de entrada

La función `normalizedMhzText()` limpia el texto de frecuencia ingresado eliminando puntos superfluos y caracteres de formato. Esto garantiza que entradas como `14.250.000` (con puntos de agrupación de dígitos) se analicen correctamente como `14.250000` MHz.

### Conveniencia de banda de 3 dígitos

Para franjas XVTR (o cuando la frecuencia supera los 54 MHz), el sistema aplica la lógica de conveniencia de banda de 3 dígitos: una entrada como `1446` se interpreta como 144.6 MHz (para la banda de 2m), mientras que las entradas para bandas de 23cm/microondas (por ejemplo, `1296`) se tratan como valores directos en MHz. Esta lógica solo se aplica cuando la entrada no es una entrada explícita en MHz.

### Escape para cancelar (v0.9.0)

Pulsar Escape mientras el editor de frecuencia está activo cancela la edición, restaura la frecuencia anterior y descarta el editor (Corregido en v0.9.0, #1954).

## Comportamiento del botón de silencio (v26.5.3)

El botón de silencio (🔊 / 🔇) ahora utiliza discriminación de clic único basada en temporizador. Esto proporciona una detección de doble clic más confiable para silenciar o reactivar el sonido de todas las franjas propias.

### Clic único

Un clic único inicia un temporizador configurado en el intervalo de doble clic de la plataforma (~400 ms). Cuando el temporizador expira, el estado de silencio de la franja actual se alterna.

### Doble clic

Un doble clic cancela inmediatamente el temporizador de clic único y emite `muteAllToggled`, que silencia o reactiva el sonido de todas las franjas propiedad del cliente actual. La segunda pulsación de la secuencia de doble clic no produce una señal `clicked()` separada porque el filtro de eventos intercepta el evento `MouseButtonDblClick` y devuelve verdadero, evitando que se ejecute `QAbstractButton::mouseDoubleClickEvent`.

### Actualización del ícono

El ícono del botón de silencio (🔊 o 🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`. Esto garantiza que el ícono refleje siempre el estado autoritativo de la radio, según lo requiere la Política de Configuración Autoritativa de la Radio (#2489).

### Persistencia del estado

El estado de silencio NO se guarda ni restaura al reconectar. La radio es siempre la fuente de verdad para el estado de silencio de audio.

## Relacionado

- [Cambiar entre múltiples franjas usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprensión de franjas y VFOs](../../getting-started/concepts/understanding-slices.md)
