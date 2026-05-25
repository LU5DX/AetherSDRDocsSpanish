# Sintonice la radio a una frecuencia (escriba MHz en el indicador)

Escriba una frecuencia directamente en el applet de Controles RX para mover el VFO del slice activo a cualquier frecuencia dentro del rango de sintonía de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no lo está, vaya a `Settings > Connect to Radio...`.
- El applet de Controles RX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Asegúrese de que el slice que desea sintonizar no esté bloqueado. Si el icono de bloqueo muestra 🔒, haga clic en él para desbloquearlo antes de continuar (consulte [Lock the slice to prevent accidental retuning](lock-the-slice-to-prevent-accidental-retuning.md)).

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña correspondiente (**A**, **B**, **C**, etc.) en la parte superior del applet de Controles RX para seleccionar el slice que desea sintonizar.
2. Haga clic en la **Etiqueta de frecuencia** (el indicador punteado, p. ej. `0.000.000`). Cambia al modo de edición, convirtiéndose en el campo **Editar frecuencia**.
3. Escriba la frecuencia deseada en MHz. Por ejemplo, escriba `14.225` para 14.225 MHz.
4. Presione **Enter**. El slice se sintoniza a la frecuencia ingresada y el panadapter se recentra en ella.

Para cancelar sin cambiar la frecuencia, presione **Escape**. El editor se cierra y se restaura la frecuencia anterior.

## Qué hace cada control

