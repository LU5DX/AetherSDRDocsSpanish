# Seleccione un valor preestablecido de ancho de filtro para el modo actual

Use los botones de valores preestablecidos de ancho de filtro en el applet de Controles RX para aplicar rápidamente un ancho de banda estándar para el modo activo. Los valores preestablecidos se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles RX requiere una conexión de radio activa.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.
- Configure primero el modo del slice. Los valores preestablecidos difieren según el modo y no se muestran valores preestablecidos para los modos FM, NFM o DFM.

## Pasos

1. Abra el applet de Controles RX. Si no está visible, haga clic en el botón de la bandeja RX en la barra lateral derecha.
2. Si la fila de pestañas de slice está visible, haga clic en la pestaña (A hasta H) del slice que desea ajustar.
3. Confirme que el modo mostrado en el cuadro combinado de Modo sea el correcto. Los valores preestablecidos de filtro cambian cuando cambia el modo.
4. Haga clic en cualquiera de los botones de valores preestablecidos de ancho de filtro para aplicar ese ancho de banda inmediatamente. El ancho de filtro actual mostrado en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el valor preestablecido aplicado.
5. Para guardar el ancho de banda de paso del filtro actual como un valor preestablecido, haga clic con el botón derecho en cualquier botón de valor preestablecido de ancho de filtro y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control                     | Comportamiento                                                                                                                                                                                                                                                      | Valores preestablecidos por defecto por modo                                                                                                                                                                                                                                                                                               |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Valores preestablecidos de ancho de filtro | Haga clic para aplicar un ancho de filtro preestablecido; haga clic con el botón derecho para guardar el ancho actual como un valor preestablecido. Botones ocultos para modos FM/NFM/DFM.                                                                          | Los valores preestablecidos son por modo. La lectura de ancho (compartida con VfoWidget a través de RxApplet::formatFilterWidth) usa lógica consciente del modo, por lo que los modos SSB/digitales muestran el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de valores preestablecidos por modo para el ensanche/estrechamiento correctos según el modo (#2208). |
| Etiqueta de ancho de filtro | Indicador de solo lectura que muestra el ancho de banda del filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un valor preestablecido o cuando se arrastran los bordes de la banda de paso.                                         | —                                                                                                                                                                                                                                                                                                                                          |
| Widget de banda de paso del filtro | Arrastre el borde bajo o alto para establecer una banda de paso personalizada. Use los valores preestablecidos para anchos estándar.                                                                                                                               | —                                                                                                                                                                                                                                                                                                                                          |
| Modo                        | Anchos preestablecidos (Hz)                                                                                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                                            |
| ---                         | ---                                                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                            |
| USB, LSB                    | 1800, 2100, 2400, 2700, 2900, 3300                                                                                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                            |
| AM, SAM                     | 5600, 6000, 8000, 10000, 12000, 14000                                                                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                            |
| CW                          | 50, 100, 250, 400, 500, 600                                                                                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                                            |
| DIGU, DIGL, NT              | 100, 300, 600, 1000, 1500, 2000                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                            |
| RTTY                        | 250, 300, 350, 400, 500, 1000                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                            |
| FM, NFM, DFM                | Sin valores preestablecidos (botones ocultos)                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                            |
| RADE                        | Sin valores preestablecidos (solo del lado del cliente, la radio devuelve el modo real)                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                            |

## Estrechar y ensanchar la banda de paso del filtro mediante pasos

El método `stepFilterWidth(direction)` le permite recorrer la lista de valores preestablecidos por modo desde cualquier atajo de aplicación o enlace de teclado. Pase `+1` para ensanchar la banda de paso al siguiente valor preestablecido más grande, o `-1` para estrechar al siguiente valor preestablecido más pequeño. Debido a que `stepFilterWidth` se enruta a través de `applyFilterPreset`, todos los modos (incluyendo LSB, CWL, DIGL, RTTY, AM y CW) usan la geometría de borde correcta para ese modo en lugar de una suposición simétrica.

Internamente, el método encuentra el valor preestablecido cuyo ancho esté más cerca de la banda de paso actual del slice, luego se mueve a la entrada siguiente o anterior en la lista (limitado a los límites válidos). Si el ancho actual ya es igual al valor preestablecido más cercano y el paso se movería más allá de la lista, la operación se ignora.

## Formato de almacenamiento de valores preestablecidos de filtro (v0.9.5.1)

A partir de v0.9.5.1, los valores preestablecidos de filtro almacenados en `FilterPresets` pueden representar ya sea un ancho de banda simple o una banda de paso completamente especificada con desplazamientos de borde bajo y alto explícitos. Ambos formatos son aceptados al cargar valores preestablecidos guardados.

- **Formato solo ancho** — Un solo entero que representa el ancho de banda en Hz (por ejemplo, `2700`). Al aplicarse, la radio posiciona la banda de paso simétricamente alrededor de la portadora según las reglas de desplazamiento por defecto del modo.
- **Formato Lo:Hi** — Dos enteros separados por dos puntos que representan los desplazamientos de borde bajo y alto de la banda de paso en Hz (por ejemplo, `300:3000`). El ancho se deriva como `hi − lo`. El valor `hi` debe ser mayor que el valor `lo` o la entrada se ignora.

Las entradas en cualquiera de los formatos pueden aparecer en la misma lista de valores preestablecidos guardada para un modo dado. La lista está separada por comas. Se cargan hasta seis entradas para el applet de Controles RX (correspondientes al número máximo de botones de valores preestablecidos mostrados).

Si una lista de valores preestablecidos guardada es cambiada externamente o una reconexión hace que la radio reporte un número diferente de slices, los botones de valores preestablecidos se reconstruyen automáticamente para reflejar los valores almacenados.

## Visibilidad de los botones de reducción de ruido y filtro DSP

La siguiente tabla resume qué botones de reducción de ruido y filtro DSP son visibles según la serie de radio y el modo.

| Botón | Serie 6000 | Serie 8000 (DSP extendido) | Oculto cuando |
|-------|------------|---------------------------|---------------|
| NR    | Sí         | Sí                        | Modo FM       |
| NR2   | Sí         | Sí                        | Modo FM       |
| NB    | Sí         | Sí                        | Modo FM       |
| NRL   | Sí         | Sí                        | Modo FM       |
| NRS   | No         | Sí                        | Modo FM       |
| RNN   | No         | Sí                        | Modo CW o FM  |
| NRF   | No         | Sí                        | Modo FM       |

Antes de V0.9.4, el botón NRL solo se mostraba en radios de la serie 8000 (DSP extendido). A partir de V0.9.4, NRL también está disponible en radios de la serie 6000. NRS, RNN y NRF siguen siendo solo para la serie 8000.

## Pestañas de slice y colores de insignias (v0.9.3)

A partir de v0.9.3, los botones de las pestañas de slice y la insignia de slice usan colores por slice gestionados por el singleton `SliceColorManager` en lugar de una tabla de colores fija. El borde activo, el resaltado de fondo en los botones de las pestañas y el fondo de la insignia reflejan el color asignado a ese slice. Los colores persisten entre sesiones y también se reflejan en los widgets VFO y las tiras de medidores. No se requiere ninguna acción; los colores se actualizan automáticamente cuando un slice está conectado.

## Comportamiento de las pestañas de slice en la reconexión (v0.9.5.1)

Cuando AetherSDR se desconecta de la radio y se vuelve a conectar, o cuando cambia el número de slices disponibles, la fila de pestañas de slice se reconstruye correctamente. Específicamente:

- Si el número de slices reportados por la radio difiere del número de botones de pestaña actualmente mostrados, `clearSliceButtons()` elimina todos los botones de pestaña existentes y la fila se reconstruye desde cero.
- Mientras la fila de pestañas está eliminada, la insignia de slice estática se restaura para que el applet continúe mostrando qué slice está vinculado.
- Las conexiones de señal de los botones de pestaña al controlador de activación de slice se establecen solo una vez por instancia del applet, evitando la acumulación de controladores duplicados a través de las reconexiones.

No se requiere ninguna acción del usuario. Si el número de slices cambia (por ejemplo, después de un ciclo de desconexión y reconexión), la fila de pestañas se actualiza automáticamente.

## Mejoras en la selección de antena RX (v26.5.2.1, v26.7.4)

En v26.5.2.1, el menú de selección de antena RX se mejoró para mostrar la lista de antenas RX dedicadas del slice cuando esté disponible, en lugar de la lista de antenas global del estado del panadapter. Si el slice tiene una lista de antenas RX, el menú muestra esas entradas; de lo contrario, recurre a la lista de antenas global. Cada elemento del menú ahora:

- Usa el identificador de la antena como su valor de datos subyacente (`act->setData(ant)`)
- Muestra una etiqueta legible para humanos a través de `antennaMenuLabel()`
- Muestra el identificador de antena sin procesar en la información sobre herramientas y la sugerencia de estado

En v26.7.4, el menú de antena RX se mejoró aún más para integrarse con la función KiwiSDR. Si un gestor KiwiSDR está disponible, los tokens de antena virtual del gestor KiwiSDR se agregan a las opciones del menú. El menú ahora se muestra con `popup()` en lugar de `exec()`, y un controlador de señal activado gestiona la selección. Cuando se selecciona una antena virtual (asociada con un perfil KiwiSDR), el applet emite `kiwiRxAntennaSelected(sliceId, profileId)`. Cuando se selecciona una antena Flex física, emite `flexRxAntennaSelected(sliceId)` y llama a `slice->setRxAntenna(token)`. El perfil KiwiSDR activo para el slice se muestra como marcado. El menú usa `QPointer<SliceModel>` para evitar el uso después de la liberación si el slice se destruye mientras el menú está abierto.

El menú de selección de antena TX también se actualizó para usar el método `txAntennaOptions()` y `antennaMenuLabel()`. Ambos menús ahora usan `sel->data().toString()` al establecer la antena, por lo que el texto de la etiqueta es secundario al identificador de la antena.

No se necesita configuración. Los menús se actualizan automáticamente cuando se reconecta a la radio.

## Cambio en la lógica de desactivación del modo RADE (v26.5.2.1)

En v26.5.2.1, se corrigió el comportamiento de la señal de desactivación del modo RADE. Anteriormente, al cambiar del modo RADE a través del cuadro combinado de Modo, el applet verificaba `m_slice->mode() == "RADE"` antes de emitir `radeActivated(false)`. Esta verificación ya no funciona correctamente porque RADE es un modo solo del lado del cliente — la radio devuelve el modo real (DIGL/DIGU) inmediatamente, por lo que `mode()` nunca devuelve "RADE" en el punto de la verificación. La verificación obsoleta se ha eliminado.

La opción RADE permanece disponible en el cuadro combinado de Modo solo cuando `HAVE_RADE` está definido en el momento de la compilación.

## Persistencia del nivel de squelch manual (v26.5.2.1)

A partir de v26.5.2.1, el umbral de squelch manual se guarda y restaura entre sesiones a través de la clave de configuración de la aplicación `LastManualSquelchLevel`. Esto evita que el valor sea sobrescrito por la lógica de squelch de modo automático que aplica la radio. El umbral se recupera cuando se construye el applet de Controles RX.

## Comportamiento del botón de silencio (v26.5.3)

En v26.5.3, se actualizó el comportamiento del botón de silencio. El botón de silencio ya no es un botón de alternancia seleccionable — es un botón pulsador simple. Un solo clic en el botón silencia/reanuda el sonido del slice actual usando un temporizador diferido. Un doble clic en el botón silencia/reanuda el sonido de todos los slices propios. El icono visual (🔊/🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`, no al hacer clic.

El estado de silencio NO se guarda ni se restaura en la reconexión — la radio es la fuente de verdad para el silencio de audio.

## Mejoras en la entrada de frecuencia (v26.5.3)

En v26.5.3, se actualizó el analizador de entrada de frecuencia. La utilidad `FrequencyEntryParser` maneja la normalización de la entrada de texto en MHz. La entrada de frecuencia ahora admite entradas explícitas en MHz por encima de 54 MHz incluso cuando no se está en una antena XVTR — si el usuario ingresa un valor con un punto decimal explícito y el valor está por encima de 54 MHz, el sistema lo trata como una entrada válida en MHz (hasta 50000 MHz) en lugar de aplicar la escala de kHz.

La función de conveniencia de banda de 3 dígitos (por ejemplo, escribir `1446` para sintonizar 144.6 MHz) continúa funcionando solo en antenas XVTR.

Cuando se ingresa y confirma una frecuencia válida, el applet emite `directEntryCommitted(freqMhz, "rx-direct-entry")` en lugar de llamar a `tuneAndRecenter()` directamente.

## Visualización de la marca central del control deslizante de paneo (v26.6.1)

En v26.6.1, se actualizó el control deslizante de paneo L/R para incluir un indicador visual de marca central. El relleno del control deslizante ahora se ancla desde el centro hacia afuera — cuando el control está a la izquierda del centro, la ranura se rellena desde el control hasta el centro en color de acento; cuando el control está a la derecha, solo la mitad derecha de la ranura se rellena. Se pinta un pequeño punto de marca central en la ranura para que pueda ver la posición neutra de un vistazo. Haga doble clic en el control deslizante para restablecer al centro (50).

El comportamiento anterior aplicaba el relleno estándar del control deslizante desde el borde izquierdo, lo que era engañoso para controles anclados al centro. No se requiere ningún cambio de configuración.

## Estilo de botones con el gestor de temas (v26.6.1)

A partir de v26.6.1,
