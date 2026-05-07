# Bloquear el slice para evitar una sintonización accidental

La función de bloqueo de sintonía impide que un slice responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin el riesgo de mover el VFO al hacer clic en el panadapter o al girar la rueda del mouse.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa a la radio.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX de la barra lateral derecha para mostrarlo.

## Pasos

1. En el applet RX Controls, identifique la fila de encabezado que contiene la insignia del slice, el botón de bloqueo y los selectores de antena.
2. Si tiene más de un slice, haga clic en la pestaña del slice correspondiente (A a H) para seleccionar el slice que desea bloquear.
3. Haga clic en el botón 🔓 de la fila de encabezado. El ícono cambia a 🔒 y se vuelve azul, confirmando que el slice está bloqueado.
4. Para desbloquear, haga clic en 🔒 nuevamente. El ícono regresa a 🔓 y el slice vuelve a responder a los cambios de frecuencia.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento                                                                                                           |
|---------|----------------------|--------------------------------------------------------------------------------------------------------------------------|
| 🔓 / 🔒 | 🔓 (desbloqueado)    | Alterna el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los cambios de frecuencia. Vuelva a hacer clic para desbloquear. |

## Consejos

- El estado de bloqueo se aplica por slice. Puede bloquear el slice A mientras el slice B permanece libremente sintonizable.
- El botón de bloqueo siempre está visible en la fila de encabezado, independientemente del modo actual.
- Desde la versión v0.9.3, los botones de las pestañas de slice y la insignia del slice usan colores por slice gestionados por SliceColorManager. Los colores son personalizables por slice y persisten entre sesiones. El mismo color se refleja en los botones de las pestañas de slice, la insignia del slice, los widgets de VFO y las barras de medidor.

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

Cuando la radio se desconecta o cambia el número de slices disponibles, AetherSDR elimina todos los botones de pestañas de slice generados y restaura automáticamente la insignia estática del slice (`clearSliceButtons()`, #2254). Al reconectar, la fila de pestañas se reconstruye para coincidir con el nuevo número de slices. Si el número no ha cambiado, los botones existentes se reutilizan sin reconstrucción.

Las conexiones de señal entre el grupo de botones de slice y el manejador `sliceActivationRequested` están protegidas para que reconectar la radio no acumule manejadores de señal duplicados.

## Formato de almacenamiento de preajustes de filtro (v0.9.5.1)

Los preajustes de filtro guardados para un modo determinado (clave de configuración `FilterPresets`) ahora admiten dos formatos de almacenamiento:

- **Solo ancho** — un número entero que representa el ancho de banda del filtro en Hz (por ejemplo, `2700`). Este es el formato heredado y sigue funcionando.
- **Lo:Hi** — un par separado por dos puntos de compensaciones de borde inferior y superior en Hz (por ejemplo, `-1400:1300`). Este formato preserva una banda de paso asimétrica exactamente como la configuró arrastrando los bordes del widget de la banda de paso del filtro.

Cuando hace clic derecho en un botón de preajuste de filtro para guardar el ancho actual, AetherSDR escribe el formato `lo:hi` cuando la banda de paso es asimétrica (#2259). Los preajustes guardados en el formato antiguo de solo ancho se leen y aplican como bandas de paso centradas, exactamente como antes.

Se almacenan y muestran hasta seis preajustes por modo en el applet RX Controls. Los botones se ocultan para los modos FM, NFM y DFM.

## Ancho de filtro por pasos (v0.9.8)

El sistema de preajustes de ancho de filtro ahora admite un método `stepFilterWidth()` que recorre la lista de preajustes por modo. Esto permite accesos directos de ampliación/reducción que producen una geometría de borde correcta para el modo en todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB).

Cuando aplica una operación de ampliación o reducción:

- AetherSDR encuentra el ancho de preajuste más cercano a la banda de paso del filtro actual.
- Luego selecciona el siguiente preajuste más ancho o más angosto de la lista por modo.
- El preajuste se aplica mediante `applyFilterPreset()`, que utiliza las compensaciones de borde correctas para el modo actual.

Esto garantiza que ampliar o reducir un filtro siempre se mantenga dentro de los valores de preajuste apropiados para el modo y produzca la geometría de banda de paso correcta.

## Formato del ancho de filtro (v0.9.8)

El método `formatFilterWidth()` ahora es una función estática pública, compartida con el panel VFO (`VfoWidget`). Esto asegura que tanto el applet RX Controls como el panel VFO muestren lecturas de ancho de filtro idénticas. El método utiliza lógica consciente del modo, por lo que los modos SSB y digitales muestran el ancho etiquetado correcto (#2197).

## Modo NT

La versión 0.9.3 agrega el modo `NT` junto a los modos digitales existentes (`DIGU`, `DIGL`). Se comporta de manera idéntica a otros modos digitales en los siguientes aspectos:

- **Preajustes de filtro** — NT comparte el conjunto de preajustes de filtro DIG (100–2000 Hz). La etiqueta de ancho de filtro se actualiza en consecuencia.
- **Cálculo del ancho de filtro** — La visualización del ancho de filtro mide la compensación del borde superior, igual que USB y DIGU.
- **Squelch** — El botón SQL y el control deslizante de squelch están deshabilitados en modo NT. Debido a que el audio se enruta a través de DAX en modos digitales, el squelch no tiene sentido. Si el squelch estaba activo al cambiar al modo NT, AetherSDR lo desactiva automáticamente y lo restaura al salir del modo NT.

## Relacionados

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
