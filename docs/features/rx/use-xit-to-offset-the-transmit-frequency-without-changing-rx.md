# Usar XIT para desplazar la frecuencia de transmisión sin cambiar la RX

XIT (Transmit Incremental Tuning) permite desplazar la frecuencia de transmisión un número fijo de hercios mientras la frecuencia de recepción permanece en el VFO. Esto es útil al trabajar en split, para compensar un desplazamiento de TX solicitado por la otra estación, o para ajustarse a la frecuencia de una red sin resintonizar el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles XIT solo están activos cuando hay una conexión de radio presente.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón RX del panel lateral derecho.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, desplácese hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para activar Transmit Incremental Tuning. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** que flanquean el spinbox de desplazamiento XIT para avanzar en incrementos de 10 Hz.
   - Coloque el cursor sobre el spinbox de desplazamiento XIT y gire la rueda del ratón para avanzar en incrementos de 10 Hz.
4. Para devolver el desplazamiento de TX a cero sin desactivar XIT, haga clic en XIT 0.
5. Para desactivar XIT, haga clic en XIT nuevamente para que el botón deje de estar iluminado.

## Qué hace cada control

| Control          | Función                                                                                                      | Valor predeterminado |
|------------------|--------------------------------------------------------------------------------------------------------------|----------------------|
| XIT              | Activa o desactiva Transmit Incremental Tuning.                                                              | Off                  |
| Desplazamiento XIT | Establece el desplazamiento de frecuencia TX en hercios. Se ajusta con los botones **<** / **>** o la rueda del ratón. | +0 Hz                |
| XIT 0            | Restablece el desplazamiento XIT a +0 Hz sin desactivar XIT.                                                 | —                    |

## Consejos

- RIT y XIT son independientes. Puede usar ambos simultáneamente: RIT desplaza la frecuencia de recepción, XIT desplaza la frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Si necesita que el desplazamiento de TX persista durante una sesión, configure el desplazamiento XIT antes de transmitir; permanece configurado hasta que haga clic en XIT 0 o desactive XIT.
- Para poner el desplazamiento a cero rápidamente antes de una transmisión, haga clic en XIT 0 en lugar de desactivar y volver a activar XIT.

## Solución de problemas

- **Los controles XIT están en gris** — El radio no está conectado. Use `Settings > Connect to Radio...` para establecer una conexión y vuelva a intentarlo.
- **La frecuencia de TX no se desplaza como se espera** — Confirme que el slice correcto está seleccionado usando las pestañas de slice (A..H). XIT actúa únicamente sobre el slice vinculado en ese momento.

## Colores de pestañas y distintivos de slice (v0.9.3)

A partir de la v0.9.3, los botones de pestañas de slice (A..H) y el distintivo de slice en la esquina superior izquierda del applet reciben color mediante SliceColorManager. Cada slice tiene su propio color que persiste entre sesiones. El mismo color se refleja en los widgets del VFO y las barras de medición de ese slice. Los colores no son configurables desde el propio applet RX Controls; los gestiona de forma centralizada SliceColorManager y se aplican de manera coherente en todos los widgets que hacen referencia a un slice determinado.

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

En la v0.9.5.1, la fila de pestañas de slice se reconstruye correctamente cuando cambia el número de slices disponibles, por ejemplo tras una desconexión y reconexión o cuando el radio informa un número de slices diferente.

Anteriormente, los botones de pestañas se creaban una sola vez y nunca se reemplazaban. Ahora, si el radio informa un número máximo de slices distinto al que ya se muestra, los botones existentes se eliminan primero —retirándolos del diseño y restaurando el distintivo de slice estático— antes de construir el nuevo conjunto. Esto evita que aparezcan botones de pestañas obsoletos tras la reconexión.

El manejador de clic que emite `sliceActivationRequested` se conecta una sola vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita que se acumulen manejadores de señal duplicados entre reconexiones.

No se requiere ninguna acción de su parte. La fila de pestañas se actualiza automáticamente cuando cambia la conexión del radio.

## Formato de almacenamiento de preajustes de filtro (v0.9.5.1)

En la v0.9.5.1, los preajustes de filtro guardados por la configuración `FilterPresets` pueden almacenar un valor de ancho de banda simple o un par explícito de borde inferior/borde superior. Esto coincide con el formato utilizado por el widget del VFO.

- **Formato solo de ancho** — un único entero en hercios, por ejemplo `2700`. El applet centra la banda de paso de forma simétrica alrededor de la portadora usando los bordes predeterminados del modo.
- **Formato Lo:Hi** — dos enteros separados por dos puntos, por ejemplo `300:3000`. El applet establece el borde inferior del filtro en 300 Hz y el borde superior en 3000 Hz exactamente. La etiqueta de ancho mostrada presenta la diferencia calculada (2700 Hz en este ejemplo).

Ambos formatos pueden aparecer en el mismo valor `FilterPresets` separado por comas para un modo determinado. Las entradas con formato incorrecto, con un borde superior igual o inferior al borde inferior, o que sean cero o negativos se omiten silenciosamente.

Este cambio afecta la forma en que se guardan y cargan los preajustes de filtro personalizados, pero no modifica la manera en que se interactúa con los botones de preajuste de filtro. Haga clic derecho en un botón de preajuste para guardar la banda de paso actual en ese slot; haga clic en él para aplicar el preajuste. El formato lo:hi se escribe automáticamente cuando guarda un preajuste cuyo borde inferior difiere del valor predeterminado del modo.

## Comportamiento del modo NT

El modo NT es tratado como un modo digital por el applet RX Controls. En concreto:

- NT sigue los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- La etiqueta de ancho de filtro calcula el ancho de banda de la misma manera que DIGU (usando el valor del borde superior).
- El botón SQL y el control deslizante del nivel de silenciador están desactivados cuando NT está activo, porque el audio se enruta a través de DAX y el silenciador no tiene sentido. Si el silenciador estaba activado al cambiar a NT, se desactiva automáticamente y el estado anterior se guarda para restaurarlo cuando salga del modo NT.

## Relacionados

- [Usar RIT para desplazar la frecuencia de recepción de una estación con deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de RX Controls](overview.md)
