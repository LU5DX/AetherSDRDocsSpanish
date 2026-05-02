# Cambiar entre múltiples slices usando la fila de pestañas A..H

El FLEX-8600 admite hasta ocho slices de recepción simultáneos. La fila de pestañas A..H en la parte superior del applet RX Controls permite cambiar a qué slice está vinculado el applet, de modo que pueda ver y ajustar el modo, la frecuencia, el filtro y otros ajustes de cada slice de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El applet RX Controls requiere una conexión de radio activa.
- El radio debe tener más de un slice activo. La fila de pestañas se oculta cuando existe un solo slice.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.

## Pasos

1. Busque en la parte superior del applet RX Controls la fila horizontal de pestañas con letras (A, B, C, y así sucesivamente hasta H).
2. Haga clic en la letra de la pestaña que corresponde al slice que desea inspeccionar o controlar.
3. Confirme el cambio: el **Slice badge** en la fila de encabezado se actualiza para mostrar la letra del slice recién seleccionado, con el color correspondiente a su identidad de slice.
4. Todos los controles debajo de la fila de pestañas — modo, frecuencia, filtro, AGC, ganancia de audio y otros — ahora reflejan y controlan el slice seleccionado.

## Qué hace cada control

| Control           | Comportamiento                                                                       | Notas                                                                                                                                                                                                                                                     |
|-------------------|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. | La fila se oculta si maxSlices <= 1. `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura el Slice badge estático al desconectar (v0.9.5.1, #2254). Las conexiones de clic de los botones de slice están protegidas contra manejadores de señal duplicados entre reconexiones. |
| Slice badge       | Muestra la letra del slice vinculado actualmente.                              | Con el color correspondiente a la identidad del slice.                                                                                                                                                                                                      |

## Comportamiento del modo NT

La versión v0.9.3 agrega `NT` como modo digital reconocido junto a `DIGU` y `DIGL`. Los siguientes comportamientos aplican al modo NT:

- **Los preajustes de ancho de filtro** utilizan la misma lista de preajustes que DIGU y DIGL (rango de 100–2000 Hz).
- **La visualización del ancho de filtro** calcula el ancho de banda desde el borde superior, siguiendo la convención de USB/DIGU/FDV.
- **El squelch** se deshabilita cuando el modo NT está activo. El audio se enruta mediante DAX, por lo que el control de squelch no es relevante. Si el squelch estaba activado al cambiar a NT, AetherSDR guarda su estado y lo desactiva automáticamente. Al salir del modo NT, se restaura el estado anterior del squelch.

## Formato de almacenamiento de preajustes de filtro

A partir de v0.9.5.1, los preajustes de filtro guardados bajo la clave de configuración `FilterPresets` pueden almacenar un valor de ancho simple o una banda de paso completamente especificada como par `lo:hi` (#2259). Esto coincide con el formato utilizado por VfoWidget.

- Una entrada simple como `2700` registra únicamente el ancho del filtro. Al aplicarse, AetherSDR centra la banda de paso alrededor del punto de portadora actual.
- Una entrada `lo:hi` como `-1400:1300` registra ambos bordes. Al aplicarse, AetherSDR restaura tanto la posición exacta de la banda de paso como el ancho.

Al hacer clic derecho en un botón de **Filter width presets** se guarda la banda de paso actual en formato `lo:hi`, de modo que ambos bordes se conserven al recargar. Las entradas de ancho simple guardadas por versiones anteriores siguen siendo válidas y se leen sin errores.

## Consejos

- La fila de pestañas se oculta por completo cuando el radio reporta un número máximo de slices igual a 1. Si no ve ninguna pestaña, solo hay un slice configurado en el radio.
- Si el número de slices activos cambia mientras AetherSDR está conectado, la fila de pestañas se reconstruye automáticamente. El conjunto anterior de botones es eliminado por `clearSliceButtons()` antes de crear los nuevos botones, lo que evita la acumulación de manejadores de clic obsoletos entre reconexiones.
- Cada slice conserva su propio modo, frecuencia, preajustes de filtro, ajustes de AGC y selección de antena. Cambiar de pestaña no altera los ajustes de ningún slice; solo cambia cuál slice muestra el applet.
- Los preajustes de ancho de filtro se guardan por modo mediante la configuración `FilterPresets`. Los preajustes que guarde en el slice A en modo USB se aplican al modo USB en todos los slices.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Descripción de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
- [Sintonizar el radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Bloquear el slice para evitar una resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
<!-- docmesh:llm version=v0.9.5.1 date=2026-05-01 -->
