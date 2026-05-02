# Sintonizar el radio a una frecuencia (escriba MHz en el indicador)

Escriba una frecuencia directamente en el applet RX Controls para mover el VFO del slice activo a cualquier frecuencia dentro del rango de sintonía del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Si no lo está, vaya a `Settings > Connect to Radio...`.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón de bandeja **RX** en la barra lateral derecha.
- Asegúrese de que el slice que desea sintonizar no esté bloqueado. Si el ícono de candado muestra 🔒, haga clic en él para desbloquearlo antes de continuar (consulte [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)).

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña del slice correspondiente (**A**, **B**, **C**, etc.) en la parte superior del applet RX Controls para seleccionar el slice que desea sintonizar.
2. Haga clic en la **Frequency label** (el indicador con puntos, p. ej. `0.000.000`). Cambia al modo de edición y se convierte en el campo **Frequency edit**.
3. Escriba la frecuencia deseada en MHz. Por ejemplo, escriba `14.225` para 14.225 MHz.
4. Presione **Enter**. El slice se sintoniza a la frecuencia ingresada y el panadapter se recentra sobre ella.

Para cancelar sin cambiar la frecuencia, presione **Escape**. El editor se cierra y se restaura la frecuencia anterior.

## Qué hace cada control

| Control                  | Comportamiento                                                                                                                                                                              | Valor predeterminado |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| **Frequency label**      | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para entrar al modo de edición.                                                                                       | `0.000.000`          |
| **Frequency edit**       | Campo de texto. Ingrese una frecuencia en MHz y presione Enter para sintonizar y recentrar. Escape cancela.                                                                                  | —                    |
| **STEP**                 | Establece el tamaño de paso usado al desplazar la frecuencia con los botones `<` / `>` o la rueda del ratón.                                                                                | 100 Hz               |
| **Filter width presets** | Haga clic en un botón de preajuste para aplicar ese ancho de filtro al modo actual. Haga clic derecho en un preajuste para guardar el ancho actual en ese espacio. Los botones están ocultos en los modos FM, NFM y DFM. | —       |

## Colores de las pestañas y la insignia del slice

A partir de v0.9.3, los botones de las pestañas de slice y el indicador **Slice badge** toman su borde, fondo activo y color de texto del singleton SliceColorManager en lugar de una tabla de colores fija. Los colores son configurables por slice, persisten entre sesiones y se reflejan de forma coherente en los botones de pestañas, la insignia Slice badge, los widgets VFO y las tiras de medidores.

## Comportamiento de la fila de pestañas al reconectar

A partir de v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cada vez que cambia el número de slices disponibles — por ejemplo, tras una desconexión y reconexión, o cuando el radio reporta un número diferente de slices. La implementación anterior omitía la reconstrucción si ya existían botones de pestaña, lo que podía dejar botones obsoletos en pantalla.

El comportamiento actualizado funciona de la siguiente manera:

- Si el nuevo número de slices coincide con el número de botones de pestaña existentes, la fila no se modifica.
- Si los números difieren, los botones de pestaña existentes se eliminan (`clearSliceButtons()`) antes de crear los nuevos.
- Al eliminarlos, la fila de pestañas se oculta y se restaura la **Slice badge** estática.
- La conexión de señal que asigna los clics de los botones a `sliceActivationRequested` se establece una sola vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita que se acumulen manejadores de señal duplicados a lo largo de las reconexiones.

No se requiere ninguna acción del usuario para aprovechar esta corrección. La fila de pestañas se actualiza automáticamente.

## Formato de almacenamiento de preajustes de ancho de filtro

A partir de v0.9.5.1, los preajustes de ancho de filtro pueden almacenar un valor de ancho de banda simple o un par explícito de bordes inferior/superior. Esto coincide con el formato de almacenamiento utilizado por VfoWidget y permite que los preajustes guardados desde VfoWidget se carguen correctamente en el applet RX Controls.

La configuración `FilterPresets` para cada modo (almacenada bajo la clave `FilterPresets_<mode>`, p. ej. `FilterPresets_USB`) acepta una lista separada por comas de entradas en cualquiera de los siguientes formatos:

| Formato   | Ejemplo      | Significado                                                                 |
|-----------|--------------|-----------------------------------------------------------------------------|
| `width`   | `2700`       | Ancho de banda en Hz; los bordes se calculan a partir de la alineación predeterminada del modo. |
| `lo:hi`   | `-1350:1350` | Bordes explícitos de la banda de paso en Hz relativos a la portadora. Ambos valores deben ser enteros y `hi` debe ser mayor que `lo`. |

Las entradas que no se ajustan a ninguno de los formatos, o donde `hi <= lo`, se omiten silenciosamente. El applet carga como máximo seis preajustes por modo.

Normalmente no es necesario editar estos valores manualmente. Al hacer clic derecho en un botón de **Filter width presets** se guarda el ancho de filtro actual en ese espacio usando el formato apropiado de forma automática.

## Modo NT

v0.9.3 añade el modo **NT** al selector de modos. NT se comporta como un modo digital de las siguientes maneras:

- Utiliza los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El ancho de filtro se calcula a partir del valor del borde superior (igual que USB, DIGU y FDV).
- El botón **SQL** y el control deslizante de nivel de squelch están deshabilitados mientras NT está activo, y cualquier squelch activo se apaga automáticamente (el mismo comportamiento que DIGU y DIGL).

## Consejos

- No es necesario escribir ceros al final. `14.2` se interpreta como 14.200 MHz.
- Para desplazar la frecuencia en pasos pequeños sin volver a escribir, use los botones `<` y `>` junto a **STEP**, o desplace la rueda del ratón sobre la **Frequency label** después de sintonizar.
- La lista de tamaños de paso cambia al cambiar de modo. Cambiar el **Mode combo** restablece los preajustes de paso a valores apropiados para ese modo.

## Solución de problemas

- **El campo Frequency edit no aparece cuando hago clic en el indicador** — Es posible que el slice esté bloqueado. Compruebe si el ícono de candado muestra 🔒. Si es así, haga clic en él para desbloquearlo y luego haga clic en el indicador de frecuencia nuevamente.
- **La frecuencia que escribí fue ignorada** — Es posible que haya presionado Escape en lugar de Enter, o ingresado un valor fuera del rango válido (0.001–54.000 MHz en una antena estándar, hasta 450.000 MHz en una antena con transverter). Vuelva a ingresar el valor y presione Enter.
- **El panadapter no siguió la nueva frecuencia** — Compruebe que `View > Pan Follows VFO` esté habilitado.
- **El botón SQL aparece desactivado después de cambiar al modo NT** — Esto es normal. NT es un modo digital; el squelch se deshabilita automáticamente, igual que con DIGU y DIGL.
- **Los botones de pestaña de slice muestran los slices incorrectos después de reconectar** — Este era un problema conocido en versiones anteriores a v0.9.5.1. Actualice a v0.9.5.1 o posterior; la fila de pestañas ahora se reconstruye automáticamente cuando cambia el número de slices.

## Relacionado

- [Bloquear el slice para evitar resintonizaciones accidentales](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
