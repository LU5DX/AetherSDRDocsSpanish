# Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Sintonización Incremental de Transmisión) le permite desplazar su frecuencia de transmisión en una cantidad fija de hercios mientras su frecuencia de recepción permanece en el VFO. Esto es útil cuando se trabaja en split, se compensa un desplazamiento de TX solicitado por la otra estación, o se iguala una frecuencia de red sin reajustar el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de XIT solo están activos cuando hay una conexión con la radio.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón RX de la barra lateral derecha.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, desplácese hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para habilitar la Sintonización Incremental de Transmisión. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento de XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** que flanquean el cuadro de desplazamiento de XIT para avanzar en incrementos de 10 Hz.
   - Pase el ratón sobre el cuadro de desplazamiento de XIT y gire la rueda del ratón para avanzar en incrementos de 10 Hz.
4. Para devolver el desplazamiento de TX a cero sin deshabilitar XIT, haga clic en XIT 0.
5. Para desactivar XIT, haga clic nuevamente en XIT para que el botón ya no esté iluminado.

## Qué hace cada control

| Control       | Qué hace                                                                                            | Por defecto |
|---------------|-----------------------------------------------------------------------------------------------------|-------------|
| XIT           | Activa o desactiva la Sintonización Incremental de Transmisión.                                     | Desactivado |
| XIT offset    | Establece el desplazamiento de frecuencia de TX en hercios. Se ajusta con los botones **<** / **>** o la rueda del ratón. | +0 Hz       |
| XIT 0         | Restablece el desplazamiento de XIT a +0 Hz sin desactivar XIT.                                    | —           |

## Consejos

- RIT y XIT son independientes. Puede ejecutar ambos simultáneamente: RIT desplaza su frecuencia de recepción, XIT desplaza su frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Si necesita que el desplazamiento de TX persista durante una sesión, ajuste el desplazamiento de XIT antes de transmitir; permanecerá establecido hasta que haga clic en XIT 0 o desactive XIT.
- Para poner a cero rápidamente el desplazamiento antes de una transmisión, haga clic en XIT 0 en lugar de desactivar y volver a activar XIT.

## Solución de problemas

- **Los controles de XIT aparecen atenuados** — La radio no está conectada. Use `Settings > Connect to Radio...` para establecer una conexión, luego intente de nuevo.
- **La frecuencia de TX no se desplaza como se espera** — Confirme que el slice correcto está seleccionado usando las pestañas de slice (A..H). XIT actúa solo sobre el slice actualmente vinculado.

---

## Applet RX Controls — Referencia completa

El applet RX Controls proporciona controles de recepción por slice para el slice actualmente vinculado. Se muestra como un panel en la barra lateral derecha cuando se hace clic en el botón RX.

### Pestañas de slice (A..H)

La fila de pestañas de slice en la parte superior del applet le permite seleccionar a qué slice está vinculado el applet. Cada slice tiene su propio color que persiste entre sesiones. El mismo color se refleja en los widgets de VFO y las tiras de medidor para ese slice.

- Haga clic en un botón de pestaña (A..H) para vincular el applet a ese slice.
- La fila de pestañas se oculta si la radio solo admite un slice.
- Al reconectar, la fila de pestañas se reconstruye correctamente cuando cambia el número de slices disponibles. El manejador de clic que emite `sliceActivationRequested` se conecta solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas.

### Insignia de slice

La insignia de slice en la esquina superior izquierda del applet muestra la letra del slice actualmente vinculado (A a H) con su color de identidad de slice. La insignia admite representación de texto enriquecido (HTML) para accesibilidad o requisitos de visualización especiales.

### 🔓 / 🔒 (Bloqueo de sintonía)

Activa o desactiva el bloqueo de sintonía en el slice. Cuando está bloqueado, el slice ignora los cambios de frecuencia.

### ANT1 (Antena de RX)

Abre un menú que lista las antenas de recepción disponibles. El menú usa la lista `rxAntennaList()` dedicada del slice cuando está disponible, recurriendo a la lista global de antenas del panadapter. Etiqueta de color azul.

### ANT1 (Antena de TX)

Abre un menú que lista las antenas capaces de TX. Los puertos de antena solo de RX (prefijo "RX") se filtran. Etiqueta de color rojo.

### 2.7K (Ancho de filtro)

