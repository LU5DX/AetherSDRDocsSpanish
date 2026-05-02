# Bloquear el slice para evitar la sintonización accidental

La función de bloqueo de sintonía impide que un slice responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin riesgo de mover el VFO al hacer clic en el panadapter o desplazar la rueda del ratón.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión de radio activa.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.

## Pasos

1. En el applet RX Controls, identifique la fila de encabezado que contiene la insignia del slice, el botón de bloqueo y los selectores de antena.
2. Si tiene más de un slice, haga clic en la pestaña correspondiente (A hasta H) para seleccionar el slice que desea bloquear.
3. Haga clic en el botón 🔓 de la fila de encabezado. El ícono cambia a 🔒 y se vuelve azul, confirmando que el slice está bloqueado.
4. Para desbloquear, haga clic en 🔒 nuevamente. El ícono vuelve a 🔓 y el slice reanuda la respuesta a los cambios de frecuencia.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento                                                                                                                              |
|---------|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| 🔓 / 🔒   | 🔓 (desbloqueado)     | Activa o desactiva el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los cambios de frecuencia. Haga clic nuevamente para desbloquear. |

## Consejos

- El estado de bloqueo se aplica por slice. Puede bloquear el slice A mientras el slice B permanece libremente sintonizable.
- El botón de bloqueo siempre es visible en la fila de encabezado, independientemente del modo actual.
- A partir de la versión v0.9.3, los botones de pestaña del slice y la insignia del slice utilizan colores por slice gestionados por SliceColorManager. Los colores son personalizables por slice y persisten entre sesiones. El mismo color se refleja en los botones de pestaña del slice, la insignia del slice, los widgets de VFO y las tiras de medidores.

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

Cuando el radio se desconecta o cambia el número de slices disponibles, AetherSDR elimina todos los botones de pestaña de slice generados y restaura automáticamente la insignia estática del slice (`clearSliceButtons()`, #2254). Al reconectar, la fila de pestañas se reconstruye para coincidir con el nuevo número de slices. Si el número no ha cambiado, los botones existentes se reutilizan sin reconstrucción.

Las conexiones de señal entre el grupo de botones de slice y el manejador `sliceActivationRequested` están protegidas para que la reconexión al radio no acumule manejadores de señal duplicados.

## Formato de almacenamiento de preajustes de filtro (v0.9.5.1)

Los preajustes de filtro guardados para un modo determinado (clave de configuración `FilterPresets`) admiten ahora dos formatos de almacenamiento:

- **Solo ancho** — un entero simple que representa el ancho de banda del filtro en Hz (por ejemplo, `2700`). Este es el formato heredado y sigue funcionando.
- **Lo:Hi** — un par separado por dos puntos con los desplazamientos del borde inferior y superior en Hz (por ejemplo, `-1400:1300`). Este formato preserva una banda de paso asimétrica exactamente tal como se configuró al arrastrar los bordes del widget de banda de paso del filtro.

Al hacer clic derecho en un botón de preajuste de filtro para guardar el ancho actual, AetherSDR escribe la forma `lo:hi` cuando la banda de paso es asimétrica (#2259). Los preajustes guardados en el formato antiguo de solo ancho se leen y aplican como bandas de paso centradas, exactamente como antes.

Se almacenan y muestran hasta seis preajustes por modo en el applet RX Controls. Los botones se ocultan para los modos FM, NFM y DFM.

## Modo NT

La versión 0.9.3 añade el modo `NT` junto a los modos digitales existentes (`DIGU`, `DIGL`). Se comporta de manera idéntica a otros modos digitales en los siguientes aspectos:

- **Preajustes de filtro** — NT comparte el conjunto de preajustes de filtro DIG (100–2000 Hz). La etiqueta de ancho de filtro se actualiza en consecuencia.
- **Cálculo del ancho de filtro** — La visualización del ancho de filtro mide el desplazamiento del borde superior, igual que USB y DIGU.
- **Silenciador** — El botón SQL y el control deslizante de silenciador están desactivados en el modo NT. Dado que el audio se enruta a través de DAX en los modos digitales, el silenciador no tiene utilidad. Si el silenciador estaba activo al cambiar al modo NT, AetherSDR lo desactiva automáticamente y lo restaura al salir del modo NT.

## Relacionado

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el visualizador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
