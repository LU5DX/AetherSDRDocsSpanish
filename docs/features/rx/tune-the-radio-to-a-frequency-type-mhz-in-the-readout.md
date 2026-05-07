# Sintonice la radio a una frecuencia (escriba MHz en el indicador)

Escriba una frecuencia directamente en el applet Controles RX para mover el VFO del slice activo a cualquier frecuencia dentro del rango de sintonización de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet Controles RX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
- Asegúrese de que el slice que desea sintonizar no esté bloqueado. Si el icono de candado muestra 🔒, haga clic en él para desbloquearlo antes de continuar (consulte [Bloquear el slice para evitar resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)).

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña de slice correspondiente (**A**, **B**, **C**, etc.) en la parte superior del applet Controles RX para seleccionar el slice que desea sintonizar.
2. Haga clic en la **Etiqueta de frecuencia** (el indicador punteado, p. ej. `0.000.000`). Cambia al modo de edición, convirtiéndose en el campo **Edición de frecuencia**.
3. Escriba la frecuencia deseada en MHz. Por ejemplo, escriba `14.225` para 14.225 MHz.
4. Presione **Enter**. El slice se sintoniza a la frecuencia ingresada y el panadapter se recentra en ella.

Para cancelar sin cambiar la frecuencia, presione **Escape**. El editor se cierra y se restaura la frecuencia anterior.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---------|----------|---------|
| **Pestañas de slice (A..H)** | Selecciona a qué slice está vinculado el applet RX. Fila oculta si la radio solo admite un slice. | — |
| **Insignia de slice** | Muestra la letra del slice actualmente vinculado, coloreada según la identidad del slice. | A |
| **🔓 / 🔒** | Alterna el bloqueo de sintonía en el slice. Los slices bloqueados ignoran los cambios de frecuencia. | 🔓 (desbloqueado) |
| **ANT1 (antena RX)** | Abre un menú que lista las antenas RX disponibles. Al seleccionar, se establece la antena de recepción del slice. | ANT1 |
| **ANT1 (antena TX)** | Abre un menú que lista las antenas capaces de transmitir. Los puertos solo RX (prefijo 'RX') se filtran. | ANT1 |
| **2.7K (ancho de filtro)** | Muestra el ancho de banda del filtro actual (p. ej. 2.7K, 3.3K, 500). | 2.7K |
| **QSK** | Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado mediante el applet CW. | apagado (gris) |
| **TX (insignia)** | Haga clic para establecer este slice como el slice de TX. | — |
| **Combo de modo** | Establece el modo de operación del slice. Las opciones varían según la radio y las banderas de compilación. | USB |
| **Etiqueta de frecuencia** | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para entrar en modo de edición. | `0.000.000` |
| **Edición de frecuencia** | Campo de texto. Ingrese la frecuencia en MHz y presione Enter para sintonizar y recentrar. Escape cancela y restaura la frecuencia anterior. | — |
| **STEP** | Establece el tamaño de paso utilizado al ajustar la frecuencia con los botones de flecha o la rueda del ratón. La lista de pasos depende del modo. | 100 Hz |
| **Preajustes de ancho de filtro** | Haga clic en un botón preajustado para aplicar ese ancho de banda de filtro. Haga clic derecho para guardar el ancho actual en esa ranura. Oculto en modos FM/NFM/DFM. | — |
| **Widget de banda de paso del filtro** | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro directamente. | — |
| **Modo de tono (FM)** | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Off |
| **Valor de tono CTCSS** | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Habilitado solo cuando el modo de tono = CTCSS TX. | — |
| **Offset (FM)** | Establece la frecuencia de offset del repetidor FM en MHz (0.0–100.0 MHz, paso 0.1). | 0.0 MHz |
| **− (offset hacia abajo)** | Establece la dirección del offset del repetidor a 'abajo' (TX por debajo de RX). | — |
| **Simplex** | Establece la dirección del offset del repetidor a simplex (TX = RX). | marcado |
| **+ (offset hacia arriba)** | Establece la dirección del offset del repetidor a 'arriba' (TX por encima de RX). | — |
| **REV** | Invierte el signo del offset de TX para trabajar un par de repetidores invertido. | — |
| **🔊 / 🔇 (silencio)** | Silencia o reactiva la salida de audio del slice. | 🔊 (sin silenciar) |
| **Ganancia AF** | Ajusta la ganancia de salida de audio del slice (0–100). | 70 |
| **Pan L / R** | Desplaza el audio del slice entre los canales izquierdo y derecho (0–100). Doble clic restablece a 50 (centro). | 50 |
| **SQL** | Activa el squelch en el nivel actual del deslizador. | — |
| **Nivel de squelch** | Ajusta el umbral de squelch (0–100). Solo tiene efecto cuando SQL está activado. | 20 |
| **Modo AGC** | Establece el modo AGC del slice: Off, Slow, Med, Fast. Oculto en modos de la familia FM. | Med |
| **Umbral AGC** | Establece el umbral AGC (o el nivel de AGC desactivado cuando el modo AGC es Off). | 65 |
| **RIT** | Activa/desactiva la sintonización incremental de recepción. | — |
| **RIT 0** | Pone a cero el offset de RIT. | — |
| **Offset RIT** | Ajusta el offset de RIT en pasos de 10 Hz usando botones de flecha o la rueda del ratón. | +0 Hz |
| **XIT** | Activa/desactiva la sintonización incremental de transmisión. | — |
| **XIT 0** | Pone a cero el offset de XIT. | — |
| **Offset XIT** | Ajusta el offset de XIT en pasos de 10 Hz usando botones de flecha o la rueda del ratón. | +0 Hz |

