# Seleccionar un ancho de filtro predefinido para el modo actual

Utilice los botones de anchos de filtro predefinidos en el applet de Controles de RX para aplicar rápidamente un ancho de banda estándar para el modo activo. Las predefiniciones se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles de RX requiere una conexión activa a la radio.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.
- Configure primero el modo del slice. Los valores predefinidos varían según el modo y no se muestran predefiniciones para los modos FM, NFM o DFM.

## Pasos

1. Abra el applet de Controles de RX. Si no está visible, haga clic en el botón de la bandeja de RX en la barra lateral derecha.
2. Si la fila de pestañas de slice es visible, haga clic en la pestaña (A a H) correspondiente al slice que desea ajustar.
3. Confirme que el modo mostrado en el cuadro combinado Mode sea correcto. Las predefiniciones de filtro cambian cuando el modo cambia.
4. Haga clic en cualquiera de los botones de ancho de filtro predefinidos para aplicar ese ancho de banda inmediatamente. El ancho de filtro actual mostrado en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar la predefinición aplicada.
5. Para guardar el ancho de banda de paso actual del filtro como una predefinición, haga clic con el botón derecho en cualquier botón de ancho de filtro predefinido y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control                     | Comportamiento                                                                                                                                                                                         | Predefiniciones predeterminadas por modo                                                                                                                                                                                                                                                                                                                                    |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Anchos de filtro predefinidos | Haga clic para aplicar un ancho de filtro predefinido; haga clic con el botón derecho para guardar el ancho actual como predefinición. Los botones se ocultan para los modos FM/NFM/DFM; son por modo. | La indicación de ancho (compartida con VfoWidget mediante RxApplet::formatFilterWidth) utiliza lógica consciente del modo, de modo que los modos SSB/digitales muestran el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de predefiniciones por modo para el ensanche/reducción correctos según el modo (#2208). |
| Etiqueta de ancho de filtro | Indicador de solo lectura que muestra el ancho de banda del filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica una predefinición o cuando se arrastran los bordes de la banda de paso. | —                                                                                                                                                                                                                                                                                                                                                                           |
| Widget de banda de paso del filtro | Arrastre el borde inferior o superior para establecer una banda de paso personalizada. Use las predefiniciones para anchos estándar.                                                        | —                                                                                                                                                                                                                                                                                                                                                                           |
| Modo                        | Anchos predefinidos (Hz)                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                             |
| ---                         | ---                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                             |
| USB, LSB                    | 1800, 2100, 2400, 2700, 2900, 3300                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                             |
| AM, SAM                     | 5600, 6000, 8000, 10000, 12000, 14000                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                             |
| CW                          | 50, 100, 250, 400                                                                                                                                                                                      |                                                                                                                                                                                                                                                                                                                                                                             |
| DIGU, DIGL, NT              | 100, 300, 600, 1000, 1500, 2000                                                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                             |
| RTTY                        | 250, 300, 350, 400, 500, 1000                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                             |
| FM, NFM, DFM                | Sin predefiniciones (botones ocultos)                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                             |
| RADE                        | Sin predefiniciones (solo del lado del cliente, la radio devuelve el modo real)                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                             |

## Reducir y ensanchar la banda de paso del filtro mediante pasos

El método `stepFilterWidth(direction)` permite recorrer la lista de predefiniciones por modo desde cualquier acceso directo de aplicación o combinación de teclas. Use `+1` para ensanchar la banda de paso al siguiente valor predefinido mayor, o `-1` para reducirla al siguiente valor predefinido menor. Dado que `stepFilterWidth` se enruta a través de `applyFilterPreset`, todos los modos, incluidos LSB, CWL, DIGL, RTTY, AM y CW, utilizan la geometría de bordes correcta para ese modo en lugar de una suposición simétrica.

Internamente, el método encuentra la predefinición cuyo ancho está más cerca de la banda de paso actual del slice, luego se mueve a la entrada siguiente o anterior en la lista (limitada a los límites válidos). Si el ancho actual ya es igual a la predefinición más cercana y el paso se saldría de la lista, la operación se ignora.

## Formato de almacenamiento de predefiniciones de filtro (v0.9.5.1)

A partir de la v0.9.5.1, las predefiniciones de filtro almacenadas en `FilterPresets` pueden representar un ancho de banda simple o una banda de paso completamente especificada con desplazamientos de borde inferior y superior explícitos. Ambos formatos son aceptados al cargar predefiniciones guardadas.

- **Formato solo de ancho** — Un único entero que representa el ancho de banda en Hz (por ejemplo, `2700`). Al aplicarlo, la radio posiciona la banda de paso simétricamente alrededor de la portadora según las reglas de desplazamiento predeterminadas del modo.
- **Formato Lo:Hi** — Dos enteros separados por dos puntos que representan los desplazamientos de los bordes inferior y superior de la banda de paso en Hz (por ejemplo, `300:3000`). El ancho se deriva como `hi − lo`. El valor `hi` debe ser mayor que el valor `lo`; de lo contrario, la entrada se ignora.

Las entradas en cualquiera de los formatos pueden aparecer en la misma lista de predefiniciones guardada para un modo determinado. La lista está separada por comas. Se cargan hasta seis entradas para el applet de Controles de RX (que coinciden con el número máximo de botones predefinidos mostrados).

Si una lista de predefiniciones guardada se modifica externamente o una reconexión hace que la radio informe un número diferente de slices, los botones de predefiniciones se reconstruyen automáticamente para reflejar los valores almacenados.

## Visibilidad de los botones de reducción de ruido y filtro DSP

La siguiente tabla resume qué botones de reducción de ruido y filtro DSP son visibles según la serie de radio y el modo.

| Botón | Serie 6000 | Serie 8000 (DSP extendido) | Oculto cuando |
|-------|------------|----------------------------|---------------|
| NR    | Sí         | Sí                         | Modo FM       |
| NR2   | Sí         | Sí                         | Modo FM       |
| NB    | Sí         | Sí                         | Modo FM       |
| NRL   | Sí         | Sí                         | Modo FM       |
| NRS   | No         | Sí                         | Modo FM       |
| RNN   | No         | Sí                         | Modo CW o FM  |
| NRF   | No         | Sí                         | Modo FM       |

Antes de V0.9.4, el botón NRL solo se mostraba en radios de la serie 8000 (DSP extendido). A partir de V0.9.4, NRL también está disponible en radios de la serie 6000. NRS, RNN y NRF siguen siendo exclusivos de la serie 8000.

## Colores de pestaña de slice y distintivo (v0.9.3)

A partir de v0.9.3, los botones de pestaña de slice y el distintivo de slice utilizan colores por slice gestionados por el singleton `SliceColorManager` en lugar de una tabla de colores fija. El borde activo, el resaltado de fondo en los botones de pestaña y el fondo del distintivo reflejan el color asignado a ese slice. Los colores persisten entre sesiones y también se reflejan en los widgets de VFO y las tiras de medidor. No se requiere ninguna acción; los colores se actualizan automáticamente cuando se conecta un slice.

## Comportamiento de la pestaña de slice al reconectar (v0.9.5.1)

Cuando AetherSDR se desconecta de la radio y se vuelve a conectar, o cuando cambia el número de slices disponibles, la fila de pestañas de slice se reconstruye correctamente. Específicamente:

- Si el número de slices informados por la radio difiere del número de botones de pestaña mostrados actualmente, `clearSliceButtons()` elimina todos los botones de pestaña existentes y la fila se reconstruye desde cero.
- Mientras la fila de pestañas está eliminada, el distintivo de slice estático se restaura para que el applet continúe mostrando qué slice está vinculado.
- Las conexiones de señal de los botones de pestaña al controlador de activación del slice se establecen solo una vez por instancia del applet, lo que evita la acumulación de controladores duplicados a través de reconexiones.

No se requiere ninguna acción del usuario. Si el recuento de slices cambia (por ejemplo, después de un ciclo de desconexión y reconexión), la fila de pestañas se actualiza automáticamente.

## Mejoras en la selección de antena RX (v26.5.2.1)

En v26.5.2.1, el menú de selección de antena RX se mejoró para mostrar la lista de antenas RX dedicadas del slice cuando está disponible, en lugar de la lista de antenas global del estado del panadapter. Si el slice tiene una lista de antenas RX, el menú muestra esas entradas; de lo contrario, recurre a la lista de antenas global. Cada elemento del menú ahora:

- Utiliza el identificador de antena como su valor de datos subyacente (`act->setData(ant)`)
- Muestra una etiqueta legible para humanos mediante `antennaMenuLabel()`
- Muestra el identificador de antena sin procesar en la información sobre herramientas y la información de estado

El menú de selección de antena TX también se actualizó para usar el método `txAntennaOptions()` y `antennaMenuLabel()`. Ambos menús ahora usan `sel->data().toString()` al configurar la antena, por lo que el texto de la etiqueta es secundario al identificador de antena.

No se necesita configuración. Los menús se actualizan automáticamente al reconectarse a la radio.

## Cambio en la lógica de desactivación del modo RADE (v26.5.2.1)

En v26.5.2.1, se corrigió el comportamiento de la señal de desactivación del modo RADE. Anteriormente, al salir del modo RADE a través del cuadro combinado Mode, el applet verificaba `m_slice->mode() == "RADE"` antes de emitir `radeActivated(false)`. Esta verificación ya no funciona correctamente porque RADE es un modo solo del lado del cliente: la radio devuelve inmediatamente el modo real (DIGL/DIGU), por lo que `mode()` nunca devuelve "RADE" en el momento de la verificación. La verificación obsoleta se ha eliminado.

La opción RADE permanece disponible en el cuadro combinado Mode solo cuando `HAVE_RADE` está definido en el momento de la compilación.

## Persistencia del nivel de silenciador manual (v26.5.2.1)

A partir de v26.5.2.1, el umbral de silenciador manual se guarda y restaura entre sesiones mediante la clave de configuración de la aplicación `LastManualSquelchLevel`. Esto evita que el valor sea sobrescrito por la lógica de silenciador de modo automático que aplica la radio. El umbral se recupera cuando se construye el applet de Controles de RX.

## Comportamiento del botón de silencio (v26.5.3)

En v26.5.3, se actualizó el comportamiento del botón de silencio. El botón de silencio ya no es un botón de alternancia verificable, sino un botón pulsador simple. Un solo clic en el botón silencia/activa el sonido del slice actual utilizando un temporizador diferido. Un doble clic en el botón silencia/activa el sonido de todos los slices propios. El icono visual (🔊/🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio mediante `SliceModel::audioMuteChanged`, no al hacer clic.

El estado de silencio NO se guarda ni se restaura al reconectar: la radio es la fuente de verdad para el silencio de audio.

## Mejoras en la entrada de frecuencia (v26.5.3)

En v26.5.3, se actualizó el analizador de entrada de frecuencia. La utilidad `FrequencyEntryParser` maneja la normalización de la entrada de texto en MHz. La entrada de frecuencia ahora admite entradas explícitas en MHz superiores a 54 MHz incluso cuando no se está en una antena XVTR: si el usuario ingresa un valor con un punto decimal explícito y el valor es superior a 54 MHz, el sistema lo trata como una entrada válida en MHz (hasta 50000 MHz) en lugar de aplicar escalado a kHz.

La función de conveniencia de banda de 3 dígitos (por ejemplo, escribir `1446` para sintonizar a 144.6 MHz) continúa funcionando solo en antenas XVTR.

Cuando se ingresa y confirma una frecuencia válida, el applet emite `directEntryCommitted(freqMhz, "rx-direct-entry")` en lugar de llamar a `tuneAndRecenter()` directamente.

## Consejos

- Si necesita un ancho que no coincida con ninguna predefinición, arrastre los bordes del widget de banda de paso del filtro para establecer un valor arbitrario, luego haga clic con el botón derecho en un botón predefinido para guardar ese ancho para uso futuro.
- Al guardar una predefinición haciendo clic con el botón derecho en un botón predefinido, la banda de paso se almacena en formato lo:hi si los bordes de la banda de paso actual se han establecido explícitamente, o en formato solo de ancho en caso contrario. Ambos formatos se cargan correctamente en todas las sesiones posteriores.
- Las predefiniciones son por modo. Cambiar de modo remodela el filtro y muestra los botones de predefiniciones para el nuevo modo.
- Los modos NT y RTTY utilizan las mismas predefiniciones de filtro y el mismo comportamiento de silenciador que DIGU y DIGL. El silenciador está deshabilitado en los modos NT, DIGU, DIGL y RTTY, y el silenciador apagado se envía a la radio automáticamente si el silenciador estaba previamente habilitado. El modo RTTY se agregó a la lista de desactivación automática en v26.5.1 para evitar que el silenciador recorte los caracteres FSK (#2504).
- Utilice el método `stepFilterWidth` desde combinaciones de teclas o scripts de macros para ensanchar y reducir la banda de paso del filtro sin hacer clic directamente en los botones de predefiniciones. El método siempre se sitúa en una predefinición apropiada para el modo.

## Solución de problemas

- **Los botones de predefiniciones no son visibles** — El modo activo es FM, NFM o DFM. Estos modos no exponen predefiniciones de filtro. Cambie el modo usando el cuadro combinado Mode a un modo que admita predefiniciones (por ejemplo, USB o CW).
- **Hacer clic derecho en un botón predefinido no hace nada visible** — Confirme que el slice está conectado a la radio. El applet de RX requiere una conexión activa a la radio para guardar valores predefinidos.
- **El botón NRL no es visible en una radio de la serie 6000** — Confirme que está ejecutando V0.9.4