| Control                    | Comportamiento                                                                                                                                                                                                                                                                   | Valor predeterminado |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| **Pestañas de slice (A..H)** | Selecciona a qué slice está vinculado el applet RX. La fila se oculta si la radio solo admite un slice. `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectarse (v0.9.5.1, #2254). Las conexiones de clic de botón están protegidas contra manejadores de señal duplicados entre reconexiones. | —                    |
| **Insignia de slice**      | Muestra la letra del slice vinculado actualmente, coloreada según la identidad del slice. Admite renderizado HTML para etiquetas de slice personalizadas (#2606).                                                                                                                 | A                    |
| **🔓 / 🔒**                | Activa/desactiva el bloqueo de sintonía en el slice. Los slices bloqueados ignoran los cambios de frecuencia.                                                                                                                                                                    | 🔓 (desbloqueado)    |
| **ANT1 (antena RX)**       | Abre un menú que lista las antenas RX disponibles. Utiliza la lista de antenas RX dedicada del slice cuando está disponible; recurre a la lista de antenas de la radio.                                                                                                           | ANT1                 |
| **ANT1 (antena TX)**       | Abre un menú que lista las antenas con capacidad TX. Filtra los puertos solo RX (prefijo 'RX') e incluye puertos ANT, TX y XVTR.                                                                                                                                                 | ANT1                 |
| **2.7K (ancho de filtro)** | Muestra el ancho de banda del filtro actual (p. ej. 2.7K, 3.3K, 500). Se actualiza cuando se aplica un ajuste preestablecido de filtro.                                                                                                                                           | 2.7K                 |
| **QSK**                    | Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado a través del applet CW.                                                                                                                                                                 | apagado (gris)       |
| **TX (insignia)**          | Haga clic para establecer este slice como el slice TX.                                                                                                                                                                                                                           | —                    |
| **Combo de modo**          | Establece el modo de operación del slice. Las opciones varían según la radio y las banderas de compilación. La opción RADE requiere la bandera de compilación HAVE_RADE. Al cambiar a modos RTTY o digitales (DIGU, DIGL), el squelch se desactiva automáticamente. Al salir del modo RADE, emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376). | USB                  |
| **Etiqueta de frecuencia** | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para entrar al modo de edición.                                                                                                                                                                             | `0.000.000`          |
| **Editar frecuencia**      | Campo de texto. Ingrese la frecuencia en MHz y presione Enter para sintonizar y recentrar. Admite autoescalado de kHz/Hz. Escape cancela y restaura la frecuencia anterior. Consciente de XVTR: acepta hasta 450 MHz en antenas XVTR; acepta entradas explícitas en MHz de hasta 50,000 MHz cuando el número escrito excede 54 MHz (#2376). | —                    |
| **PASO**                   | Establece el tamaño de paso utilizado al ajustar la frecuencia con los botones de flecha o la rueda del ratón. La lista de pasos depende del modo.                                                                                                                               | 100 Hz               |
| **Ajustes preestablecidos de ancho de filtro** | Haga clic en un botón preestablecido para aplicar ese ancho de banda de filtro. Haga clic derecho para guardar el ancho actual en esa ranura. Oculto en modos FM/NFM/DFM. El indicador de ancho usa lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). `stepFilterWidth()` recorre la lista preestablecida por modo para el escalado correcto de ancho/estrecho (#2208). | —                    |
| **Widget de banda pasante del filtro** | Arrastre los bordes lo/hi para ajustar la banda pasante del filtro directamente.                                                                                                                                                                                               | —                    |
| **Modo de tono (FM)**      | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM.                                                                                                                                                                                          | Off                  |
| **Valor de tono CTCSS**   | Selecciona la frecuencia de tono CTCSS enviada en transmisión. Habilitado solo cuando el modo de tono = CTCSS TX.                                                                                                                                                                | —                    |
| **Offset (FM)**            | Establece la frecuencia de offset del repetidor FM en MHz (0.0–100.0 MHz, paso 0.1).                                                                                                                                                                                             | 0.0 MHz              |
| **− (offset hacia abajo)** | Establece la dirección del offset del repetidor a 'abajo' (TX por debajo de RX).                                                                                                                                                                                                 | —                    |
| **Simplex**                | Establece la dirección del offset del repetidor a simplex (TX = RX).                                                                                                                                                                                                             | marcado              |
| **+ (offset hacia arriba)** | Establece la dirección del offset del repetidor a 'arriba' (TX por encima de RX).                                                                                                                                                                                               | —                    |
| **REV**                    | Invierte el signo del offset TX para trabajar un par de repetidores invertido.                                                                                                                                                                                                   | —                    |
| **🔊 / 🔇 (silencio)**     | Un solo clic silencia/activa el sonido de este slice (diferido por el intervalo de discriminación de clics de la plataforma). Doble clic silencia/activa el sonido de todos los slices propios. El icono cambia cuando la radio lo confirma a través de `SliceModel::audioMuteChanged`. El estado de silencio NO se guarda/restaura en la reconexión: la radio es la fuente de verdad. | 🔊 (sonido activado) |
| **Ganancia AF**            | Ajusta la ganancia de salida de audio del slice (0–100).                                                                                                                                                                                                                         | 70                   |
| **Pan L / R**              | Desplaza el audio del slice entre los canales izquierdo y derecho (0–100). Doble clic restablece a 50 (centro).                                                                                                                                                                  | 50                   |
| **SQL**                    | Activa el squelch en el nivel actual del deslizador. Desactivado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch podría recortar caracteres FSK (#2504).                                                                                     | —                    |
| **Nivel de squelch**       | Ajusta el umbral del squelch (0–100). Solo tiene efecto cuando SQL está activado. Desactivado en modos RTTY y digitales. El nivel manual persiste entre sesiones.                                                                                                                 | 20                   |
| **Modo AGC**               | Establece el modo AGC del slice: Off, Slow, Med, Fast. Oculto en modos de la familia FM.                                                                                                                                                                                         | Med                  |
| **Umbral AGC**             | Establece el umbral AGC (o el nivel AGC desactivado cuando el modo AGC es Off).                                                                                                                                                                                                 | 65                   |
| **RIT**                    | Activa/desactiva la Sintonización Incremental de Recepción.                                                                                                                                                                                                                      | —                    |
| **RIT 0**                  | Pone a cero el offset RIT.                                                                                                                                                                                                                                                       | —                    |
| **Offset RIT**             | Ajusta el offset RIT en pasos de 10 Hz usando los botones de flecha o la rueda del ratón.                                                                                                                                                                                        | +0 Hz                |
| **XIT**                    | Activa/desactiva la Sintonización Incremental de Transmisión.                                                                                                                                                                                                                    | —                    |
| **XIT 0**                  | Pone a cero el offset XIT.                                                                                                                                                                                                                                                       | —                    |
| **Offset XIT**             | Ajusta el offset XIT en pasos de 10 Hz usando los botones de flecha o la rueda del ratón.                                                                                                                                                                                        | +0 Hz                |

## Escalado del ancho de filtro

A partir de la v0.9.8, el applet admite un escalado preciso del ancho de filtro, correcto para el modo, a través de la lista preestablecida por modo. El método `stepFilterWidth()` recorre la lista preestablecida para el modo actual, encuentra el preestablecido más cercano al ancho de filtro actual y aplica el siguiente o el anterior en la dirección elegida.

Esto significa:

- Los atajos de ampliar y estrechar producen anchos de filtro que coinciden con la lista preestablecida del modo actual (SSB, CW, AM, digital, etc.).
- La actualización del ancho de filtro utiliza `applyFilterPreset()`, que calcula la geometría correcta del borde inferior y superior para el modo (USB, LSB, CWL, CZU, DIGL, DIGU, RTTY, AM, SAM, etc.).
- No se produce ningún cambio de filtro si el slice no tiene anchos de filtro configurados o si el ancho actual ya es igual al ancho objetivo.

El indicador de ancho de filtro (compartido con VfoWidget a través de `RxApplet::formatFilterWidth`) utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

## Colores de pestañas e insignia de slice

A partir de la v0.9.3, los botones de las pestañas de slice y el indicador de **Insignia de slice** toman su color de borde, fondo activo y color de texto del singleton SliceColorManager en lugar de una tabla de colores fija. Los colores son configurables por slice, persisten entre sesiones y se reflejan de manera consistente en los botones de las pestañas de slice, la Insignia de slice, los widgets VFO y las barras de medidores.

A partir de la v26.5.2.1, la **Insignia de slice** admite renderizado HTML (`setTextFormat(Qt::RichText)`), lo que permite etiquetas de slice personalizadas con formato de texto enriquecido.

## Comportamiento de la fila de pestañas de slice en la reconexión

A partir de la v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cada vez que cambia el número de slices disponibles, por ejemplo, después de una desconexión y reconexión o cuando la radio informa un número de slices diferente. La implementación anterior omitía la reconstrucción si ya existían botones de pestaña, lo que podía dejar botones obsoletos en pantalla.

El comportamiento actualizado funciona de la siguiente manera:

- Si el nuevo número de slices coincide con el número de botones de pestaña existentes, la fila se deja sin cambios.
- Si los números difieren, los botones de pestaña existentes se eliminan (`clearSliceButtons()`) antes de crear nuevos botones.
- Al eliminar, la fila de pestañas se oculta y se restaura la **Insignia de slice** estática.
- La conexión de señal que asigna los clics de botón a `sliceActivationRequested` se establece solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de manejadores de señal duplicados entre reconexiones.

No se requiere ninguna acción del usuario para aprovechar esta corrección. La fila de pestañas se actualiza automáticamente.

## Formato de almacenamiento de ajustes preestablecidos de ancho de filtro

A partir de la v0.9.5.1, los ajustes preestablecidos de ancho de filtro pueden almacenar un valor de ancho de banda simple o un par explícito de borde inferior/borde superior. Esto coincide con el formato de almacenamiento utilizado por VfoWidget y permite que los ajustes preestablecidos guardados desde VfoWidget se carguen correctamente en el applet de Controles RX.

La configuración `FilterPresets` para cada modo (almacenada bajo la clave `FilterPresets_<modo>`, p. ej. `FilterPresets_USB`) acepta una lista separada por comas de entradas en cualquiera de los siguientes formatos:

| Formato  | Ejemplo      | Significado                                                                                                 |
|----------|--------------|-------------------------------------------------------------------------------------------------------------|
| `ancho`  | `2700`       | Ancho de banda en Hz; los bordes se calculan a partir de la alineación predeterminada del modo.              |
| `lo:hi`  | `-1350:1350` | Bordes de banda pasante explícitos en Hz relativos a la portadora. Ambos valores deben ser enteros y `hi` debe ser mayor que `lo`. |

Las entradas que no se ajustan a ninguno de los dos formatos, o donde `hi <= lo`, se omiten silenciosamente. El applet carga un máximo de seis ajustes preestablecidos por modo.

Normalmente no es necesario editar estos valores manualmente. Al hacer clic derecho en un botón de **Ajustes preestablecidos de ancho de filtro**, se guarda el ancho de filtro actual en esa ranura utilizando el formato apropiado automáticamente.

## Comportamiento del squelch en modos RTTY y digitales

A partir de la v26.5.1, cuando cambia al modo RTTY, el botón **SQL** y el deslizador de nivel de squelch se desactivan, y cualquier squelch activo se apaga automáticamente. Esto evita que el squelch recorte los caracteres FSK y rompa la decodificación. El mismo comportamiento se aplica a los modos DIGU, DIGL y NT.

## Comportamiento del modo RADE

RADE se maneja solo como un modo del lado del cliente. La radio responde reflejando el modo real (DIGL o DIGU) inmediatamente. La señal `radeActivated` se emite correctamente según el estado de activación de RADE del lado del cliente, lo que garantiza un comportamiento adecuado al cambiar de modo en slices con o sin RADE.

Al salir del modo RADE a través del combo de modo, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE.

## Mejoras en el menú de antenas

A partir de la v26.5.2.1, los menús de selección de antena RX y TX se han actualizado:

- **Menú de antena RX** utiliza la lista de antenas RX dedicada del slice (`SliceModel::rxAntennaList()`) cuando está disponible, recurriendo a la lista de antenas de la radio.
- **Menú de antena TX** utiliza `txAntennaOptions()` para filtrar
