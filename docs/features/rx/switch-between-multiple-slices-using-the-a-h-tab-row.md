# Cambiar entre múltiples slices usando la fila de pestañas A..H

La FLEX-8600 admite hasta ocho slices de recepción simultáneos. La fila de pestañas A..H en la parte superior del applet RX Controls le permite cambiar a qué slice está vinculado el applet, para que pueda ver y ajustar el modo, la frecuencia, el filtro y otras configuraciones de cada slice de forma independiente.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet RX Controls requiere una conexión activa a la radio.
- La radio debe tener más de un slice activo. La fila de pestañas se oculta cuando existe solo un slice.
- El applet RX Controls debe ser visible. Si no lo está, haga clic en el botón RX tray en la barra lateral derecha para mostrarlo.

## Pasos

1. Busque en la parte superior del applet RX Controls la fila horizontal de pestañas con letras (A, B, C, etc., hasta H).
2. Haga clic en la pestaña de letra que corresponde al slice que desea inspeccionar o controlar.
3. Confirme el cambio: el **Slice badge** en la fila de encabezado se actualiza para mostrar la letra del slice recién seleccionado, coloreado según su identidad de slice.
4. Todos los controles debajo de la fila de pestañas —modo, frecuencia, filtro, AGC, ganancia de AF y otros— ahora reflejan y controlan el slice seleccionado.

## Qué hace cada control

| Control           | Comportamiento                                                                       | Por defecto                                                                                                                                                                                       |
|-------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1. El borde del botón y el fondo activo siguen el color por slice de SliceColorManager (v0.9.3+).                                                                    |
| Slice badge       | Muestra la letra del slice actualmente vinculado.                              | Color controlado por el singleton SliceColorManager (v0.9.3+). Los colores personalizables por slice persisten entre sesiones y se reflejan aquí, en los botones de pestaña de slice, widgets VFO y barras de medidor. |

## Comportamiento del modo NT

v0.9.3 añade `NT` como un modo digital reconocido junto con `DIGU` y `DIGL`. Los siguientes comportamientos se aplican al modo NT:

- **Presets de ancho de filtro** utilizan la misma lista de presets que DIGU y DIGL (rango 100–2000 Hz).
- **Pantalla de ancho de filtro** calcula el ancho de banda desde el borde superior, siguiendo la convención USB/DIGU/FDV.
- **Squelch** se desactiva cuando el modo NT está activo. El audio se enruta a través de DAX, por lo que el control de squelch no es relevante. Si el squelch estaba activado cuando cambió a NT, AetherSDR guarda su estado y lo desactiva automáticamente. Al cambiar de NT, se restaura el estado anterior de squelch.

## Consejos

- La fila de pestañas se oculta completamente cuando la radio reporta un número máximo de slices de 1. Si no ve pestañas, solo un slice está configurado en la radio.
- Cada slice retiene su propio modo, frecuencia, presets de filtro, configuraciones de AGC y selección de antena. Cambiar de pestaña no altera la configuración de ningún slice; solo cambia qué slice muestra el applet.
- Los presets de ancho de filtro se guardan por modo a través de la configuración `FilterPresets`. Los presets que guarda en el slice A en modo USB se aplican al modo USB en todos los slices.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Entender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Elegir un preset de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Bloquear el slice para evitar resintonía accidental](lock-the-slice-to-prevent-accidental-retuning.md)
