# Bloquear el slice para evitar cambios de sintonía accidentales

La función de bloqueo de sintonía evita que un slice responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin el riesgo de modificar el VFO al hacer clic en el panadapter o al desplazarse con la rueda del mouse.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa con la radio.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX de la barra lateral derecha para mostrarlo.

## Pasos

1. En el applet RX Controls, identifique la fila de encabezado que contiene la insignia del slice, el botón de bloqueo y los selectores de antena.
2. Si tiene más de un slice, haga clic en la pestaña del slice correspondiente (A a la H) para seleccionar el slice que desea bloquear.
3. Haga clic en el botón 🔓 en la fila de encabezado. El ícono cambia a 🔒 y se vuelve azul, lo que confirma que el slice está bloqueado.
4. Para desbloquear, haga clic en 🔒 nuevamente. El ícono vuelve a 🔓 y el slice reanuda la respuesta a los cambios de frecuencia.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento                                                                                                           |
|---------|----------------------|--------------------------------------------------------------------------------------------------------------------------|
| 🔓 / 🔒   | 🔓 (desbloqueado)     | Alterna el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los cambios de frecuencia. Haga clic nuevamente para desbloquear. |

## Consejos

- El estado de bloqueo se aplica por slice. Puede bloquear el slice A mientras el slice B permanece libremente sintonizable.
- El botón de bloqueo siempre está visible en la fila de encabezado, independientemente del modo actual.
- A partir de la v0.9.3, los botones de pestaña del slice y la insignia del slice utilizan colores por slice administrados por SliceColorManager. Los colores se pueden personalizar por slice y persisten entre sesiones. El mismo color se refleja en los botones de pestaña del slice, la insignia del slice, los widgets de VFO y las barras de medidor.

## Comportamiento de las pestañas del slice al reconectar (v0.9.5.1)