## Ajuste de ancho de filtro por pasos

Desde la v0.9.8, el applet admite un ajuste de ancho de filtro preciso y correcto para el modo a través de la lista de preajustes por modo. El método `stepFilterWidth()` recorre la lista de preajustes para el modo actual, encuentra el preajuste más cercano al ancho de filtro actual y aplica el siguiente o el anterior en la dirección elegida.

Esto significa:

- Los accesos directos para ensanchar y estrechar producen anchos de filtro que coinciden con la lista de preajustes del modo actual (SSB, CW, AM, digital, etc.).
- La actualización del ancho de filtro utiliza `applyFilterPreset()`, que calcula la geometría correcta del borde inferior y superior para el modo (USB, LSB, CWL, CZU, DIGL, DIGU, RTTY, AM, SAM, etc.).
- No se produce ningún cambio de filtro si el slice no tiene anchos de filtro configurados o si el ancho actual ya es igual al ancho objetivo.

El indicador de ancho de filtro (compartido con VfoWidget a través de `RxApplet::formatFilterWidth`) utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

## Colores de pestañas de slice e insignia

Desde la v0.9.3, los botones de las pestañas de slice y el indicador **Insignia de slice** toman su borde, fondo activo y color de texto del singleton SliceColorManager en lugar de una tabla de colores fija. Los colores son configurables por slice, persisten entre sesiones y se reflejan de manera consistente en los botones de las pestañas de slice, la Insignia de slice, los widgets VFO y las tiras de medidores.

## Comportamiento de la fila de pestañas de slice al reconectar

Desde la v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente siempre que cambia el número de slices disponibles — por ejemplo, después de una desconexión y reconexión o cuando la radio reporta un número diferente de slices. La implementación anterior omitía la reconstrucción si ya existían botones de pestaña, lo que podía dejar botones obsoletos en pantalla.

El comportamiento actualizado funciona de la siguiente manera:

- Si el nuevo número de slices coincide con el número de botones de pestaña existentes, la fila se deja sin cambios.
- Si los números difieren, los botones de pestaña existentes se eliminan (`clearSliceButtons()`) antes de crear nuevos botones.
- Al eliminar, la fila de pestañas se oculta y se restaura la **Insignia de slice** estática.
- La conexión de señal que asigna los clics de botón a `sliceActivationRequested` se establece solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de controladores de señal duplicados a través de reconexiones.