Muestra el ancho de banda del filtro del slice actual. La lectura se comparte con el panel VFO y usa lógica sensible al modo para que los modos SSB y digitales muestren el ancho etiquetado correcto.

### QSK

Se ilumina en ámbar cuando la ruptura de CW (QSK) está activa. Solo lectura; controlado a través del botón Breakin del applet CW.

### TX (Insignia)

Haga clic para establecer este slice como el slice de TX.

### Combo de modo

Selecciona el modo del slice entre las opciones disponibles: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY. Si la compilación tiene soporte RADE, también está disponible RADE.

Al cambiar de modo:
- Cambiar a RTTY o modos digitales (DIGU, DIGL) desactiva automáticamente el squelch, que de lo contrario eliminaría los caracteres FSK y rompería la decodificación.
- Al salir del modo RADE, el applet emite una señal de desactivación solo si el slice estaba realmente en modo RADE, evitando señales de desactivación obsoletas al cambiar de modo en un slice que no es RADE.

### Etiqueta de frecuencia

Muestra la frecuencia actual del VFO con agrupación de puntos. Haga clic para cambiar al modo de edición.

### Edición de frecuencia

Ingrese una frecuencia en MHz y presione Enter para sintonizar y re-centrar. Admite escalado automático de kHz/Hz. La entrada se normaliza para que solo se mantenga el primer punto como separador decimal; cualquier punto adicional se elimina. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor. Consciente de XVTR: acepta hasta 450 MHz cuando el slice está en una antena XVTR.

### STEP

Cicla a través de los tamaños de paso por modo usando los botones < / > o la rueda del ratón. La lista de pasos depende del modo del slice.

### Preajustes de ancho de filtro

Haga clic para aplicar un ancho de filtro preajustado. Haga clic derecho para guardar el ancho actual como un preajuste. Los botones se ocultan para los modos FM/NFM/DFM. Los preajustes son por modo.

El método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo para ampliar o reducir la banda de paso, produciendo una geometría de borde correcta para el modo.

Los preajustes de filtro guardados pueden almacenar un valor de ancho de banda simple o un par explícito de borde bajo/borde alto (por ejemplo, `300:3000`).

### Widget de banda de paso del filtro

Arrastre los bordes lo/hi para ajustar la banda de paso del filtro.

### Modo de tono (FM)

Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM.

### Valor de tono CTCSS

Selecciona la frecuencia del tono CTCSS enviada con la transmisión. Habilitado solo cuando el modo de tono es CTCSS TX.

### Offset (FM)

Establece la frecuencia de desplazamiento del repetidor de FM en MHz.

### −, Símplex, + (Dirección del offset)

Establece la dirección del desplazamiento del repetidor hacia abajo, símplex o hacia arriba.

### REV

Invierte el signo del desplazamiento de TX para trabajar un par de repetidores invertido.

### 🔊 / 🔇 (Silencio)

Un solo clic silencia/activa el sonido de este slice. Un doble clic silencia/activa el sonido de todos los slices propios. La acción se difiere por el intervalo de doble clic de la plataforma para que un doble clic pueda anular un solo clic.

El estado de silencio NO se guarda ni se restaura al reconectar — la radio es la fuente de verdad para el estado de silencio de audio. El ícono de silencio se actualiza solo cuando la radio confirma el cambio de estado de silencio.

### Ganancia de AF

Ajusta la ganancia de salida de audio del slice (0-100).

### Panorámico L / R

Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Un doble clic restablece a 50 (centro). El relleno del deslizador se ancla desde el centro hacia afuera para que el operador pueda ver la posición neutral de un vistazo. Se dibuja un pequeño punto de marca central en la ranura.

### SQL

