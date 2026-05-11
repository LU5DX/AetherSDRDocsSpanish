# Bloquear el slice para evitar una sintonización accidental

La función de bloqueo de sintonía evita que un slice responda a cambios de frecuencia. Úsela cuando desee monitorear una frecuencia fija sin el riesgo de mover el VFO al hacer clic en el panadapter o al girar la rueda del mouse.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión de radio activa.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX de la barra lateral derecha para mostrarlo.

## Pasos

1. En el applet RX Controls, identifique la fila de encabezado que contiene la insignia del slice, el botón de bloqueo y los selectores de antena.
2. Si tiene más de un slice, haga clic en la pestaña del slice correspondiente (A a la H) para seleccionar el slice que desea bloquear.
3. Haga clic en el botón 🔓 en la fila de encabezado. El ícono cambia a 🔒 y se vuelve azul, lo que confirma que el slice está bloqueado.
4. Para desbloquear, haga clic nuevamente en 🔒. El ícono vuelve a 🔓 y el slice reanuda la respuesta a los cambios de frecuencia.

## Función de cada control

| Control | Valor predeterminado | Comportamiento |
|---------|----------------------|----------------|
| 🔓 / 🔒 | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía en el slice activo. Cuando está bloqueado (🔒), el slice ignora todos los cambios de frecuencia. Vuelva a hacer clic para desbloquear. |

## Consejos

- El estado de bloqueo se aplica por slice. Puede bloquear el slice A mientras el slice B permanece libremente sintonizable.
- El botón de bloqueo siempre está visible en la fila de encabezado, independientemente del modo actual.
- Desde la versión v0.9.3, los botones de pestaña del slice y la insignia del slice usan colores por slice administrados por SliceColorManager. Los colores son personalizables por slice y persisten entre sesiones. El mismo color se refleja en los botones de pestaña del slice, la insignia del slice, los widgets VFO y las tiras del medidor.

## Comportamiento de las pestañas del slice al reconectar (v0.9.5.1)

Cuando la radio se desconecta o cambia la cantidad de slices disponibles, AetherSDR elimina todos los botones de pestaña de slice generados y restaura automáticamente la insignia estática del slice (`clearSliceButtons()`, #2254). Al reconectar, la fila de pestañas se reconstruye para coincidir con la nueva cantidad de slices. Si la cantidad no ha cambiado, los botones existentes se reutilizan sin reconstrucción.

Las conexiones de señal entre el grupo de botones del slice y el manejador `sliceActivationRequested` están protegidas para que la reconexión a la radio no acumule manejadores de señal duplicados.

## Formato de almacenamiento de presets de filtro (v0.9.5.1)

Los presets de filtro guardados para un modo determinado (clave de configuración `FilterPresets`) ahora admiten dos formatos de almacenamiento:

- **Solo ancho** — un número entero simple que representa el ancho de banda del filtro en Hz (por ejemplo, `2700`). Este es el formato heredado y sigue funcionando.
- **Lo:Hi** — un par separado por dos puntos de los desplazamientos del borde inferior y superior en Hz (por ejemplo, `-1400:1300`). Este formato conserva exactamente una banda de paso asimétrica tal como la configuró arrastrando los bordes del widget de la banda de paso del filtro.

Cuando hace clic derecho en un botón de preset de filtro para guardar el ancho actual, AetherSDR escribe la forma `lo:hi` cuando la banda de paso es asimétrica (#2259). Los presets guardados en el formato antiguo de solo ancho se leen y se aplican como bandas de paso centradas, exactamente como antes.

Se almacenan y muestran hasta seis presets por modo en el applet RX Controls. Los botones están ocultos para los modos FM, NFM y DFM.

## Ancho de filtro por pasos (v0.9.8)

El sistema de presets de ancho de filtro ahora admite un método `stepFilterWidth()` que recorre la lista de presets por modo. Esto permite atajos de ampliación/reducción que producen una geometría de bordes correcta para el modo en todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB).

Cuando aplica una operación de ampliación o reducción:

- AetherSDR encuentra el preset de ancho más cercano que coincida con la banda de paso actual del filtro.
- Luego selecciona el preset siguiente más ancho o más estrecho de la lista por modo.
- El preset se aplica mediante `applyFilterPreset()`, que utiliza los desplazamientos de bordes correctos para el modo actual.

Esto garantiza que al ampliar o reducir un filtro, siempre se mantenga dentro de los valores de preset apropiados para el modo y se produzca la geometría de banda de paso correcta.

## Formato del ancho de filtro (v0.9.8)

El método `formatFilterWidth()` ahora es una función estática pública, compartida con el panel VFO (`VfoWidget`). Esto asegura que tanto el applet RX Controls como el panel VFO muestren lecturas de ancho de filtro idénticas. El método utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto (#2197).

## Comportamiento del squelch en modo NT y RTTY (v26.5.1)

El squelch está deshabilitado en modo NT, modo RTTY y los modos digitales existentes (`DIGU`, `DIGL`). Esto evita que el squelch compuerta señales FSK débiles y recorte caracteres, lo que interrumpiría la decodificación (#2504). Si el squelch estaba activo cuando cambió a RTTY o a un modo digital, AetherSDR lo desactiva automáticamente y guarda el estado para poder restaurarlo cuando salga del modo. El botón y el deslizador de squelch permanecen deshabilitados mientras el modo esté activo.

## Activación del modo RADE (v26.5.1)

Cuando selecciona el modo RADE en el cuadro combinado de modos, el modo del slice se establece inmediatamente en el slice antes de emitir la señal `radeActivated`. Al cambiar del modo RADE a cualquier otro modo, la desactivación `radeActivated(false)` solo se emite si el slice estaba realmente en modo RADE antes del cambio. Esta lógica de defensa en profundidad evita señales de desactivación espurias en los siguientes escenarios:

- Intercambio entre modos que no son RADE (por ejemplo, USB a LSB) en un slice que nunca estuvo en RADE — no se envía ninguna señal de desactivación.
- Reenlace de un slice mediante `setSlice()` — el modo actual siempre se lee del slice enlazado, no de una marca residual.
- RADE activado externamente (mediante el combo VFO, carga de perfil al inicio o `MainWindow::activateRADE`) — el modo del slice es `"RADE"` independientemente de cómo se haya activado, por lo que la desactivación se envía correctamente.

## Modo NT

La versión 0.9.3 agrega el modo `NT` junto con los modos digitales existentes (`DIGU`, `DIGL`). Se comporta de manera idéntica a otros modos digitales en los siguientes aspectos:

- **Presets de filtro** — NT comparte el conjunto de presets de filtro DIG (100–2000 Hz). La etiqueta de ancho de filtro se actualiza en consecuencia.
- **Cálculo del ancho de filtro** — La visualización del ancho de filtro mide el desplazamiento del borde superior, igual que USB y DIGU.
- **Squelch** — El botón SQL y el deslizador de squelch están deshabilitados en modo NT. Debido a que el audio se enruta a través de DAX en los modos digitales, el squelch no tiene sentido. Si el squelch estaba activo cuando cambió al modo NT, AetherSDR lo desactiva automáticamente y lo restaura cuando sale del modo NT.

## Relacionado

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en el visualizador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
