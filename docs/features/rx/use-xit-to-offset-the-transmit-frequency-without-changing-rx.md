# Uso de XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Sintonización Incremental de Transmisión) le permite desplazar su frecuencia de transmisión una cantidad fija de hercios mientras su frecuencia de recepción permanece en el VFO. Esto es útil cuando se trabaja en split, se compensa un desplazamiento de TX solicitado por la otra estación, o se iguala una frecuencia de red sin reajustar el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Los controles XIT solo están activos cuando hay una conexión con el equipo.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón RX de la barra lateral derecha.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet.

## Pasos

1. En el applet RX Controls, desplace hacia abajo hasta la sección RIT/XIT.
2. Haga clic en XIT para activar la Sintonización Incremental de Transmisión. El botón se ilumina cuando está activo.
3. Ajuste el desplazamiento XIT usando uno de estos métodos:
   - Haga clic en los botones **<** o **>** que flanquean el cuadro de desplazamiento XIT para avanzar en incrementos de 10 Hz.
   - Pase el cursor sobre el cuadro de desplazamiento XIT y gire la rueda del ratón para avanzar en incrementos de 10 Hz.
4. Para devolver el desplazamiento de TX a cero sin desactivar XIT, haga clic en XIT 0.
5. Para desactivar XIT, haga clic en XIT nuevamente para que el botón deje de estar iluminado.

## Qué hace cada control

| Control       | Qué hace                                                                                         | Valor por defecto |
|---------------|--------------------------------------------------------------------------------------------------|-------------------|
| XIT           | Activa o desactiva la Sintonización Incremental de Transmisión.                                   | Off               |
| Desplazamiento XIT | Establece el desplazamiento de frecuencia de TX en hercios. Se ajusta con los botones **<** / **>** o la rueda del ratón. | +0 Hz             |
| XIT 0         | Restablece el desplazamiento XIT a +0 Hz sin desactivar XIT.                                     | —                 |

## Consejos

- RIT y XIT son independientes. Puede ejecutar ambos simultáneamente: RIT desplaza su frecuencia de recepción, XIT desplaza su frecuencia de transmisión, y la lectura del VFO permanece sin cambios.
- Si necesita que el desplazamiento de TX persista durante una sesión, ajuste el desplazamiento XIT antes de transmitir; permanecerá establecido hasta que haga clic en XIT 0 o desactive XIT.
- Para poner a cero el desplazamiento rápidamente antes de una transmisión, haga clic en XIT 0 en lugar de desactivar y volver a activar XIT.

## Solución de problemas

- **Los controles XIT están atenuados** — El equipo no está conectado. Use `Settings > Connect to Radio...` para establecer una conexión y vuelva a intentarlo.
- **La frecuencia de TX no se desplaza como se esperaba** — Confirme que el slice correcto está seleccionado usando las pestañas de slice (A..H). XIT solo actúa sobre el slice actualmente vinculado.

---

## Applet RX Controls — Referencia completa

El applet RX Controls proporciona controles de recepción por slice para el slice actualmente vinculado. Se muestra como un panel en la barra lateral derecha al hacer clic en el botón RX.

### Pestañas de slice (A..H)

La fila de pestañas de slice en la parte superior del applet le permite seleccionar a qué slice está vinculado el applet. Cada slice tiene su propio color que persiste entre sesiones. El mismo color se refleja en los widgets VFO y las tiras de medidor para ese slice.