Activa el squelch al nivel actual del deslizador. Deshabilitado (y desactivado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch eliminaría los caracteres FSK.

### Nivel de squelch

Ajusta el umbral de squelch (0-100). Solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales.

El nivel de umbral de squelch manual se guarda y restaura entre sesiones bajo `LastManualSquelchLevel`. Esto preserva su umbral de squelch preferido cuando sale del modo automático o reinicia la aplicación.

### Modo AGC

Establece el modo AGC del slice (Off, Slow, Med, Fast). Oculto en modos de la familia FM.

### Umbral AGC

Establece el umbral AGC (o nivel de AGC desactivado cuando el modo AGC está en Off). La información sobre herramientas refleja qué valor se está ajustando.

### RIT

Activa o desactiva la Sintonización Incremental de Recepción.

### RIT 0

Pone a cero el desplazamiento de RIT.

### RIT offset

Ajusta el desplazamiento de RIT en pasos de 10 Hz usando los botones < / > o la rueda del ratón.

### XIT

Activa o desactiva la Sintonización Incremental de Transmisión.

### XIT 0

Pone a cero el desplazamiento de XIT.

### XIT offset

Ajusta el desplazamiento de XIT en pasos de 10 Hz usando los botones < / > o la rueda del ratón.

---

## Comportamiento del modo NT

El modo NT se trata como un modo digital por el applet RX Controls. Específicamente:

- NT sigue los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- La etiqueta de ancho de filtro calcula el ancho de banda de la misma manera que DIGU (usando el valor del borde alto).
- El botón SQL y el deslizador de nivel de squelch están deshabilitados cuando NT está activo, porque el audio se enruta a través de DAX y el squelch no es significativo. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y el estado anterior se guarda para su restauración cuando salga del modo NT.

## Comportamiento del squelch en modos RTTY y digitales

A partir de la versión v26.5.1, los controles de squelch (botón SQL y deslizador de nivel de squelch) también están deshabilitados en modo RTTY, además de los modos digitales existentes (DIGU, DIGL) y el modo NT. Este cambio asegura que el squelch no elimine los caracteres FSK, lo que de otro modo rompería la decodificación.

Cuando cambia al modo RTTY:
- El botón SQL y el deslizador de nivel de squelch se deshabilitan automáticamente.
- Si el squelch estaba activado cuando cambió a RTTY, se desactiva automáticamente y el estado anterior se guarda para su restauración cuando salga del modo RTTY o digital.
- Los modos CW (CW, CWL) continúan teniendo el squelch deshabilitado como antes, con el estado del squelch gestionado por la propia radio.

## Seguridad del modo RADE

En la versión v26.5.2.1, la lógica de desactivación del modo RADE se actualizó para reflejar que "RADE" es un modo solo del lado del cliente. La radio en sí misma no entiende RADE como un modo distinto — cuando RADE está activo, la radio devuelve inmediatamente el modo real subyacente (DIGL o DIGU).

El applet emite `radeActivated(false)` solo si el slice estaba realmente en modo RADE cuando cambió la selección del combo de modo, evitando señales de desactivación obsoletas al cambiar de modo en un slice que no es RADE.

Esta corrección aborda los siguientes escenarios:
- Cambiar entre modos que no son RADE en un slice que nunca estuvo en RADE.
- RADE se activó externamente (a través del combo del widget VFO, carga de perfil al inicio, o `MainWindow::activateRADE`).
- El slice se re-vincula a un slice diferente a través de `setSlice()`.

No se requiere ninguna acción de su parte. El comportamiento de desactivación del modo RADE ahora se alinea correctamente con la naturaleza de solo lado del cliente del modo.

## Estado de silencio de audio al reconectar

El estado del botón de silencio (🔊 / 🔇) NO se guarda ni se restaura cuando la conexión con la radio se pierde y se restablece. La radio es la fuente de verdad para el estado de silencio de audio. Después de desconectarse y reconectarse, el botón de silencio refleja el estado de silencio real informado por la radio, que puede ser diferente de lo que era antes de la desconexión.

## Comportamiento de doble clic del botón de silencio

El botón de silencio (🔊 / 🔇) tiene un manejo mejorado de doble clic:

- **Un solo clic** silencia/activa el sonido solo del slice actual. La acción se difiere por el intervalo de doble clic de la plataforma (aproximadamente 400 ms) para que un doble clic pueda anularlo. Si hace clic dos veces rápidamente, el segundo clic cancela el temporizador de un solo clic.
- **Doble clic** silencia/activa el sonido de todos los slices propios a la vez.
- El ícono de silencio (🔊 o 🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio, no instantáneamente al hacer clic. Esto asegura que el estado mostrado siempre coincida con el estado de silencio de audio real de la radio.

No se requiere ninguna acción de su parte. El botón de silencio ahora maneja correctamente tanto los clics simples como los dobles.

## Comportamiento visual del deslizador de panorámico

El relleno del deslizador de panorámico L/R se ancla desde el centro hacia afuera, por lo que el cero significativo es el punto medio. Se dibuja un pequeño punto de marca central en la ranura para que el operador pueda ver la posición neutral de un vistazo.

## Tematización de colores

En la versión v26.6.
