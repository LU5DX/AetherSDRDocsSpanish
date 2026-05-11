# Uso de XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Sintonización incremental de transmisión) permite desplazar la frecuencia de transmisión en una cantidad fija de hercios mientras la frecuencia de recepción permanece en el VFO. Esto es útil cuando se trabaja en split, se compensa un desplazamiento de TX solicitado por la otra estación, o se iguala la frecuencia de una red sin necesidad de re-sintonizar el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles XIT solo están activos cuando hay una conexión con el radio.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón RX de la barra lateral derecha.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, desplácese hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para habilitar la sintonización incremental de transmisión. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** que flanquean el cuadro de desplazamiento XIT para ajustar en incrementos de 10 Hz.
   - Pase el cursor sobre el cuadro de desplazamiento XIT y gire la rueda del ratón para ajustar en incrementos de 10 Hz.
4. Para devolver el desplazamiento de TX a cero sin deshabilitar XIT, haga clic en XIT 0.
5. Para desactivar XIT, haga clic en XIT nuevamente para que el botón deje de estar iluminado.

## Qué hace cada control

| Control       | Qué hace                                                                                         | Valor predeterminado |
|---------------|--------------------------------------------------------------------------------------------------|-----------------------|
| XIT           | Activa o desactiva la sintonización incremental de transmisión.                                  | Desactivado           |
| Desplazamiento XIT | Establece el desplazamiento de frecuencia de TX en hercios. Se ajusta con los botones **<** / **>** o la rueda del ratón. | +0 Hz                 |
| XIT 0         | Restablece el desplazamiento XIT a +0 Hz sin desactivar XIT.                                     | —                     |

## Consejos

- RIT y XIT son independientes. Puede usar ambos simultáneamente: RIT desplaza su frecuencia de recepción, XIT desplaza su frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Si necesita que el desplazamiento de TX persista durante una sesión, ajuste el desplazamiento XIT antes de transmitir; permanecerá configurado hasta que haga clic en XIT 0 o desactive XIT.
- Para poner a cero el desplazamiento rápidamente antes de una transmisión, haga clic en XIT 0 en lugar de desactivar y volver a activar XIT.

## Solución de problemas

- **Los controles XIT aparecen atenuados** — El radio no está conectado. Use `Settings > Connect to Radio...` para establecer una conexión y luego intente nuevamente.
- **La frecuencia de TX no se desplaza como se espera** — Confirme que el slice correcto esté seleccionado usando las pestañas de slice (A..H). XIT actúa solo sobre el slice actualmente vinculado.

## Colores de pestañas y distintivos de slice (v0.9.3)

A partir de v0.9.3, los botones de pestaña de slice (A..H) y el distintivo de slice en la esquina superior izquierda del applet se colorean según el SliceColorManager. Cada slice tiene su propio color que persiste entre sesiones. El mismo color se refleja en los widgets VFO y las barras de medidor para ese slice. Los colores no se pueden configurar desde el propio applet RX Controls; son gestionados centralmente por SliceColorManager y se aplican de manera consistente en todos los widgets que hacen referencia a un slice dado.

## Comportamiento de pestañas de slice al reconectar (v0.9.5.1)

En v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cuando cambia el número de slices disponibles, por ejemplo, después de una desconexión y reconexión, o después de que el radio informe un número diferente de slices.

Anteriormente, los botones de pestaña se creaban solo una vez y nunca se reemplazaban. Ahora, si el radio informa un número máximo de slices diferente del que ya se muestra, los botones existentes se eliminan primero —quitándolos del diseño y restaurando el distintivo de slice estático— antes de construir el nuevo conjunto. Esto evita que aparezcan botones de pestaña obsoletos después de la reconexión.

El manejador de clic que emite `sliceActivationRequested` se conecta solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de manejadores de señal duplicados a través de las reconexiones.

No se requiere ninguna acción de su parte. La fila de pestañas se actualiza automáticamente cuando cambia la conexión del radio.

## Formato de almacenamiento de preajustes de filtro (v0.9.5.1)

En v0.9.5.1, los preajustes de filtro guardados por la configuración `FilterPresets` pueden almacenar un valor de ancho de banda simple o un par explícito de borde inferior/borde superior. Esto coincide con el formato utilizado por el widget VFO.

- **Formato solo de ancho** — un solo entero en hercios, por ejemplo `2700`. El applet centra la banda de paso simétricamente alrededor de la portadora usando los bordes predeterminados del modo.
- **Formato Lo:Hi** — dos enteros separados por dos puntos, por ejemplo `300:3000`. El applet establece el borde inferior del filtro exactamente a 300 Hz y el borde superior a 3000 Hz. La etiqueta de ancho mostrada muestra la diferencia calculada (2700 Hz en este ejemplo).