- Haga clic en un botón de pestaña (A..H) para vincular el applet a ese slice.
- La fila de pestañas se oculta si el equipo solo admite un slice.
- Al reconectar, la fila de pestañas se reconstruye correctamente cuando cambia el número de slices disponibles. El controlador de clic que emite `sliceActivationRequested` se conecta solo una vez por instancia del applet, independientemente de cuántas veces se reconstruya la fila de pestañas.
- Las conexiones de clic de los botones de slice están protegidas contra manejadores de señal duplicados entre reconexiones. `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar.

### Insignia de slice

La insignia de slice en la parte superior izquierda del applet muestra la letra del slice actualmente vinculado (A a H) con su color de identidad de slice. La insignia admite representación de texto enriquecido (HTML) para accesibilidad o requisitos de visualización especiales.

### 🔓 / 🔒 (Bloqueo de sintonía)

Activa o desactiva el bloqueo de sintonía en el slice. Cuando está bloqueado, el slice ignora los cambios de frecuencia.

### ANT1 (Antena RX)

Abre un menú que lista las antenas de recepción disponibles. El menú usa la `rxAntennaList()` dedicada del slice cuando está disponible, recurriendo a la lista de antenas del panadapter global. Etiqueta de color azul.

### ANT1 (Antena TX)

Abre un menú que lista las antenas con capacidad TX. Los puertos de solo RX (prefijo "RX") se filtran. Etiqueta de color rojo.

### 2.7K (Ancho de filtro)

Muestra el ancho de banda del filtro del slice actual. La lectura se comparte con el panel VFO y usa lógica consciente del modo, de modo que los modos SSB y digitales muestren el ancho etiquetado correcto. El método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo para ampliar o reducir el paso de banda, produciendo una geometría de bordes correcta según el modo.

### QSK

Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW.

### TX (Insignia)

Haga clic para establecer este slice como el slice de TX.

### Combo Modo

Selecciona el modo del slice entre las opciones disponibles: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY. Si la compilación tiene soporte RADE, RADE también está disponible.

Al cambiar de modo:
- Al cambiar a RTTY o modos digitales (DIGU, DIGL), se desactiva automáticamente el squelch, que de lo contrario eliminaría los caracteres FSK e interrumpiría la decodificación.
- Al salir del modo RADE, el applet emite una señal de desactivación solo si el slice estaba realmente en modo RADE, evitando señales de desactivación obsoletas al cambiar de modo en un slice que no era RADE.
- Seleccionar cualquier modo de radio real elimina automáticamente la superposición del demodulador de software WFM si se estaba ejecutando en ese slice (consulte la sección del botón WFM).

### Botón WFM

Un botón de alternancia etiquetado "WFM" aparece inmediatamente después del cuadro combinado de modo. Activa o desactiva el demodulador FM por software, que utiliza audio DAX IQ enrutado a través del cable Hi-Fi. No es un modo de radio, sino una superposición del lado del cliente.

- Haga clic para activar o desactivar el demodulador WFM.
- Cuando está activo, el botón se resalta con un fondo verde.
- Tooltip: "Demodulador FM por software vía DAX IQ → Cable Hi-Fi"
- Seleccionar cualquier modo del cuadro combinado de modo desactiva automáticamente WFM en ese slice.
- El estado de WFM se sincroniza entre reconexiones: si la conexión con el equipo se pierde y se restablece, el botón refleja el estado de WFM previamente activo.

### Etiqueta de frecuencia

Muestra la frecuencia actual del VFO con agrupación de puntos. Haga clic para cambiar al modo de edición.

### Edición de frecuencia

Ingrese una frecuencia en MHz y presione Enter para sintonizar y re-centrar. Admite autoescalado de kHz/Hz. La entrada se normaliza para que solo el primer punto se mantenga como separador decimal; cualquier punto adicional se elimina. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor. Consciente de XVTR: acepta hasta 450 MHz cuando el slice está en una antena XVTR. El campo de texto ahora es un widget `FreqLineEdit` con una etiqueta de sugerencia "MHz" en lugar de texto de marcador de posición.

### STEP

Recorre los tamaños de paso por modo usando los botones < / > o la rueda del ratón. La lista de pasos depende del modo del slice. La señal `stepSizeChangedByUser` se emite junto con `stepSizeChanged` para distinguir los cambios de paso iniciados por el usuario de los programáticos.

### Preajustes de ancho de filtro

Haga clic para aplicar un ancho de filtro predefinido. Haga clic derecho para guardar el ancho actual como preajuste. Los botones se ocultan para los modos FM/NFM/DFM. Los preajustes son por modo.

El método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo para ampliar o reducir el paso de banda, produciendo una geometría de bordes correcta según el modo.

Los preajustes de filtro guardados pueden almacenar un valor de ancho de banda simple o un par explícito de borde inferior/borde superior (por ejemplo, `300:3000`).

### Widget de paso de banda del filtro

Arrastre los bordes lo/hi para ajustar el paso de banda del filtro.

### Modo de tono (FM)

Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM.

### Valor de tono CTCSS

Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Habilitado solo cuando el modo de tono es CTCSS TX.

### Desplazamiento (FM)

Establece la frecuencia de desplazamiento del repetidor FM en MHz.

### −, Símplex, + (Dirección del desplazamiento)

Establece la dirección del desplazamiento del repetidor hacia abajo, símplex o hacia arriba.

### REV

Invierte el signo del desplazamiento de TX para trabajar un par de repetidor inverso.

### 🔊 / 🔇 (Silencio)

Un solo clic silencia/activa el sonido de este slice. Doble clic silencia/activa el sonido de todos los slices propios. La acción se retrasa según el intervalo de doble clic de la plataforma para que un doble clic pueda anular un solo clic.

El estado de silencio NO se guarda ni restaura al reconectar — el equipo es la fuente de verdad para el estado de silencio de audio. El icono de silencio se actualiza solo cuando el equipo confirma el cambio de estado de silencio.

### Ganancia AF

Ajusta la ganancia de salida de audio del slice (0-100).

### Panorámico L / R

Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Doble clic restablece a 50 (centro). El relleno del deslizador se ancla desde el centro hacia afuera para que el operador pueda ver la posición neutral de un vistazo. Se dibuja un pequeño punto de marca central en la ranura.

### SQL

Activa el squelch al nivel actual del deslizador. Desactivado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch eliminaría los caracteres FSK.

### Nivel de squelch

Ajusta el umbral de squelch (0-100). Solo tiene efecto cuando SQL está activado. Desactivado en modos RTTY y digitales.

El nivel de umbral de squelch manual se guarda y restaura entre sesiones bajo `LastManualSquelchLevel`. Esto preserva su umbral de squelch preferido cuando sale del modo automático o reinicia la aplicación.

### Modo AGC

Establece el modo AGC del slice (Off, Slow, Med, Fast). Oculto en modos de la familia FM.

### Umbral AGC

Establece el umbral AGC (o nivel de AGC off cuando el modo AGC es Off). El tooltip refleja qué valor se está ajustando. Además, el tooltip ahora anuncia la función de calibración con clic derecho: "Haga clic derecho para calibrar contra el piso de ruido."

Haga clic derecho en el deslizador de umbral AGC para abrir un menú contextual con la opción "Calibrar AGC-T contra el piso de ruido…". Al seleccionarlo, se emite una señal `calibrateAgcTRequested` para el slice actual, que abre el panel de calibración de ruido AGC-T. Esta función le ayuda a establecer el umbral AGC basado en el piso de ruido real en lugar de un valor arbitrario.

### Menú contextual de calibración AGC-T

El deslizador de umbral AGC tiene un menú contextual de clic derecho que proporciona acceso al panel de calibración de ruido:

1. Haga clic derecho en el deslizador de umbral AGC.
2. Seleccione "Calibrar AGC-T contra el piso de ruido…" en el menú contextual.
3. Se abre el panel de calibración, permitiéndole establecer el umbral AGC basado en el piso de ruido medido.

Esta función le ayuda a establecer el umbral AGC con mayor precisión para su entorno operativo. El menú contextual solo está disponible cuando un slice está vinculado al applet.

### RIT

Activa o desactiva la Sintonización Incremental de Recepción.

### RIT 0

Pone a cero el desplazamiento RIT.

### Desplazamiento RIT

Ajusta el desplazamiento RIT en pasos de 10 Hz usando los botones < / > o la rueda del ratón.

### XIT

Activa o desactiva la Sintonización Incremental de Transmisión.

### XIT 0

Pone a cero el desplazamiento XIT.

### Desplazamiento XIT

Ajusta el desplazamiento XIT en pasos de 10 Hz usando los botones < / > o la rueda del ratón.

---

## Comportamiento del modo NT

El modo NT se trata como un modo digital por el applet RX Controls. Específicamente:

- NT sigue los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- La etiqueta de ancho de filtro calcula el ancho de banda de la misma manera que DIGU (usando el valor del borde superior).
- El botón SQL y el deslizador de nivel de squelch están desactivados cuando NT está activo, porque el audio se enruta a través de DAX y el squelch no tiene sentido. Si el squelch estaba activado cuando cambió a NT, se apaga automáticamente y el estado anterior se guarda para restaurarlo al salir del modo NT.

## Comportamiento del squelch en modos RTTY y digitales

A partir de v26.5.1, los controles de squelch (botón SQL y deslizador de nivel de squelch) también están desactivados en modo RTTY, además de los modos digitales existentes (DIGU, DIGL) y el modo NT. Este cambio garantiza que el squelch no elimine los caracteres FSK, lo que de otro modo interrumpiría la decodificación.

Cuando cambie al modo RTTY:
- El botón SQL y el deslizador de nivel de squelch se desactivan automáticamente.
- Si el squelch estaba activado cuando cambió a RTTY, se apaga automáticamente y el estado anterior se guarda para restaurarlo al salir del modo RTTY o digital.
- Los modos CW (CW, CWL) continúan teniendo el squelch desactivado como antes, con el estado del squelch gestionado por el propio equipo.

## Seguridad del modo RADE

En v26.5.2.1, la lógica de desactivación del modo RADE se actualizó para reflejar que "RADE"
