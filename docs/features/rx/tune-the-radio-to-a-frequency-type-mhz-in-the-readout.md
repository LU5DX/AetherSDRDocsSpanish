# Sintonizar la radio a una frecuencia (escriba MHz en el indicador)

Escriba una frecuencia directamente en el applet de Controles RX para mover el VFO de la franja activa a cualquier frecuencia dentro del rango de sintonización de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet de Controles RX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Asegúrese de que la franja que desea sintonizar no esté bloqueada. Si el icono de bloqueo muestra 🔒, haga clic en él para desbloquearla antes de continuar (consulte [Lock the slice to prevent accidental retuning](lock-the-slice-to-prevent-accidental-retuning.md)).

## Pasos

1. Si tiene más de una franja, haga clic en la pestaña de franja correspondiente (**A**, **B**, **C**, etc.) en la parte superior del applet de Controles RX para seleccionar la franja que desea sintonizar.
2. Haga clic en la **Etiqueta de frecuencia** (el indicador punteado, p. ej. `0.000.000`). Cambia al modo de edición, convirtiéndose en el campo **Edición de frecuencia**.
3. Escriba la frecuencia deseada en MHz. Por ejemplo, escriba `14.225` para 14.225 MHz.
4. Presione **Enter**. La franja se sintoniza a la frecuencia introducida y el panadapter la centra.

