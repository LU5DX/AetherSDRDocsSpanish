# Uso de XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Sintonización Incremental de Transmisión) le permite desplazar su frecuencia de transmisión una cantidad fija de hercios mientras su frecuencia de recepción permanece en el VFO. Esto es útil cuando se trabaja en split, se compensa un desplazamiento de TX solicitado por la otra estación, o se iguala una frecuencia de red sin reajustar el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de XIT solo están activos cuando hay una conexión de radio presente.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón RX de la barra lateral derecha.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, desplácese hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para habilitar la Sintonización Incremental de Transmisión. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento de XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** a los lados del cuadro giratorio de desplazamiento de XIT para avanzar en incrementos de 10 Hz.
   - Pase el cursor sobre el cuadro giratorio de desplazamiento de XIT y gire la rueda del ratón para avanzar en incrementos de 10 Hz.
4. Para devolver el desplazamiento de TX a cero sin desactivar XIT, haga clic en XIT 0.
5. Para desactivar XIT, haga clic en XIT nuevamente para que el botón deje de estar iluminado.

## Qué hace cada control

| Control        | Qué hace                                                                                         | Por defecto |
|----------------|--------------------------------------------------------------------------------------------------|-------------|
| XIT            | Activa o desactiva la Sintonización Incremental de Transmisión.                                  | Desactivado |
| Desplazamiento XIT | Establece el desplazamiento de frecuencia de TX en hercios. Se ajusta con los botones **<** / **>** o la rueda del ratón. | +0 Hz       |
| XIT 0          | Restablece el desplazamiento de XIT a +0 Hz sin desactivar XIT.                                  | —           |

## Consejos

- RIT y XIT son independientes. Puede ejecutar ambos simultáneamente: RIT desplaza su frecuencia de recepción, XIT desplaza su frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Si necesita que el desplazamiento de TX persista durante una sesión, ajuste el desplazamiento de XIT antes de transmitir; permanecerá configurado hasta que haga clic en XIT 0 o desactive XIT.
- Para poner a cero el desplazamiento rápidamente antes de una transmisión, haga clic en XIT 0 en lugar de desactivar y volver a activar XIT.

## Solución de problemas

- **Los controles de XIT aparecen atenuados** — La radio no está conectada. Use `Settings > Connect to Radio...` para establecer una conexión e intente nuevamente.
- **La frecuencia de TX no se desplaza como se esperaba** — Confirme que el slice correcto esté seleccionado usando las pestañas de slice (A..H). XIT solo actúa sobre el slice vinculado actualmente.

## Colores de pestañas e insignias de slice (v0.9.3)

A partir de v0.9.3, los botones de pestaña de slice (A..H) y la insignia de slice en la esquina superior izquierda del applet se colorean mediante SliceColorManager. Cada slice tiene su propio color que persiste entre sesiones. El mismo color se refleja en los widgets de VFO y las barras de medidor para ese slice. Los colores no se pueden configurar desde el propio applet RX Controls; son gestionados centralmente por SliceColorManager y se aplican de manera consistente en todos los widgets que hacen referencia a un slice determinado.

## Formato de texto de la insignia de slice (v26.5.2.1)

A partir de v26.5.2.1, la etiqueta de la insignia de slice admite renderizado de texto enriquecido (HTML). Esto permite formatear la letra del slice con etiquetas HTML cuando sea necesario, por ejemplo, para accesibilidad o requisitos especiales de visualización. La insignia continúa mostrando la letra única del slice vinculado actualmente (A a H) con su color de identidad de slice. No se requiere ninguna acción de su parte.

## Comportamiento de la pestaña de slice al reconectar (v0.9.5.1)

En v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cuando cambia la cantidad de slices disponibles, como después de una desconexión y reconexión o cuando la radio reporta un número diferente de slices.

Anteriormente, los botones de pestaña se creaban solo una vez y nunca se reemplazaban. Ahora, si la radio reporta un número máximo de slices diferente al ya mostrado, los botones existentes se eliminan primero —quitándolos del diseño y restaurando la insignia de slice estática— antes de construir el nuevo conjunto. Esto evita que botones de pestaña obsoletos aparezcan después de la reconexión.

El controlador de clic que emite `sliceActivationRequested` se conecta solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de manejadores de señal duplicados a lo largo de las reconexiones.