No se requiere ninguna acción del usuario para aprovechar esta corrección. La fila de pestañas se actualiza automáticamente.

## Formato de almacenamiento de preajustes de ancho de filtro

Desde la v0.9.5.1, los preajustes de ancho de filtro pueden almacenar un valor de ancho de banda simple o un par explícito de borde inferior/borde superior. Esto coincide con el formato de almacenamiento utilizado por VfoWidget y permite que los preajustes guardados desde VfoWidget se carguen correctamente en el applet Controles RX.

La configuración `FilterPresets` para cada modo (almacenada bajo la clave `FilterPresets_<mode>`, p. ej. `FilterPresets_USB`) acepta una lista separada por comas de entradas en cualquiera de los siguientes formatos:

| Formato | Ejemplo | Significado |
|--------|---------|---------|
| `width` | `2700` | Ancho de banda en Hz; los bordes se calculan a partir de la alineación predeterminada del modo. |
| `lo:hi` | `-1350:1350` | Bordes explícitos de la banda de paso en Hz con respecto a la portadora. Ambos valores deben ser enteros y `hi` debe ser mayor que `lo`. |

Las entradas que no se ajusten a ninguno de los formatos, o donde `hi <= lo`, se omiten silenciosamente. El applet carga un máximo de seis preajustes por modo.

Normalmente no es necesario editar estos valores manualmente. Haga clic derecho en un botón de **Preajustes de ancho de filtro** para guardar el ancho de filtro actual en esa ranura usando el formato apropiado automáticamente.

## Modo NT

La v0.9.3 añade el modo **NT** al selector de modo. NT se comporta como un modo digital de las siguientes maneras:

- Utiliza los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El ancho de filtro se calcula a partir del valor del borde superior (igual que USB, DIGU y FDV).
- El botón **SQL** y el deslizador de nivel de squelch están deshabilitados mientras NT está activo, y cualquier squelch activo se desactiva automáticamente (mismo comportamiento que DIGU y DIGL).

## Consejos

- No es necesario escribir ceros finales. `14.2` se interpreta como 14.200 MHz.
- Para mover la frecuencia en pasos pequeños sin volver a escribir, use los botones `<` y `>` junto a **STEP**, o desplace la rueda del ratón sobre la **Etiqueta de frecuencia** después de sintonizar.
- La lista de tamaños de paso cambia cuando cambia de modo. Cambiar el **Combo de modo** restablece los preajustes de paso a valores apropiados para ese modo.
- Los accesos directos para ensanchar y estrechar el ancho de filtro recorren la lista de preajustes por modo desde la v0.9.8, proporcionando una geometría de filtro correcta para el modo en cada paso.

## Solución de problemas

- **El campo de Edición de frecuencia no aparece cuando hago clic en el indicador** — El slice puede estar bloqueado. Verifique si el icono de candado muestra 🔒. Si es así, haga clic en él para desbloquearlo, luego haga clic nuevamente en el indicador de frecuencia.
- **La frecuencia que escribí fue ignorada** — Es posible que haya presionado Escape en lugar de Enter, o que haya ingresado un valor fuera del rango válido (0.001–54.000 MHz en una antena estándar, hasta 450.000 MHz en una antena de transverter). Vuelva a ingresar el valor y presione Enter.
- **El panadapter no siguió la nueva frecuencia** — Verifique que `View > Pan Follows VFO` esté habilitado.
- **El botón SQL está atenuado después de cambiar al modo NT** — Esto es esperado. NT es un modo digital; el squelch se desactiva automáticamente, igual que para DIGU y DIGL.
- **Los botones de pestaña de slice muestran los slices incorrectos después de reconectar** — Este era un problema conocido en versiones anteriores a la v0.9.5.1. Actualice a la v0.9.5.1 o posterior; la fila de pestañas ahora se reconstruye automáticamente cuando cambia el número de slices.

## Relacionado

- [Bloquear el slice para evitar resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
