# Bloquear la slice para evitar retunización accidental

La función de bloqueo de sintonización impide que una slice responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin riesgo de mover accidentalmente el VFO haciendo clic en el panadapter o desplazando la rueda del ratón.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa a la radio.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX en la barra lateral derecha para mostrarlo.

## Pasos

1. En el applet RX Controls, identifique la fila de encabezado que contiene la insignia de slice, el botón de bloqueo y los selectores de antena.
2. Si tiene más de una slice, haga clic en la pestaña de slice correspondiente (A a H) para seleccionar la slice que desea bloquear.
3. Haga clic en el botón 🔓 en la fila de encabezado. El icono cambia a 🔒 y se vuelve azul, confirmando que la slice está bloqueada.
4. Para desbloquear, haga clic en 🔒 nuevamente. El icono vuelve a 🔓 y la slice reanuda la respuesta a cambios de frecuencia.

## Qué hace cada control

| Control | Por defecto  | Comportamiento                                                                                                          |
|---------|--------------|-------------------------------------------------------------------------------------------------------------------------|
| 🔓 / 🔒   | 🔓 (desbloqueado) | Activa/desactiva el bloqueo de sintonización en la slice activa. Cuando está bloqueada (🔒), la slice ignora todos los cambios de frecuencia. Haga clic nuevamente para desbloquear. |

## Consejos

- El estado de bloqueo se aplica por slice. Puede bloquear la slice A mientras la slice B permanece libremente sintonizable.
- El botón de bloqueo siempre es visible en la fila de encabezado independientemente del modo actual.
- A partir de v0.9.3, los botones de pestaña de slice y la insignia de slice utilizan colores por slice administrados por SliceColorManager. Los colores se pueden personalizar por slice y persisten entre sesiones. El mismo color se refleja en los botones de pestaña de slice, la insignia de slice, los widgets VFO y las barras de medidores.

## Modo NT

La versión 0.9.3 añade el modo `NT` junto con los modos digitales existentes (`DIGU`, `DIGL`). Se comporta de manera idéntica a otros modos digitales de las siguientes formas:

- **Preajustes de filtro** — NT comparte el conjunto de preajustes de filtro DIG (100–2000 Hz). La etiqueta de ancho de filtro se actualiza en consecuencia.
- **Cálculo del ancho de filtro** — La pantalla de ancho de filtro mide el desplazamiento del borde superior, igual que USB y DIGU.
- **Squelch** — El botón SQL y el regulador de squelch están deshabilitados en modo NT. Debido a que el audio se enruta a través de DAX en modos digitales, el squelch no es significativo. Si el squelch estaba activo cuando cambió al modo NT, AetherSDR lo desactiva automáticamente y lo restaura cuando sale del modo NT.

## Relacionado

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
