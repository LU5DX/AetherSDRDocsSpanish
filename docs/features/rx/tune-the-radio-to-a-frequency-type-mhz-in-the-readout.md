# Sintonizar la radio a una frecuencia (escriba MHz en el indicador)

Escriba una frecuencia directamente en el applet de Controles RX para mover el VFO del slice activo a cualquier frecuencia dentro del rango de sintonización de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet de Controles RX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Asegúrese de que el slice que desea sintonizar no esté bloqueado. Si el icono de candado muestra 🔒, haga clic en él para desbloquearlo antes de continuar (consulte [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)).

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña de slice correspondiente (**A**, **B**, **C**, etc.) en la parte superior del applet de Controles RX para seleccionar el slice que desea sintonizar.
2. Haga clic en la **Etiqueta de frecuencia** (el indicador punteado, p. ej. `0.000.000`). Cambia al modo de edición, convirtiéndose en el campo **Edición de frecuencia**.
3. Escriba la frecuencia deseada en MHz. Por ejemplo, escriba `14.225` para 14.225 MHz.
4. Presione **Enter**. El slice se sintoniza en la frecuencia ingresada y el panadapter se recentra en ella.

Para cancelar sin cambiar la frecuencia, presione **Escape**. El editor se cierra y se restaura la frecuencia anterior.

## Qué hace cada control