No se requiere ninguna acción de su parte. La fila de pestañas se actualiza automáticamente cuando cambia la conexión de la radio.

## Comportamiento del menú de antena (v26.5.2.1)

En v26.5.2.1, los menús de antena de RX y TX se mejoraron para una mayor precisión y fiabilidad:

- **Menú de antena RX** ahora usa la `rxAntennaList()` dedicada del slice cuando está disponible, en lugar de la lista global de antenas del panadapter. Esto asegura que el menú muestre solo antenas válidas para el slice actual. Si el slice no proporciona una lista de antenas RX dedicada, se usa la lista global de antenas como alternativa.
- **Menú de antena TX** filtra explícitamente las antenas para mostrar solo aquellas adecuadas para la transmisión. El applet usa un método dedicado (`txAntennaOptions()`) que identifica las antenas capaces de TX verificando si el token de antena comienza con "ANT", "TX", o es igual a "XVTR". Las antenas que comienzan con "RX" se excluyen de las opciones de TX.
- **Los elementos del menú** ahora muestran información sobre herramientas y consejos de estado con la cadena identificadora de la antena sin procesar. El campo de datos de la acción del menú, en lugar de su texto mostrado, se usa al establecer la antena en el slice. Esto evita que el formato de visualización interfiera con la selección real de la antena.

No se requiere ninguna acción de su parte. Los menús de antena ahora muestran solo las antenas apropiadas para cada función.

## Persistencia del nivel de squelch manual (v26.5.2.1)

A partir de v26.5.2.1, el nivel de umbral de squelch manual se guarda y restaura entre sesiones. Cuando ajusta el control deslizante del nivel de squelch manualmente, el valor se almacena del lado del cliente en el archivo de configuración de AetherSDR bajo `LastManualSquelchLevel`.

Esto es necesario porque el modo de squelch automático de la radio puede sobrescribir la propiedad `squelchLevel` del slice, por lo que no se puede confiar en la radio para preservar la preferencia manual del operador. Al persistir el nivel manual en AetherSDR, el applet puede restaurar su umbral de squelch preferido cuando sale del modo automático o reinicia la aplicación.

El valor almacenado se limita al rango válido (0-100) al cargarse. El valor predeterminado es 20.

No se requiere ninguna acción de su parte. Su preferencia de squelch manual ahora se recuerda entre sesiones.

## Formato de almacenamiento de preselecciones de filtro (v0.9.5.1)

En v0.9.5.1, las preselecciones de filtro guardadas por la configuración `FilterPresets` pueden almacenar un valor de ancho de banda simple o un par explícito de borde inferior/borde superior. Esto coincide con el formato utilizado por el widget VFO.

- **Formato solo-ancho** — un solo entero en hercios, por ejemplo `2700`. El applet centra la banda de paso simétricamente alrededor de la portadora usando los bordes predeterminados del modo.
- **Formato Lo:Hi** — dos enteros separados por dos puntos, por ejemplo `300:3000`. El applet establece el borde inferior del filtro en 300 Hz y el borde superior en 3000 Hz exactamente. La etiqueta de ancho mostrada calcula la diferencia (2700 Hz en este ejemplo).

Ambos formatos pueden aparecer en el mismo valor `FilterPresets` separado por comas para un modo dado. Las entradas malformadas, aquellas con un borde superior igual o inferior al borde inferior, o que sean cero o negativas, se omiten silenciosamente.

Este cambio afecta cómo se guardan y cargan las preselecciones de filtro personalizadas, pero no cambia la forma en que interactúa con los botones de preselección de filtro. Haga clic derecho en un botón de preselección para guardar la banda de paso actual en esa ranura; haga clic en él para aplicar la preselección. El formato lo:hi se escribe automáticamente cuando guarda una preselección cuyo borde inferior difiere del predeterminado del modo.

## Comportamiento del paso de ancho de filtro (v0.9.8)

En v0.9.8, el método `stepFilterWidth()` recorre la lista de preselecciones de filtro por modo para ensanchar o estrechar la banda de paso. Esto asegura que los atajos de teclado u otros controles que avanzan por los anchos de filtro produzcan una geometría de borde correcta para el modo.