Para cancelar sin cambiar la frecuencia, presione **Escape**. El editor se cierra y se restaura la frecuencia anterior.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| **Pestañas de franja (A..H)** | Selecciona a qué franja está vinculado el applet RX. Fila oculta si la radio solo admite una franja. | — |
| **Distintivo de franja** | Muestra la letra de la franja actualmente vinculada, coloreada por identidad de franja. Soporta renderizado HTML para etiquetas de franja personalizadas (#2606). | A |
| **🔓 / 🔒** | Activa/desactiva el bloqueo de sintonía en la franja. Las franjas bloqueadas ignoran los cambios de frecuencia. | 🔓 (desbloqueado) |
| **ANT1 (antena RX)** | Abre un menú que lista las antenas RX disponibles. Utiliza la lista de antenas RX dedicada de la franja cuando está disponible; recurre a la lista de antenas de la radio. | ANT1 |
| **ANT1 (antena TX)** | Abre un menú que lista las antenas con capacidad TX. Filtra los puertos solo RX (prefijo 'RX') e incluye puertos ANT, TX y XVTR. | ANT1 |
| **2.7K (ancho de filtro)** | Muestra el ancho de banda del filtro actual (p. ej. 2.7K, 3.3K, 500). | 2.7K |
| **QSK** | Se ilumina en ámbar cuando el QSK (CW break-in) está activo. Solo lectura; se controla mediante el applet CW. | apagado (gris) |
| **TX (distintivo)** | Haga clic para establecer esta franja como la franja TX. | — |
| **Combinación de modo** | Establece el modo de operación de la franja. Las opciones varían según la radio y las banderas de compilación. La opción RADE requiere la bandera de compilación HAVE_RADE. | USB |
| **Etiqueta de frecuencia** | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para entrar en modo de edición. | `0.000.000` |
| **Edición de frecuencia** | Campo de texto. Introduzca la frecuencia en MHz y presione Enter para sintonizar y centrar. Escape cancela y restaura la frecuencia anterior. | — |
| **PASO** | Establece el tamaño de paso utilizado al ajustar la frecuencia con los botones de flecha o la rueda del ratón. La lista de pasos depende del modo. | 100 Hz |
| **Preajustes de ancho de filtro** | Haga clic en un botón de preajuste para aplicar ese ancho de banda de filtro. Haga clic derecho para guardar el ancho actual en esa ranura. Oculto en modos FM/NFM/DFM. | — |
| **Widget de banda pasante del filtro** | Arrastre los bordes inferior/superior para ajustar la banda pasante del filtro directamente. | — |
| **Modo de tono (FM)** | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Off |
| **Valor de tono CTCSS** | Selecciona la frecuencia de tono CTCSS enviada en transmisión. Habilitado solo cuando Tone mode = CTCSS TX. | — |
| **Offset (FM)** | Establece la frecuencia de offset del repetidor FM en MHz (0.0–100.0 MHz, paso 0.1). | 0.0 MHz |
| **− (offset descendente)** | Establece la dirección del offset del repetidor a 'descendente' (TX por debajo de RX). | — |
| **Simplex** | Establece la dirección del offset del repetidor a simplex (TX = RX). | marcado |
| **+ (offset ascendente)** | Establece la dirección del offset del repetidor a 'ascendente' (TX por encima de RX). | — |
| **REV** | Invierte el signo del offset TX para trabajar un par de repetidores invertido. | — |
| **🔊 / 🔇 (silencio)** | Silencia o reactiva la salida de audio de la franja. El estado de silencio NO se guarda/restaura al reconectar: la radio es la fuente de verdad. | 🔊 (sin silencio) |
| **Ganancia AF** | Ajusta la ganancia de salida de audio de la franja (0–100). | 70 |
| **Panorámica L / R** | Desplaza el audio de la franja entre los canales izquierdo y derecho (0–100). Doble clic restablece a 50 (centro). | 50 |
| **SQL** | Activa el squelch en el nivel actual del deslizador. Deshabilitado en modos RTTY y digitales (DIGU, DIGL, NT) donde el squelch recortaría los caracteres FSK. | — |
| **Nivel de squelch** | Ajusta el umbral de squelch (0–100). Solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. El nivel manual persiste entre sesiones. | 20 |
| **Modo AGC** | Establece el modo AGC de la franja: Off, Slow, Med, Fast. Oculto en modos de la familia FM. | Med |
| **Umbral AGC** | Establece el umbral AGC (o el nivel de AGC-off cuando el modo AGC es Off). | 65 |
| **RIT** | Activa/desactiva la sintonización incremental de recepción. | — |
| **RIT 0** | Pone a cero el offset RIT. | — |
| **Offset RIT** | Ajusta el offset RIT en pasos de 10 Hz usando los botones de flecha o la rueda del ratón. | +0 Hz |
| **XIT** | Activa/desactiva la sintonización incremental de transmisión. | — |
| **XIT 0** | Pone a cero el offset XIT. | — |
| **Offset XIT** | Ajusta el offset XIT en pasos de 10 Hz usando los botones de flecha o la rueda del ratón. | +0 Hz |

## Avance de ancho de filtro

Desde v0.9.8, el applet admite un avance preciso del ancho de filtro corregido por modo a través de la lista de preajustes por modo. El método `stepFilterWidth()` recorre la lista de preajustes para el modo actual, encuentra el preajuste más cercano al ancho de filtro actual y aplica el siguiente o anterior preajuste en la dirección elegida.

Esto significa que:

- Los atajos para ensanchar y estrechar producen anchos de filtro que coinciden con la lista de preajustes del modo actual (SSB, CW, AM, digital, etc.).
- La actualización del ancho de filtro utiliza `applyFilterPreset()`, que calcula la geometría correcta del borde inferior y superior para el modo (USB, LSB, CWL, CZU, DIGL, DIGU, RTTY, AM, SAM, etc.).
- No se produce ningún cambio de filtro si la franja no tiene anchos de filtro configurados o si el ancho actual ya es igual al ancho objetivo.

El indicador de ancho de filtro (compartido con VfoWidget mediante `RxApplet::formatFilterWidth`) utiliza una lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

## Colores de pestañas y distintivo de franja

Desde v0.9.3, los botones de pestañas de franja y el indicador **Distintivo de franja** toman su borde, fondo activo y color de texto del singleton SliceColorManager en lugar de una tabla de colores fija. Los colores son configurables por franja, persisten entre sesiones y se reflejan de manera consistente en los botones de pestañas de franja, el distintivo de franja, los widgets VFO y las barras de medidor.

Desde v26.5.2.1, el **Distintivo de franja** admite renderizado HTML (`setTextFormat(Qt::RichText)`), permitiendo etiquetas de franja personalizadas con formato de texto enriquecido.

## Comportamiento de la fila de pestañas de franja al reconectar

Desde v0.9.5.1, la fila de pestañas de franja se reconstruye correctamente cada vez que cambia el número de franjas disponibles — por ejemplo, después de una desconexión y reconexión o cuando la radio informa un número diferente de franjas. La implementación anterior omitía la reconstrucción si ya existían botones de pestaña, lo que podía dejar botones obsoletos en pantalla.

El comportamiento actualizado funciona de la siguiente manera:

- Si el nuevo número de franjas coincide con el número de botones de pestaña existentes, la fila no se modifica.
- Si los números difieren, los botones de pestaña existentes se eliminan (`clearSliceButtons()`) antes de crear nuevos botones.
- Al eliminar, la fila de pestañas se oculta y se restaura el **Distintivo de franja** estático.
- La conexión de señal que asigna los clics de botón a `sliceActivationRequested` se establece solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de manejadores de señal duplicados en las reconexiones.

No se requiere ninguna acción del usuario para aprovechar esta corrección. La fila de pestañas se actualiza automáticamente.

## Formato de almacenamiento de preajustes de ancho de filtro

Desde v0.9.5.1, los preajustes de ancho de filtro pueden almacenar un valor de ancho de banda simple o un par explícito de borde inferior/borde superior. Esto coincide con el formato de almacenamiento utilizado por VfoWidget y permite que los preajustes guardados desde VfoWidget se carguen correctamente en el applet de Controles RX.

La configuración `FilterPresets` para cada modo (almacenada bajo la clave `FilterPresets_<mode>`, p. ej. `FilterPresets_USB`) acepta una lista separada por comas de entradas en cualquiera de los siguientes formatos:

| Formato | Ejemplo | Significado |
|---|---|---|
| `width` | `2700` | Ancho de banda en Hz; los bordes se calculan a partir de la alineación predeterminada del modo. |
| `lo:hi` | `-1350:1350` | Bordes de banda pasante explícitos en Hz relativos a la portadora. Ambos valores deben ser enteros y `hi` debe ser mayor que `lo`. |

Las entradas que no se ajustan a ninguno de los formatos, o donde `hi <= lo`, se omiten silenciosamente. El applet carga un máximo de seis preajustes por modo.

Normalmente no es necesario editar estos valores manualmente. Al hacer clic derecho en un botón de **Preajustes de ancho de filtro** se guarda el ancho de filtro actual en esa ranura utilizando el formato apropiado automáticamente.

## Modo NT

v0.9.3 añade el modo **NT** al selector de modos. NT se comporta como un modo digital de las siguientes maneras:

- Utiliza los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El ancho de filtro se calcula a partir del valor del borde superior (igual que USB, DIGU y FDV).
- El botón **SQL** y el deslizador de nivel de squelch están deshabilitados mientras NT está activo, y cualquier squelch activo se desactiva automáticamente (mismo comportamiento que DIGU y DIGL).

## Comportamiento de los modos RTTY y RADE

Desde v26.5.1:

- **Modo RTTY** ahora está incluido en la lógica de desactivación de squelch junto con DIGU, DIGL y NT. Cuando cambia al modo RTTY, el botón **SQL** y el deslizador de nivel de squelch se deshabilitan, y cualquier squelch activo se desactiva automáticamente. Esto evita que el squelch recorte los caracteres FSK y rompa la decodificación.
- **Modo RADE** — RADE se maneja solo como un modo del lado del cliente. La radio responde reflejando el modo real (DIGL o DIGU) inmediatamente. La señal `radeActivated` ahora se emite correctamente basándose en el estado de activación de RADE del lado del cliente, asegurando un comportamiento adecuado al cambiar de modo dentro o fuera de las franjas RADE.

## Mejoras en el menú de antenas

Desde v26.5.2.1, los menús de selección de antena RX y TX se han actualizado:

- **Menú de antena RX** utiliza la lista de antenas RX dedicada de la franja (`SliceModel::rxAntennaList()`) cuando está disponible, recurriendo a la lista de antenas de la radio.
- **Menú de antena TX** utiliza `txAntennaOptions()` para filtrar puertos con capacidad TX, incluyendo prefijos ANT, TX y XVTR, mientras excluye puertos solo RX.
- Todos los elementos del menú de antena llevan su nombre de antena como `data()` para una selección fiable, con la etiqueta de visualización formateada mediante `antennaMenuLabel()` para una apariencia consistente.
- Cada elemento del menú incluye texto de tooltip y status tip para accesibilidad.

## Persistencia del nivel manual de squelch

Desde v26.5.2.1, el nivel manual de squelch persiste entre sesiones. El applet almacena el último umbral de squelch elegido por el usuario bajo la clave de configuración `LastManualSquelchLevel`. Esto es necesario porque el modo automático puede sobrescribir el nivel de squelch de la franja con valores sugeridos por el algoritmo, haciendo que la radio sea una fuente de verdad no fiable para la preferencia manual del operador.

Cuando el applet se inicia, carga el nivel de squelch manual previamente guardado (predeterminado: 20) y lo aplica al deslizador de **Nivel de squelch**. Esto asegura que su umbral de squelch establecido manualmente se conserva entre ciclos de modo e inicios de aplicación.

## Consejos

- No es necesario escribir ceros finales. `14.2` se interpreta como 14.200 MHz.
- Para mover la frecuencia en pequeños pasos sin volver a escribir, use los botones `<` y `>` junto a **PASO**, o gire la rueda del ratón sobre la **Etiqueta de frecuencia** después de sintonizar.
- El tamaño de paso
