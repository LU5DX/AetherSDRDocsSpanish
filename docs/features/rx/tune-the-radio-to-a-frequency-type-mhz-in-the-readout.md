# Sintonizar la radio a una frecuencia (escriba MHz en el indicador)

Escriba una frecuencia directamente en el applet RX Controls para mover el VFO del slice activo a cualquier frecuencia dentro del rango de sintonización de la radio.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón de bandeja **RX** en la barra lateral derecha.
- Asegúrese de que el slice que desea sintonizar no esté bloqueado. Si el icono de bloqueo muestra 🔒, haga clic en él para desbloquearlo antes de continuar (véase [Lock the slice to prevent accidental retuning](lock-the-slice-to-prevent-accidental-retuning.md)).

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña de slice correspondiente (**A**, **B**, **C**, etc.) en la parte superior del applet RX Controls para seleccionar el slice que desea sintonizar.
2. Haga clic en la **Etiqueta de frecuencia** (el indicador punteado, p. ej. `0.000.000`). Se cambia al modo de edición, convirtiéndose en el campo **Frequency edit**.
3. Escriba la frecuencia deseada en MHz. Por ejemplo, escriba `14.225` para 14.225 MHz.
4. Presione **Enter**. El slice se sintoniza a la frecuencia ingresada y el panadapter se recentra en ella.

Para cancelar sin cambiar la frecuencia, presione **Escape**. El editor se cierra y se restaura la frecuencia anterior.

## Qué hace cada control

| Control                  | Comportamiento                                                                                                                  | Predeterminado |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| **Frequency label**      | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para entrar en modo de edición.                                                        | `0.000.000` |
| **Frequency edit**       | Campo de texto. Ingrese una frecuencia en MHz y presione Enter para sintonizar y recentrar. Escape cancela.                                                | —           |
| **STEP**                 | Establece el tamaño de paso utilizado al ajustar la frecuencia con los botones `<` / `>` o la rueda del ratón.                                         | 100 Hz      |
| **Filter width presets** | Haga clic en un botón predefinido para aplicar ese ancho de filtro para el modo actual. Haga clic con el botón derecho en un predefinido para guardar el ancho actual en ese espacio. Los botones se ocultan en los modos FM, NFM, DFM y NT. | —           |

## Colores de pestañas de slice e insignia

A partir de v0.9.3, los botones de pestaña de slice y el indicador **Slice badge** toman su borde, fondo activo y color de texto del singleton SliceColorManager en lugar de una tabla de colores fija. Los colores se pueden configurar por slice, se persisten entre sesiones y se reflejan consistentemente en los botones de pestaña de slice, la insignia de slice, widgets VFO y barras de metros.

## Modo NT

v0.9.3 agrega el modo **NT** al selector de modo. NT se comporta como un modo digital de las siguientes maneras:

- Utiliza los mismos presets de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El ancho del filtro se calcula a partir del valor del borde superior (igual que USB, DIGU y FDV).
- El botón **SQL** y el deslizador de nivel de silenciador se deshabilitan mientras NT está activo, y cualquier silenciador activo se apaga automáticamente (mismo comportamiento que DIGU y DIGL).

## Consejos

- No es necesario escribir ceros finales. `14.2` se interpreta como 14.200 MHz.
- Para mover la frecuencia en pasos pequeños sin reescribir, use los botones `<` y `>` junto a **STEP**, o desplace la rueda del ratón sobre la **Frequency label** después de sintonizar.
- La lista de tamaños de paso cambia cuando cambia de modo. Cambiar el **Mode combo** reinicia los presets de paso a valores apropiados para ese modo.

## Solución de problemas

- **El campo Frequency edit no aparece cuando hago clic en el indicador** — El slice puede estar bloqueado. Compruebe si el icono de bloqueo muestra 🔒. Si es así, haga clic en él para desbloquearlo, luego haga clic en el indicador de frecuencia nuevamente.
- **Se ignoró la frecuencia que escribí** — Puede haber presionado Escape en lugar de Enter, o ingresado un valor fuera del rango válido (0.001–54.000 MHz en una antena estándar, hasta 450.000 MHz en una antena transvertidor). Reingrese el valor y presione Enter.
- **El panadapter no siguió la nueva frecuencia** — Compruebe que `View > Pan Follows VFO` esté habilitado.
- **El botón SQL está atenuado después de cambiar al modo NT** — Esto es expected. NT es un modo digital; el silenciador se deshabilita automáticamente, igual que para DIGU y DIGL.

## Relacionado

- [Lock the slice to prevent accidental retuning](lock-the-slice-to-prevent-accidental-retuning.md)
- [Change mode (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Pick a filter width preset for the current mode](pick-a-filter-width-preset-for-the-current-mode.md)
- [Switch between multiple slices using the A..H tab row](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Understanding slices and VFOs](../../getting-started/concepts/understanding-slices.md)
