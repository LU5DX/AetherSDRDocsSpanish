# Seleccionar un ancho de filtro predefinido para el modo actual

Use los botones de predefinidos de ancho de filtro en el applet de Controles RX para aplicar rápidamente un ancho de banda estándar para el modo activo. Los predefinidos se guardan por modo en `FilterPresets`.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet de Controles RX requiere una conexión de radio activa.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.
- Configure primero el modo del slice. Los valores predefinidos difieren según el modo y no se muestran predefinidos para los modos FM, NFM o DFM.

## Pasos

1. Abra el applet de Controles RX. Si no está visible, haga clic en el botón RX en la barra lateral derecha.
2. Si la fila de pestañas de slice está visible, haga clic en la pestaña (de la A a la H) del slice que desea ajustar.
3. Confirme que el modo mostrado en el combo Mode sea correcto. Los predefinidos de filtro cambian cuando cambia el modo.
4. Haga clic en cualquiera de los botones de ancho de filtro predefinido para aplicar ese ancho de banda inmediatamente. El ancho de filtro actual mostrado en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el predefinido aplicado.
5. Para guardar el ancho de banda de paso actual como predefinido, haga clic derecho en cualquier botón de ancho de filtro predefinido y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control                    | Comportamiento                                                                                                                                                                                                                   | Valores predefinidos por modo                                                                                                                                                                                                                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Predefinidos de ancho de filtro | Haga clic para aplicar un ancho de filtro predefinido; haga clic derecho para guardar el ancho actual como predefinido.                                                                                                          | Los botones están ocultos para los modos FM/NFM/DFM; los predefinidos son por modo. La lectura de ancho (compartida con VfoWidget a través de `RxApplet::formatFilterWidth`) utiliza lógica según el modo, por lo que los modos SSB/digitales muestran el ancho etiquetado correcto (#2197). El método `stepFilterWidth(direction)` recorre la lista de predefinidos por modo para ensanchar/reducir según el modo (#2208). |
| Etiqueta de ancho de filtro     | Indicador de solo lectura que muestra el ancho de banda del filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un predefinido o cuando se arrastran los bordes del ancho de banda de paso.         | —                                                                                                                                                                                                                                                                                                                                        |
| Widget de ancho de banda de paso | Arrastre el borde inferior o superior para establecer un ancho de banda de paso personalizado. Use los predefinidos para anchos estándar.                                                                                        | —                                                                                                                                                                                                                                                                                                                                        |
| Mode                        | Anchuras predefinidas (Hz)                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                          |
| ---                         | ---                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                          |
| USB, LSB                    | 1800, 2100, 2400, 2700, 2900, 3300                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                          |
| AM, SAM                     | 5600, 6000, 8000, 10000, 12000, 14000                                                                                                                              |                                                                                                                                                                                                                                                                                                                                          |
| CW                          | 50, 100, 250, 400                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                          |
| DIGU, DIGL, NT              | 100, 300, 600, 1000, 1500, 2000                                                                                                                                   |                                                                                                                                                                                                                                                                                                                                          |
| RTTY                        | 250, 300, 350, 400, 500, 1000                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                          |
| FM, NFM, DFM                | Sin predefinidos (botones ocultos)                                                                                                                                |                                                                                                                                                                                                                                                                                                                                          |
| RADE                        | Sin predefinidos (solo del lado del cliente, la radio repite el modo real)                                                                                        |                                                                                                                                                                                                                                                                                                                                          |

## Reducir y ensanchar el ancho de banda de paso mediante pasos

El método `stepFilterWidth(direction)` le permite recorrer la lista de predefinidos por modo desde cualquier acceso directo de la aplicación o combinación de teclas. Use `+1` para ensanchar el ancho de banda al siguiente predefinido más grande, o `-1` para reducirlo al siguiente predefinido más pequeño. Dado que `stepFilterWidth` se enruta a través de `applyFilterPreset`, todos los modos (incluyendo LSB, CWL, DIGL, RTTY, AM y CW) utilizan la geometría de borde correcta para ese modo en lugar de una suposición simétrica.

Internamente, el método encuentra el predefinido cuyo ancho está más cerca del ancho de banda del slice actual, luego se mueve a la entrada siguiente o anterior en la lista (dentro de los límites válidos). Si el ancho actual ya es igual al predefinido más cercano y el paso se saldría de la lista, la operación se ignora.

## Formato de almacenamiento de predefinidos de filtro (v0.9.5.1)

A partir de la v0.9.5.1, los predefinidos de filtro almacenados en `FilterPresets` pueden representar ya sea un ancho de banda simple o un ancho de banda de paso completamente especificado con desplazamientos de borde inferior y superior explícitos. Ambos formatos se aceptan al cargar predefinidos guardados.

- **Formato solo de ancho** — Un único entero que representa el ancho de banda en Hz (por ejemplo, `2700`). Al aplicarse, la radio posiciona el ancho de banda de paso simétricamente alrededor de la portadora según las reglas de desplazamiento predeterminadas del modo.
- **Formato Lo:Hi** — Dos enteros separados por dos puntos que representan los desplazamientos de borde inferior y superior del ancho de banda de paso en Hz (por ejemplo, `300:3000`). El ancho se obtiene como `hi − lo`. El valor `hi` debe ser mayor que el valor `lo`; de lo contrario, la entrada se ignora.

Las entradas en cualquiera de los formatos pueden aparecer en la misma lista de predefinidos guardados para un modo dado. La lista está separada por comas. Se cargan hasta seis entradas para el applet de Controles RX (que coincide con el número máximo de botones de predefinidos mostrados).

Si una lista de predefinidos guardados se modifica externamente o si una reconexión provoca que la radio informe un número diferente de slices, los botones de predefinidos se reconstruyen automáticamente para reflejar los valores almacenados.

## Visibilidad de los botones de reducción de ruido y filtro DSP

La siguiente tabla resume qué botones de reducción de ruido y filtro DSP son visibles según la serie de la radio y el modo.

| Botón | Serie 6000 | Serie 8000 (DSP extendido) | Oculto cuando |
|-------|------------|---------------------------|-------------|
| NR    | Sí         | Sí                        | Modo FM     |
| NR2   | Sí         | Sí                        | Modo FM     |
| NB    | Sí         | Sí                        | Modo FM     |
| NRL   | Sí         | Sí                        | Modo FM     |
| NRS   | No         | Sí                        | Modo FM     |
| RNN   | No         | Sí                        | Modo CW o FM |
| NRF   | No         | Sí                        | Modo FM     |

Antes de la V0.9.4, el botón NRL solo se mostraba en las radios de la serie 8000 (DSP extendido). A partir de la V0.9.4, NRL también está disponible en las radios de la serie 6000. NRS, RNN y NRF siguen siendo solo para la serie 8000.

## Pestañas de slice y colores de insignia (v0.9.3)

A partir de la v0.9.3, los botones de pestaña de slice y la insignia de slice usan colores por slice gestionados por el singleton `SliceColorManager` en lugar de una tabla de colores fija. El borde activo, el resaltado de fondo en los botones de pestaña y el fondo de la insignia reflejan el color asignado a ese slice. Los colores persisten entre sesiones y también se reflejan en los widgets VFO y las tiras de medidor. No se requiere ninguna acción; los colores se actualizan automáticamente cuando se conecta un slice.

## Comportamiento de pestañas de slice en reconexión (v0.9.5.1)

Cuando AetherSDR se desconecta de la radio y se reconecta, o cuando cambia el número de slices disponibles, la fila de pestañas de slice se reconstruye correctamente. Específicamente:

- Si el número de slices informado por la radio difiere del número de botones de pestaña mostrados actualmente, `clearSliceButtons()` elimina todos los botones de pestaña existentes y la fila se reconstruye desde cero.
- Mientras la fila de pestañas está eliminada, la insignia de slice estática se restaura para que el applet continúe mostrando qué slice está vinculado.
- Las conexiones de señal de los botones de pestaña al controlador de activación de slice se establecen solo una vez por instancia del applet, evitando la acumulación de controladores duplicados a través de las reconexiones.

No se requiere ninguna acción del usuario. Si el número de slices cambia (por ejemplo, después de un ciclo de desconexión y reconexión), la fila de pestañas se actualiza automáticamente.

## Mejoras en la selección de antena RX (v26.5.2.1)

En la v26.5.2.1, se mejoró el menú de selección de antena RX para mostrar la lista de antenas RX dedicadas del slice cuando esté disponible, en lugar de la lista global de antenas del estado del panadapter. Si el slice tiene una lista de antenas RX, el menú muestra esas entradas; de lo contrario, recurre a la lista global de antenas. Cada elemento del menú ahora:

- Utiliza el identificador de la antena como su valor de datos subyacente (`act->setData(ant)`)
- Muestra una etiqueta legible para humanos a través de `antennaMenuLabel()`
- Muestra el identificador de antena sin procesar en la información sobre herramientas y la información de estado

El menú de selección de antena TX también se actualizó para usar el método `txAntennaOptions()` y `antennaMenuLabel()`. Ambos menús ahora usan `sel->data().toString()` al configurar la antena, por lo que el texto de la etiqueta es secundario al identificador de la antena.

No se necesita configuración. Los menús se actualizan automáticamente al reconectarse a la radio.

## Cambio en la lógica de desactivación del modo RADE (v26.5.2.1)

En la v26.5.2.1, se corrigió el comportamiento de la señal de desactivación del modo RADE. Anteriormente, al salir del modo RADE a través del combo Mode, el applet verificaba `m_slice->mode() == "RADE"` antes de emitir `radeActivated(false)`. Esta verificación ya no funciona correctamente porque RADE es un modo solo del lado del cliente: la radio repite inmediatamente el modo real (DIGL/DIGU), por lo que `mode()` nunca devuelve "RADE" en el momento de la verificación. La verificación obsoleta se ha eliminado.

La opción RADE permanece disponible en el combo Mode solo cuando `HAVE_RADE` está definido en el momento de la compilación.

## Persistencia del nivel de squelch manual (v26.5.2.1)

A partir de la v26.5.2.1, el umbral de squelch manual se guarda y restaura entre sesiones a través de la clave de configuración de la aplicación `LastManualSquelchLevel`. Esto evita que el valor sea sobrescrito por la lógica de squelch de modo automático que aplica la radio. El umbral se recuerda cuando se construye el applet de Controles RX.

## Comportamiento del botón de silencio (v26.5.3)

En la v26.5.3, se actualizó el comportamiento del botón de silencio. El botón de silencio ya no es un botón de alternancia seleccionable; es un botón pulsador simple. Al hacer clic una vez en el botón, se silencia/activa el sonido del slice actual utilizando un temporizador diferido. Al hacer doble clic en el botón, se silencia/activa el sonido de todos los slices propiedad. El icono visual (🔊/🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`, no con el clic mismo.

El estado de silencio NO se guarda ni se restaura durante la reconexión: la radio es la fuente de verdad para la activación/desactivación del audio del micrófono.

## Mejoras en la entrada de frecuencia (v26.5.3)

En la v26.5.3, se actualizó el analizador de entrada de frecuencia. La utilidad `FrequencyEntryParser` maneja la normalización de la entrada de texto en MHz. La entrada de frecuencia ahora admite entradas explícitas de MHz por encima de 54 MHz incluso cuando no se usa una antena XVTR: si el usuario ingresa un valor con un punto decimal explícito y el valor es superior a 54 MHz, el sistema lo trata como una entrada válida de MHz (hasta 50000 MHz) en lugar de aplicar una escala de kHz.

La función de conveniencia de banda de 3 dígitos (por ejemplo, escribir `1446` para sintonizar 144,6 MHz) continúa funcionando solo en antenas XVTR.

Cuando se ingresa y confirma una frecuencia válida, el applet emite `directEntryCommitted(freqMhz, "rx-direct-entry")` en lugar de llamar a `tuneAndRecenter()` directamente.

## Visualización de la marca central del control deslizante de paneo (v26.6.1)

En la v26.6.1, se actualizó el control deslizante de paneo L/R para incluir un indicador visual de la marca central. El relleno del control deslizante ahora se ancla desde el centro hacia afuera: cuando el control está a la izquierda del centro, la ranura se rellena desde el control hasta el centro en color de acento; cuando el control está a la derecha, solo se rellena la mitad derecha de la ranura. Se pinta un pequeño punto de marca central en la ranura para que pueda ver la posición neutra de un vistazo. Haga doble clic en el control deslizante para restablecer al centro (50).

El comportamiento anterior aplicaba el relleno estándar del control deslizante desde el borde izquierdo, lo que era engañoso para controles anclados al centro. No se requiere ningún cambio de configuración.

## Estilo de botones con el gestor de temas (v26.6.1)

A partir de la v26.6.1, los botones de filtro predefinido (1.8K, 2.1K, etc.) y todos los demás botones pulsadores en el applet de Controles RX utilizan colores gestionados por el tema en lugar de valores hexadecimales codificados. El fondo del botón, el borde, los colores de flotación y de pulsado se resuelven a través de `ThemeManager` usando los tokens `color.background.1`, `color.background.2` y `color.accent`. Esto asegura que los botones del applet se re-tematizen de manera consistente cuando cambia el tema de la aplicación. No se requiere ninguna acción del usuario.

## Consejos

- Si necesita un ancho que no coincida con ningún predefinido, arrastre los bordes del widget de ancho de banda de paso para establecer un valor arbitrario, luego haga clic derecho en un botón de predefinido para guardar ese ancho para uso futuro.
- Al guardar un predefinido haciendo clic derecho en un botón de predefinido, el ancho de banda de paso se almacena en formato lo:hi si los bordes del ancho de banda de paso actual se han establecido