| Control                    | Comportamiento                                                                                                                                                                                                                                                                                                                        | Valor predeterminado |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| **Pestañas de slice (A..H)** | Selecciona a qué slice está vinculado el applet RX. La fila se oculta si la radio solo admite un slice. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic de botón están protegidas contra controladores de señal duplicados en reconexiones. | —                     |
| **Insignia de slice**      | Muestra la letra del slice actualmente vinculado, coloreada según la identidad del slice. Admite renderizado HTML para etiquetas de slice personalizadas (#2606).                                                                                                                                                                      | A                     |
| **🔓 / 🔒**                  | Alterna el bloqueo de sintonía en el slice. Los slices bloqueados ignoran los cambios de frecuencia.                                                                                                                                                                                                                                  | 🔓 (desbloqueado)     |
| **ANT1 (antena RX)**       | Abre un menú que lista las antenas RX disponibles. Utiliza la lista de antenas RX dedicada del slice cuando está disponible; en caso contrario, recurre a la lista de antenas de la radio.                                                                                                                                            | ANT1                  |
| **ANT1 (antena TX)**       | Abre un menú que lista las antenas capaces de TX. Filtra los puertos solo RX (prefijo 'RX') e incluye puertos ANT, TX y XVTR.                                                                                                                                                                                                        | ANT1                  |
| **2.7K (ancho de filtro)** | Muestra el ancho de banda del filtro actual (p. ej. 2.7K, 3.3K, 500). Se actualiza cuando se aplica un ajuste preestablecido de filtro.                                                                                                                                                                                               | 2.7K                  |
| **QSK**                    | Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado mediante el applet CW.                                                                                                                                                                                                                       | apagado (gris)        |
| **TX (insignia)**          | Haga clic para establecer este slice como el slice de TX.                                                                                                                                                                                                                                                                             | —                     |
| **Modo (combo)**           | Establece el modo de operación del slice. Las opciones varían según la radio y las marcas de compilación. La opción RADE requiere la marca de compilación HAVE_RADE. Cambiar a RTTY o modos digitales (DIGU, DIGL) desactiva automáticamente el squelch. Al salir del modo RADE, emite radeActivated(false) solo si el slice estaba realmente en RADE (#2376). | USB                   |
| **Etiqueta de frecuencia** | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para entrar en modo de edición.                                                                                                                                                                                                                                   | `0.000.000`           |
| **Edición de frecuencia**  | Campo de texto. Ingrese la frecuencia en MHz y presione Enter para sintonizar y recentrar. Admite autoescalado de kHz/Hz. Escape cancela y restaura la frecuencia anterior. Consciente de XVTR: acepta hasta 450 MHz en antenas XVTR; acepta entradas explícitas de MHz hasta 50 000 MHz cuando el número escrito supera 54 MHz (#2376). | —                     |
| **PASO**                   | Establece el tamaño de paso utilizado al ajustar la frecuencia con los botones de flecha o la rueda del ratón. La lista de pasos depende del modo.                                                                                                                                                                                     | 100 Hz                |
| **Ajustes predefinidos de ancho de filtro** | Haga clic en un botón de ajuste predefinido para aplicar ese ancho de banda de filtro. Haga clic derecho para guardar el ancho actual en esa ranura. Oculto en modos FM/NFM/DFM. El indicador de ancho usa lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). stepFilterWidth() recorre la lista de ajustes predefinidos por modo para un ensanche/estrechamiento correcto según el modo (#2208). | —                     |
| **Widget de banda pasante del filtro** | Arrastre los bordes lo/hi para ajustar la banda pasante del filtro directamente.                                                                                                                                                                                                                                                       | —                     |
| **Modo de tono (FM)**      | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM.                                                                                                                                                                                                                                              | Desactivado           |
| **Valor de tono CTCSS**    | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Habilitado solo cuando el modo de tono = CTCSS TX.                                                                                                                                                                                                                | —                     |
| **Desplazamiento (FM)**    | Establece la frecuencia de desplazamiento del repetidor FM en MHz (0.0–100.0 MHz, paso 0.1).                                                                                                                                                                                                                                         | 0.0 MHz               |
| **− (desplazamiento abajo)**| Establece la dirección del desplazamiento del repetidor hacia 'abajo' (TX por debajo de RX).                                                                                                                                                                                                                                          | —                     |
| **Simplex**                | Establece la dirección del desplazamiento del repetidor a simplex (TX = RX).                                                                                                                                                                                                                                                          | marcado               |
| **+ (desplazamiento arriba)**| Establece la dirección del desplazamiento del repetidor hacia 'arriba' (TX por encima de RX).                                                                                                                                                                                                                                         | —                     |
| **REV**                    | Invierte el signo del desplazamiento TX para trabajar un par de repetidores invertido.                                                                                                                                                                                                                                               | —                     |
| **🔊 / 🔇 (silencio)**      | Un solo clic silencia/activa el sonido de este slice (diferido por el intervalo de discriminación de clics de la plataforma). Doble clic silencia/activa el sonido de todos los slices propios. El icono cambia cuando la radio lo confirma mediante SliceModel::audioMuteChanged. El estado de silencio NO se guarda/restaura al reconectar: la radio es la fuente de verdad. | 🔊 (sin silenciar)    |
| **Ganancia AF**            | Ajusta la ganancia de salida de audio del slice (0–100).                                                                                                                                                                                                                                                                              | 70                    |
| **Panorámica L / R**       | Desplaza el audio del slice entre los canales izquierdo y derecho (0–100). Doble clic restablece a 50 (centro). El deslizador usa un relleno anclado al centro: la ranura se colorea desde el centro hacia la posición del mango, proporcionando una indicación visual de la dirección de la panorámica. Un punto de marca central indica la posición neutral de un vistazo. | 50                    |
| **SQL**                    | Activa el squelch al nivel actual del deslizador. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK (#2504).                                                                                                                                            | —                     |
| **Nivel de squelch**       | Ajusta el umbral de squelch (0–100). Solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. El nivel manual persiste entre sesiones.                                                                                                                                                                     | 20                    |
| **Modo AGC**               | Establece el modo AGC del slice: Desactivado, Lento, Medio, Rápido. Oculto en modos de la familia FM.                                                                                                                                                                                                                                 | Medio                 |
| **Umbral AGC**             | Establece el umbral AGC (o el nivel de desactivación de AGC cuando el modo AGC está en Desactivado).                                                                                                                                                                                                                                  | 65                    |
| **RIT**                    | Activa/desactiva la sintonización incremental de recepción.                                                                                                                                                                                                                                                                           | —                     |
| **RIT 0**                  | Pone a cero el desplazamiento RIT.                                                                                                                                                                                                                                                                                                    | —                     |
| **Desplazamiento RIT**     | Ajusta el desplazamiento RIT en pasos de 10 Hz usando botones de flecha o la rueda del ratón.                                                                                                                                                                                                                                        | +0 Hz                 |
| **XIT**                    | Activa/desactiva la sintonización incremental de transmisión.                                                                                                                                                                                                                                                                         | —                     |
| **XIT 0**                  | Pone a cero el desplazamiento XIT.                                                                                                                                                                                                                                                                                                    | —                     |
| **Desplazamiento XIT**     | Ajusta el desplazamiento XIT en pasos de 10 Hz usando botones de flecha o la rueda del ratón.                                                                                                                                                                                                                                        | +0 Hz                 |

## Avance por ancho de filtro

Desde la v0.9.8, el applet admite un avance preciso del ancho de filtro corregido por modo a través de la lista de ajustes predefinidos por modo. El método `stepFilterWidth()` recorre la lista de ajustes predefinidos para el modo actual, encuentra el ajuste predefinido más cercano al ancho de filtro actual y aplica el siguiente o anterior ajuste predefinido en la dirección elegida.

Esto significa:

- Los atajos de ensanchar y estrechar producen anchos de filtro que coinciden con la lista de ajustes predefinidos del modo actual (SSB, CW, AM, digital, etc.).
- La actualización del ancho de filtro usa `applyFilterPreset()`, que calcula la geometría correcta del borde inferior y superior para el modo (USB, LSB, CWL, CZU, DIGL, DIGU, RTTY, AM, SAM, etc.).
- No se produce ningún cambio de filtro si el slice no tiene configurados anchos de filtro o si el ancho actual ya es igual al ancho objetivo.

El indicador de ancho de filtro (compartido con VfoWidget mediante `RxApplet::formatFilterWidth`) usa lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

## Pestañas de slice y colores de insignia

Desde la v0.9.3, los botones de pestaña de slice y el indicador de **Insignia de slice** toman su borde, fondo activo y color de texto del singleton SliceColorManager en lugar de una tabla de colores fija. Los colores son configurables por slice, persisten entre sesiones y se reflejan de manera consistente en los botones de pestaña de slice, la insignia de slice, los widgets VFO y las tiras de medidores.

Desde la v26.5.2.1, la **Insignia de slice** admite renderizado HTML (`setTextFormat(Qt::RichText)`), permitiendo etiquetas de slice personalizadas con formato de texto enriquecido.

## Comportamiento de la fila de pestañas de slice al reconectar

Desde la v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cada vez que cambia el número de slices disponibles — por ejemplo, después de una desconexión y reconexión o cuando la radio informa un número diferente de slices. La implementación anterior omitía la reconstrucción si ya existían botones de pestaña, lo que podía dejar botones obsoletos en la pantalla.

El comportamiento actualizado funciona de la siguiente manera:

- Si el nuevo número de slices coincide con el número de botones de pestaña existentes, la fila se deja sin cambios.
- Si los números difieren, los botones de pestaña existentes se eliminan (`clearSliceButtons()`) antes de crear nuevos botones.
- Al eliminar, la fila de pestañas se oculta y se restaura la **Insignia de slice** estática.
- La conexión de señal que asigna los clics de botón a `sliceActivationRequested` se establece solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de controladores de señal duplicados en las reconexiones.

No se requiere ninguna acción del usuario para aprovechar esta corrección. La fila de pestañas se actualiza automáticamente.

## Formato de almacenamiento de ajustes predefinidos de ancho de filtro

Desde la v0.9.5.1, los ajustes predefinidos de ancho de filtro pueden almacenar ya sea un valor de ancho de banda simple o un par explícito de borde inferior/borde superior. Esto coincide con el formato de almacenamiento utilizado por VfoWidget y permite que los ajustes predefinidos guardados desde VfoWidget se carguen correctamente en el applet de Controles RX.

La configuración `FilterPresets` para cada modo (almacenada bajo la clave `FilterPresets_<modo>`, p. ej. `FilterPresets_USB`) acepta una lista separada por comas de entradas en cualquiera de los siguientes formatos:

| Formato | Ejemplo | Significado |
|---------|---------|-------------|
| `ancho` | `2700` | Ancho de banda en Hz; los bordes se calculan a partir de la alineación predeterminada del modo. |
| `lo:hi` | `-1350:1350` | Bordes de banda pasante explícitos en Hz relativos a la portadora. Ambos valores deben ser enteros y `hi` debe ser mayor que `lo`. |

Las entradas que no se ajustan a ninguno de los formatos, o donde `hi <= lo`, se omiten silenciosamente. El applet carga un máximo de seis ajustes predefinidos por modo.

Normalmente no necesita editar estos valores manualmente. Al hacer clic derecho en un botón de **Ajustes predefinidos de ancho de filtro**, se guarda el ancho de filtro actual en esa ranura utilizando el formato adecuado automáticamente.

## Comportamiento del squelch en modos RTTY y digitales

Desde la v26.5.1, cuando cambia al modo RTTY, el botón **SQL** y el deslizador de nivel de squelch se deshabilitan, y cualquier squelch activo se apaga automáticamente. Esto evita que el squelch recorte los caracteres FSK y rompa la decodificación. El mismo comportamiento se aplica a los modos DIGU, DIGL y NT.

## Comportamiento del modo RADE

RADE se maneja solo como un modo del lado del cliente. La radio responde reflejando el modo real (DIGL o DIGU) inmediatamente. La señal `radeActivated` se emite correctamente según el estado de activación de RADE del lado del cliente, asegurando un comportamiento adecuado al cambiar de modo en slices RADE o al salir de ellos.

Al salir del modo RADE mediante el combo de modos, el applet emite `radeActivated(false)` solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no es RADE.

## Mejoras
