# Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Sintonización Incremental de Transmisión) permite desplazar la frecuencia de transmisión en una cantidad fija de hercios mientras la frecuencia de recepción permanece en el VFO. Esto es útil cuando se trabaja en split, se compensa un desplazamiento de TX solicitado por la otra estación, o se ajusta a una frecuencia de red sin re-sintonizar el panadapter.

## Antes de empezar

- AetherSDR debe estar conectado al equipo de radio. Los controles XIT solo están activos cuando hay una conexión con el equipo.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón RX de la bandeja en la barra lateral derecha.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, desplácese hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para habilitar la Sintonización Incremental de Transmisión. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** que flanquean el cuadro de desplazamiento XIT para incrementar en pasos de 10 Hz.
   - Coloque el cursor sobre el cuadro de desplazamiento XIT y gire la rueda del ratón para incrementar en pasos de 10 Hz.
4. Para devolver el desplazamiento de TX a cero sin deshabilitar XIT, haga clic en XIT 0.
5. Para desactivar XIT, haga clic en XIT nuevamente para que el botón deje de estar iluminado.

## Qué hace cada control

| Control       | Qué hace                                                                                         | Valor predeterminado |
|---------------|--------------------------------------------------------------------------------------------------|----------------------|
| XIT           | Activa o desactiva la Sintonización Incremental de Transmisión.                                   | Desactivado          |
| Desplazamiento XIT | Establece el desplazamiento de frecuencia de TX en hercios. Se ajusta con los botones **<**/**>** o la rueda del ratón. | +0 Hz                |
| XIT 0         | Restablece el desplazamiento XIT a +0 Hz sin desactivar XIT.                                     | —                    |

## Consejos

- RIT y XIT son independientes. Puede ejecutar ambos simultáneamente: RIT desplaza su frecuencia de recepción, XIT desplaza su frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Si necesita que el desplazamiento de TX persista durante una sesión, ajuste el desplazamiento XIT antes de transmitir; permanecerá configurado hasta que haga clic en XIT 0 o desactive XIT.
- Para poner a cero el desplazamiento rápidamente antes de una transmisión, haga clic en XIT 0 en lugar de desactivar y volver a activar XIT.

## Solución de problemas

- **Los controles XIT están atenuados** — El equipo no está conectado. Use `Settings > Connect to Radio...` para establecer una conexión y luego intente nuevamente.
- **La frecuencia de TX no se desplaza como se espera** — Confirme que el slice correcto está seleccionado usando las pestañas de slice (A..H). XIT solo actúa sobre el slice actualmente vinculado.

## Colores de pestañas y distintivos de slice (v0.9.3)

A partir de la v0.9.3, los botones de pestaña de slice (A..H) y el distintivo de slice en la esquina superior izquierda del applet se colorean mediante el SliceColorManager. Cada slice tiene su propio color que persiste entre sesiones. El mismo color se refleja en los widgets VFO y las tiras de medidor para ese slice. Los colores no se pueden configurar desde el propio applet RX Controls; son gestionados centralmente por SliceColorManager y se aplican de manera consistente en todos los widgets que hacen referencia a un slice determinado.

## Formato de texto del distintivo de slice (v26.5.2.1)

A partir de la v26.5.2.1, la etiqueta del distintivo de slice admite renderizado de texto enriquecido (HTML). Esto permite que la letra del slice se formatee con etiquetas HTML cuando sea necesario, por ejemplo, para accesibilidad o requisitos de visualización especiales. El distintivo continúa mostrando la letra única del slice actualmente vinculado (A a H) con su color de identidad de slice. No se requiere ninguna acción de su parte.

## Comportamiento de la pestaña de slice al reconectar (v0.9.5.1)

En la v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cuando el número de slices disponibles cambia, por ejemplo, después de una desconexión y reconexión o después de que el equipo informe un número de slices diferente.

Anteriormente, los botones de pestaña se creaban solo una vez y nunca se reemplazaban. Ahora, si el equipo informa un número máximo de slices diferente al ya mostrado, los botones existentes se eliminan primero —quitándolos del diseño y restaurando el distintivo de slice estático— antes de construir el nuevo conjunto. Esto evita que aparezcan botones de pestaña obsoletos después de la reconexión.

El controlador de clic que emite `sliceActivationRequested` se conecta solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita que se acumulen manejadores de señales duplicados a través de reconexiones.

No se requiere ninguna acción de su parte. La fila de pestañas se actualiza automáticamente cuando la conexión con el equipo cambia.

## Comportamiento del menú de antena (v26.5.2.1)

En la v26.5.2.1, los menús de antena RX y TX mejoraron para una mayor precisión y fiabilidad:

- **Menú de antena RX** ahora utiliza la `rxAntennaList()` dedicada del slice cuando está disponible, en lugar de la lista global de antenas del panadapter. Esto asegura que el menú muestre solo antenas válidas para el slice actual. Si el slice no proporciona una lista dedicada de antenas RX, se utiliza la lista global de antenas como respaldo.
- **Menú de antena TX** filtra explícitamente las antenas para mostrar solo aquellas adecuadas para la transmisión. El applet utiliza un método dedicado (`txAntennaOptions()`) que identifica las antenas capaces de TX verificando si el token de la antena comienza con "ANT", "TX", o es igual a "XVTR". Las antenas que comienzan con "RX" se excluyen de las opciones de TX.
- Los **elementos del menú** ahora muestran tooltips y consejos de estado que indican la cadena de identificación de la antena sin procesar. El campo de datos de la acción del menú, en lugar de su texto mostrado, se usa al establecer la antena en el slice. Esto evita que el formato de visualización interfiera con la selección real de la antena.

No se requiere ninguna acción de su parte. Los menús de antena ahora muestran solo antenas apropiadas para cada función.

## Persistencia del nivel de squelch manual (v26.5.2.1)

A partir de la v26.5.2.1, el nivel de umbral de squelch manual se guarda y restaura entre sesiones. Cuando ajusta el control deslizante del nivel de squelch manualmente, el valor se almacena del lado del cliente en el archivo de configuración de AetherSDR bajo `LastManualSquelchLevel`.

Esto es necesario porque el modo de squelch automático del equipo puede sobrescribir la propiedad `squelchLevel` del slice, por lo que no se puede confiar en el equipo para preservar la preferencia manual del operador. Al persistir el nivel manual en AetherSDR, el applet puede restaurar su umbral de squelch preferido cuando salga del modo automático o reinicie la aplicación.

El valor almacenado se limita al rango válido (0-100) al cargarse. El valor predeterminado es 20.

No se requiere ninguna acción de su parte. Su preferencia de squelch manual ahora se recuerda entre sesiones.

## Formato de almacenamiento de preselecciones de filtro (v0.9.5.1)

En la v0.9.5.1, las preselecciones de filtro guardadas por el ajuste `FilterPresets` pueden almacenar un valor simple de ancho de banda o un par explícito de borde inferior/borde superior. Esto coincide con el formato utilizado por el widget VFO.

- **Formato de solo ancho** — un solo entero en hercios, por ejemplo `2700`. El applet centra la banda de paso simétricamente alrededor de la portadora utilizando los bordes predeterminados del modo.
- **Formato Lo:Hi** — dos enteros separados por dos puntos, por ejemplo `300:3000`. El applet establece el borde inferior del filtro en 300 Hz y el borde superior en 3000 Hz exactamente. La etiqueta de ancho mostrada muestra la diferencia calculada (2700 Hz en este ejemplo).

Ambos formatos pueden aparecer en el mismo valor de `FilterPresets` separado por comas para un modo determinado. Las entradas que son mal formadas, tienen un borde superior igual o inferior al borde inferior, o son cero o negativas se omiten silenciosamente.

Este cambio afecta cómo se guardan y cargan las preselecciones de filtro personalizadas, pero no cambia cómo interactúa con los botones de preselección de filtro. Haga clic derecho en un botón de preselección para guardar la banda de paso actual en esa ranura; haga clic en él para aplicar la preselección. El formato lo:hi se escribe automáticamente cuando guarda una preselección cuyo borde inferior difiere del valor predeterminado del modo.

## Comportamiento del paso de ancho de filtro (v0.9.8)

En la v0.9.8, el método `stepFilterWidth()` recorre la lista de preselecciones de filtro por modo para ensanchar o estrechar la banda de paso. Esto asegura que los atajos de teclado u otros controles que recorren los anchos de filtro produzcan una geometría de borde correcta para el modo.

Cuando usa una acción de ensanchar/estrechar (como desde los botones Widen/Narrow en el panel VFO), el applet busca en la lista de preselecciones de filtro por modo la preselección más cercana al ancho de filtro actual. Luego aplica la siguiente preselección más ancha o más estrecha de esa lista. Si el ancho actual coincide exactamente con una preselección, se aplica directamente la siguiente preselección en la dirección elegida.

Este comportamiento se aplica a todos los modos: LSB, CWL, DIGL, RTTY, AM, CW y USB. Los modos de la familia FM (FM, NFM, DFM) no tienen preselecciones de filtro e ignoran la acción de paso.

No se necesita configuración. El comportamiento de paso utiliza el mismo ajuste `FilterPresets` que puede personalizar con el guardado con clic derecho.

## Formato de la etiqueta de ancho de filtro (v0.9.8)

En la v0.9.8, la lectura del ancho de filtro (compartida con el panel VFO a través de `RxApplet::formatFilterWidth`) utiliza lógica consciente del modo para que los modos SSB y digitales muestren el ancho etiquetado correcto. Esto asegura lecturas consistentes entre el applet RX Controls y el panel VFO, como se referencia en el problema #2197. No se requiere ninguna acción de su parte.

## Comportamiento del modo NT

El modo NT se trata como un modo digital por el applet RX Controls. Específicamente:

- NT sigue las mismas preselecciones de ancho de filtro y tamaños de paso que DIGU y DIGL.
- La etiqueta de ancho de filtro calcula el ancho de banda de la misma manera que DIGU (usando el valor del borde superior).
- El botón SQL y el control deslizante del nivel de squelch están deshabilitados cuando NT está activo, porque el audio se enruta a través de DAX y el squelch no tiene sentido. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y el estado anterior se guarda para su restauración cuando salga del modo NT.

## Comportamiento del squelch en modos RTTY y digitales (v26.5.1)

A partir de la v26.5.1, los controles de squelch (botón SQL y control deslizante del nivel de squelch) también están deshabilitados en modo RTTY, además de los modos digitales existentes (DIGU, DIGL) y el modo NT. Este cambio asegura que el squelch no elimine los caracteres FSK, lo que de otro modo rompería la decodificación.

Cuando cambia al modo RTTY:
- El botón SQL y el control deslizante del nivel de squelch se deshabilitan automáticamente.
- Si el squelch estaba activado cuando cambió a RTTY, se desactiva automáticamente y el estado anterior se guarda para su restauración cuando salga del modo RTTY o digital.
- Los modos CW (CW, CWL) continúan teniendo el squelch deshabilitado como antes, con el estado del squelch gestionado por el propio equipo.

## Seguridad del modo RADE (v26.5.2.1)

En la v26.5.2.1, la lógica de desactivación del modo RADE (RADE) se actualizó para reflejar que "RADE" es un modo solo del lado del cliente. El equipo en sí no entiende RADE como un modo distinto — cuando RADE está activo, el equipo devuelve el modo real subyacente (DIGL o DIGU) inmediatamente.

Anteriormente, el applet verificaba `m_slice->mode() == "RADE"` antes de emitir una señal de desactivación. Debido a que el equipo informa inmediatamente el modo real después de configurar RADE, esta condición nunca podía ser verdadera. Ahora, el applet emite `radeActivated(false)` solo si el slice estaba realmente en modo RADE cuando cambió la selección del combo de modo, evitando señales de desactivación obsoletas al cambiar modos en un slice que no estaba en RADE.

Esta corrección aborda los siguientes escenarios:
- Cambiar entre modos que no son RADE en un slice que nunca estuvo en RADE.
- RADE fue activado externamente (a través del combo del widget VFO, carga de perfil al inicio, o `MainWindow::activateRADE`).
- El slice se re-vincula a un slice diferente a través de `setSlice()`.

No se requiere ninguna acción de su parte. El comportamiento de desactivación del modo RADE ahora se alinea correctamente con la naturaleza de solo lado del cliente del modo.

## Estado de silencio de audio al reconectar (v0.9.10)

En la v0.9.10, el estado del botón de silencio (🔊/🔇) NO se guarda ni restaura cuando la conexión con el equipo se pierde y se restablece. El equipo es la fuente de verdad para el estado de silencio de audio, según la Política de Ajustes Autoritativos del Equipo (#2489). Después de desconectarse y reconectarse, el botón de silencio refleja el estado de silencio real informado por el equipo, que puede ser diferente de lo que era antes de la desconexión.

## Comportamiento del botón de silencio con doble clic (v26.5.3)

A partir de la v26.5.3, el botón de silencio (🔊/🔇) tiene un manejo mejorado del doble clic:

- **Un solo clic** silencia/activa el sonido solo del slice actual. La acción se difiere por el intervalo de doble clic de la plataforma (aproximadamente 400 ms) para que un doble clic pueda anularla. Si hace clic dos veces rápidamente, el segundo clic cancela el temporizador del clic único.
- **Doble clic** silencia/activa el sonido de todos los slices propietarios a la vez.
- El icono de silencio (🔊 o 🔇) se actualiza solo cuando el equipo confirma el cambio de estado de silencio, no instantáneamente al hacer clic. Esto asegura que el estado mostrado