Ambos formatos pueden aparecer en el mismo valor `FilterPresets` separado por comas para un modo dado. Las entradas que están mal formadas, tienen un borde superior igual o inferior al borde inferior, o son cero o negativas se omiten silenciosamente.

Este cambio afecta cómo se guardan y cargan los preajustes de filtro personalizados, pero no cambia la forma de interactuar con los botones de preajuste de filtro. Haga clic derecho en un botón de preajuste para guardar la banda de paso actual en esa ranura; haga clic en él para aplicar el preajuste. El formato lo:hi se escribe automáticamente cuando guarda un preajuste cuyo borde inferior difiere del valor predeterminado del modo.

## Comportamiento del paso de ancho de filtro (v0.9.8)

En v0.9.8, el método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo para ensanchar o estrechar la banda de paso. Esto garantiza que los atajos de teclado u otros controles que recorren los anchos de filtro produzcan una geometría de bordes correcta para el modo.

Cuando usa una acción de ensanchar/estrechar (como desde los botones Widen/Narrow en el panel VFO), el applet busca en la lista de preajustes de filtro por modo el preajuste más cercano al ancho de filtro actual. Luego aplica el siguiente preajuste más ancho o más estrecho de esa lista. Si el ancho actual coincide exactamente con un preajuste, el siguiente preajuste en la dirección elegida se aplica directamente.

Este comportamiento se aplica a todos los modos: LSB, CWL, DIGL, RTTY, AM, CW y USB. Los modos de la familia FM (FM, NFM, DFM) no tienen preajustes de filtro e ignoran la acción de paso.

No se necesita configuración. El comportamiento de paso utiliza la misma configuración `FilterPresets` que puede personalizar con el clic derecho para guardar.

## Comportamiento del modo NT

El modo NT se trata como un modo digital por el applet RX Controls. Específicamente:

- NT sigue los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- La etiqueta de ancho de filtro calcula el ancho de banda de la misma manera que DIGU (usando el valor del borde superior).
- El botón SQL y el control deslizante de nivel de squelch están deshabilitados cuando NT está activo, porque el audio se enruta a través de DAX y el squelch no es significativo. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y el estado anterior se guarda para restaurarlo cuando salga del modo NT.

## Comportamiento del squelch en modos RTTY y digitales (v26.5.1)

A partir de v26.5.1, los controles de squelch (botón SQL y control deslizante de nivel de squelch) también están deshabilitados en modo RTTY, además de los modos digitales existentes (DIGU, DIGL) y el modo NT. Este cambio asegura que el squelch no recorte los caracteres FSK, lo que de otro modo interrumpiría la decodificación.

Cuando cambia al modo RTTY:
- El botón SQL y el control deslizante de nivel de squelch se deshabilitan automáticamente.
- Si el squelch estaba activado cuando cambió a RTTY, se desactiva automáticamente y el estado anterior se guarda para restaurarlo cuando salga del modo RTTY o digital.
- Los modos CW (CW, CWL) continúan teniendo el squelch deshabilitado como antes, con el estado del squelch gestionado por el propio radio.

## Seguridad del modo RADE (v26.5.1)

En v26.5.1, se mejoró la lógica de activación y desactivación del modo RADE (RADE) para evitar señales de desactivación espurias. Cuando selecciona el modo RADE:

1. El applet activa RADE en el slice correcto y llama a `m_slice->setMode(mode)` inmediatamente.
2. Al cambiar de RADE a otro modo, el applet solo emite una señal de desactivación si el slice estaba realmente en modo RADE antes del cambio. Esto evita enviar una desactivación falsa cuando:
   - El usuario alterna entre modos no RADE en un slice que nunca estuvo en RADE.
   - RADE se activó externamente (a través del combo del widget VFO, carga de perfil al inicio, o `MainWindow::activateRADE`).
   - El slice se reasigna a un slice diferente mediante `setSlice()`.

El applet lee el modo del slice *antes* de llamar a `m_slice->setMode(mode)`, por lo que ve correctamente el modo anterior al cambio independientemente de cómo se activó RADE.

No se requiere ninguna acción de su parte. La activación y desactivación del modo RADE ahora se comporta correctamente en todos los escenarios.

## Relacionado

- [Uso de RIT para desplazar la frecuencia de recepción para una estación a la deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Sintonice el radio a una frecuencia (escriba MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambie entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de RX Controls](overview.md)