Cuando usa una acción de ensanchar/estrechar (como desde los botones Widen/Narrow en el panel VFO), el applet busca en la lista de preselecciones de filtro por modo la preselección más cercana al ancho de filtro actual. Luego aplica la siguiente preselección más ancha o más estrecha de esa lista. Si el ancho actual coincide exactamente con una preselección, la siguiente preselección en la dirección elegida se aplica directamente.

Este comportamiento se aplica a todos los modos: LSB, CWL, DIGL, RTTY, AM, CW y USB. Los modos de la familia FM (FM, NFM, DFM) no tienen preselecciones de filtro e ignoran la acción de paso.

No se necesita configuración. El comportamiento de paso usa la misma configuración `FilterPresets` que puede personalizar guardando con clic derecho.

## Formato de la etiqueta de ancho de filtro (v0.9.8)

En v0.9.8, la lectura del ancho de filtro (compartida con el panel VFO a través de `RxApplet::formatFilterWidth`) usa lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto. Esto asegura lecturas consistentes entre el applet RX Controls y el panel VFO, según se referencia en el issue #2197. No se requiere ninguna acción de su parte.

## Comportamiento del modo NT

El modo NT se trata como un modo digital en el applet RX Controls. Específicamente:

- NT sigue las mismas preselecciones de ancho de filtro y tamaños de paso que DIGU y DIGL.
- La etiqueta de ancho de filtro calcula el ancho de banda de la misma manera que DIGU (usando el valor del borde superior).
- El botón SQL y el control deslizante del nivel de squelch están desactivados cuando NT está activo, porque el audio se enruta a través de DAX y el squelch no tiene sentido. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y el estado anterior se guarda para restaurarlo cuando salga del modo NT.

## Comportamiento del squelch en modo RTTY y modos digitales (v26.5.1)

A partir de v26.5.1, los controles de squelch (botón SQL y control deslizante del nivel de squelch) también están desactivados en modo RTTY, además de los modos digitales existentes (DIGU, DIGL) y el modo NT. Este cambio asegura que el squelch no enmascare los caracteres FSK, lo que de otro modo interrumpiría la decodificación.

Cuando cambia al modo RTTY:
- El botón SQL y el control deslizante del nivel de squelch se desactivan automáticamente.
- Si el squelch estaba activado cuando cambió a RTTY, se desactiva automáticamente y el estado anterior se guarda para restaurarlo cuando salga del modo RTTY o digital.
- Los modos CW (CW, CWL) continúan teniendo el squelch desactivado como antes, y el estado del squelch es gestionado por la propia radio.

## Seguridad del modo RADE (v26.5.2.1)

En v26.5.2.1, la lógica de desactivación del modo RADE se actualizó para reflejar que "RADE" es un modo solo del lado del cliente. La radio en sí misma no entiende RADE como un modo distinto — cuando RADE está activo, la radio devuelve el modo real subyacente (DIGL o DIGU) inmediatamente.

Anteriormente, el applet verificaba `m_slice->mode() == "RADE"` antes de emitir una señal de desactivación. Debido a que la radio reporta inmediatamente el modo real después de configurar RADE, esta condición nunca podía cumplirse. Esto afectaba los siguientes escenarios:
- Cambio entre modos no RADE en un slice que nunca estuvo en RADE.
- RADE fue activado externamente (a través del combo del widget VFO, carga de perfil al inicio, o `MainWindow::activateRADE`).
- El slice se re-vincula a un slice diferente mediante `setSlice()`.

No se requiere ninguna acción de su parte. El comportamiento de desactivación del modo RADE ahora se alinea correctamente con la naturaleza de solo lado del cliente del modo.

## Estado de silencio de audio al reconectar (v0.9.10)

En v0.9.10, el estado del botón de silencio (🔊 / 🔇) NO se guarda ni restaura cuando la conexión con la radio se pierde y se restablece. La radio es la fuente de verdad para el estado de silencio de audio, según la Política de Configuración Autoritativa de la Radio (#2489). Después de desconectarse y reconectarse, el botón de silencio refleja el estado de silencio real reportado por la radio, que puede ser diferente de lo que era antes de la desconexión.

## Relacionado

- [Use RIT para desplazar la frecuencia de recepción para una estación a la deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Sintonice la radio a una frecuencia (escriba MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambie entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Visión general de RX Controls](overview.md)