Cuando la radio se desconecta o la cantidad de slices disponibles cambia, AetherSDR ahora elimina todos los botones de pestaña de slice generados y restaura automáticamente la insignia de slice estática (`clearSliceButtons()`, #2254). Al reconectar, la fila de pestañas se reconstruye para que coincida con la nueva cantidad de slices. Si la cantidad no ha cambiado, los botones existentes se reutilizan sin reconstrucción.

Las conexiones de señal entre el grupo de botones de slice y el controlador `sliceActivationRequested` están protegidas para que la reconexión a la radio no acumule controladores de señal duplicados.

## Formato de almacenamiento de preajustes de filtro (v0.9.5.1)

Los preajustes de filtro guardados para un modo determinado (clave de configuración `FilterPresets`) ahora admiten dos formatos de almacenamiento:

- **Solo ancho** — un número entero simple que representa el ancho de banda del filtro en Hz (por ejemplo, `2700`). Este es el formato heredado y sigue funcionando.
- **Lo:Hi** — un par separado por dos puntos de los desplazamientos de borde inferior y superior en Hz (por ejemplo, `-1400:1300`). Este formato preserva una banda de paso asimétrica exactamente como la configuró al arrastrar los bordes del widget de la banda de paso del filtro.

Cuando hace clic derecho en un botón de preajuste de filtro para guardar el ancho actual, AetherSDR escribe el formato `lo:hi` cuando la banda de paso es asimétrica (#2259). Los preajustes guardados en el formato antiguo de solo ancho se leen y aplican como bandas de paso centradas, exactamente como antes.

Se almacenan y muestran hasta seis preajustes por modo en el applet RX Controls. Los botones están ocultos para los modos FM, NFM y DFM.

## Ancho de filtro por pasos (v0.9.8)

El sistema de preajustes de ancho de filtro ahora admite un método `stepFilterWidth()` que recorre la lista de preajustes por modo. Esto permite accesos directos para ensanchar/reducir que producen la geometría de borde correcta según el modo para todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB).

Cuando aplica una operación de ensanchar o reducir:

- AetherSDR encuentra el preajuste de ancho más cercano a la banda de paso del filtro actual.
- Luego selecciona el siguiente preajuste más ancho o más estrecho de la lista por modo.
- El preajuste se aplica a través de `applyFilterPreset()`, que utiliza los desplazamientos de borde correctos para el modo actual.

Esto garantiza que ensanchar o reducir un filtro siempre se mantenga dentro de los valores de preajuste apropiados para el modo y produzca la geometría de banda de paso correcta.

## Formato del ancho del filtro (v0.9.8)

El método `formatFilterWidth()` ahora es una función pública estática, compartida con el panel VFO (`VfoWidget`). Esto garantiza que tanto el applet RX Controls como el panel VFO muestren lecturas de ancho de filtro idénticas. El método utiliza lógica adaptada al modo para que los modos SSB y digitales muestren el ancho etiquetado correcto (#2197).

## Comportamiento del squelch en modos NT y RTTY (v26.5.1)

El squelch está deshabilitado en el modo NT, el modo RTTY y los modos digitales existentes (`DIGU`, `DIGL`). Esto evita que el squelch bloquee señales FSK débiles y recorte caracteres, lo que rompería la decodificación (#2504). Si el squelch estaba activo cuando cambió a RTTY o a un modo digital, AetherSDR lo desactiva automáticamente y guarda el estado para que pueda restaurarse cuando salga del modo. El botón y el control deslizante de squelch permanecen deshabilitados mientras el modo esté activo.

## Activación del modo RADE (v26.5.2.1)

RADE ("Reverse Adaptive Digital Enhancement" o un modo digital específico) es una etiqueta de modo solo del lado del cliente. Cuando selecciona RADE en el cuadro combinado de modos, AetherSDR establece el modo inmediatamente en el slice, pero la radio devuelve el modo real subyacente (DIGL o DIGU) en la siguiente actualización de estado. Debido a esto, la propiedad `mode()` interna del slice nunca será `"RADE"` después de que la radio responda.

Al cambiar del modo RADE a cualquier otro modo:

- AetherSDR verifica si el modo del slice era `"RADE"` antes de emitir la señal de desactivación `radeActivated(false)`.
- Debido a que la radio anula RADE con DIGL/DIGU, `mode() == "RADE"` nunca es verdadero en el momento del cambio. Esto significa que la señal de desactivación no se emite al cambiar de RADE.

Para activar el modo RADE desde el código (por ejemplo, a través del cuadro combinado VFO, la carga de perfil al inicio o `MainWindow::activateRADE`), AetherSDR llama a la ruta de activación RADE interna directamente en lugar de depender del cambio de valor del cuadro combinado de modos. Use el botón `Activate RADE` en el menú de modos o el sistema de perfiles para habilitar RADE.

## Persistencia del umbral manual de squelch (v26.5.2.1)

El control deslizante de nivel de squelch ahora conserva el último valor manual elegido por el usuario entre sesiones. Esto es necesario porque el modo de squelch automático puede sobrescribir el `squelchLevel` en el slice con valores sugeridos por el algoritmo, y la radio no conserva la preferencia manual del operador entre ciclos de modo o inicios de aplicación.

AetherSDR almacena el umbral manual en la configuración de la aplicación bajo la clave `LastManualSquelchLevel`. El valor se limita al rango válido de 0 a 100. En el primer inicio, el valor predeterminado es 20.

Cuando habilita el squelch y ajusta el control deslizante, el nuevo valor se guarda inmediatamente. Cuando inicia una nueva sesión, el control deslizante vuelve al último nivel manual guardado en lugar del valor predeterminado.

## Modo NT

La versión 0.9.3 agrega el modo `NT` junto con los modos digitales existentes (`DIGU`, `DIGL`). Se comporta de manera idéntica a otros modos digitales en los siguientes aspectos:

- **Preajustes de filtro** — NT comparte el conjunto de preajustes de filtro DIG (100–2000 Hz). La etiqueta de ancho de filtro se actualiza en consecuencia.
- **Cálculo del ancho del filtro** — La visualización del ancho del filtro mide el desplazamiento del borde superior, igual que USB y DIGU.
- **Squelch** — El botón SQL y el control deslizante de squelch están deshabilitados en el modo NT. Debido a que el audio se enruta a través de DAX en los modos digitales, el squelch no es significativo. Si el squelch estaba activo cuando cambió al modo NT, AetherSDR lo desactiva automáticamente y lo restaura cuando sale del modo NT.

## Mejoras en la selección de antena (v26.5.2.1)

Los cuadros combinados de antena RX y TX ahora utilizan las listas de antenas por slice cuando están disponibles, en lugar de depender únicamente de la lista global de antenas de la radio. Esto proporciona opciones de antena más precisas, especialmente para slices en diferentes panadapters.

### Menú de antena RX

- Cuando el slice proporciona una `rxAntennaList()`, el menú muestra solo esos puertos de antena.
- Si el slice no proporciona una lista, se utiliza la `ant_list` global del estado del panadapter como respaldo.
- Cada acción del menú almacena el nombre del puerto de antena en la propiedad de datos de la acción, lo que garantiza una selección correcta incluso cuando las etiquetas mostradas difieren de los nombres de los puertos.
- La información sobre herramientas y las sugerencias de estado muestran el nombre del puerto de antena sin procesar para mayor claridad.

### Menú de antena TX

- El menú de antena TX se completa mediante una función auxiliar `txAntennaOptions()`.
- Esta función recopila antenas con capacidad TX tanto de la lista global de antenas como de cualquier fuente adicional.
- Los puertos de antena solo RX (aquellos que comienzan con `RX` sin distinción entre mayúsculas y minúsculas) se excluyen del menú.
- Los puertos de antena con los prefijos `ANT`, `TX` o la cadena exacta `XVTR` se consideran tokens de respaldo con capacidad TX.

### Formato de visualización

Ambos menús de antena ahora utilizan una función auxiliar `antennaMenuLabel()` para formatear las etiquetas mostradas. La etiqueta incluye el nombre del puerto de antena seguido de información del rango de frecuencia entre paréntesis cuando está disponible, lo que facilita la identificación de qué antena seleccionar para una banda determinada.

## Formato de la insignia del slice (v26.5.2.1)

La etiqueta de la insignia del slice ahora admite la representación de texto enriquecido (HTML). Esto permite que la letra del slice incluya formato, como caracteres en superíndice o subíndice, cuando la identidad del slice lo requiere (#2606). La insignia continúa usando el mismo esquema de color por slice y el tamaño fijo de 20x20 píxeles que antes.

## Relacionado

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
