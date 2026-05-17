# Seleccionar un ancho de filtro preestablecido para el modo actual

Utilice los botones de ancho de filtro preestablecido en el applet de Controles de RX para aplicar rápidamente un ancho de banda estándar para el modo activo. Los valores preestablecidos se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles de RX requiere una conexión de radio activa.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.
- Configure el modo del slice primero. Los valores preestablecidos difieren según el modo y no se muestran valores preestablecidos para los modos FM, NFM o DFM.

## Pasos

1. Abra el applet de Controles de RX. Si no está visible, haga clic en el botón de la bandeja RX en la barra lateral derecha.
2. Si la fila de pestañas de slice está visible, haga clic en la pestaña (A a H) del slice que desea ajustar.
3. Confirme que el modo mostrado en el combo Modo sea correcto. Los valores preestablecidos de filtro cambian cuando cambia el modo.
4. Haga clic en cualquiera de los botones de ancho de filtro preestablecido para aplicar ese ancho de banda inmediatamente. El ancho de filtro actual mostrado en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el valor preestablecido aplicado.
5. Para guardar el ancho de banda de paso del filtro actual como un valor preestablecido, haga clic con el botón derecho en cualquier botón de ancho de filtro preestablecido y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control                      | Comportamiento                                                                                                                                                                                                                | Valores preestablecidos por defecto según el modo                                                                                                                                                                                                                                                                                                                                 |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Anchos de filtro preestablecidos | Haga clic para aplicar un ancho de filtro preestablecido; haga clic con el botón derecho para guardar el ancho actual como valor preestablecido.                                                                               | Botones ocultos para modos FM/NFM/DFM; los valores preestablecidos son por modo. El indicador de ancho (compartido con VfoWidget mediante RxApplet::formatFilterWidth) utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de valores preestablecidos por modo para el ajuste de ancho/estrechamiento correcto según el modo (#2208). |
| Etiqueta de ancho de filtro  | Indicador de solo lectura que muestra el ancho de banda del filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un valor preestablecido o cuando se arrastran los bordes del ancho de banda de paso. | —                                                                                                                                                                                                                                                                                                                                                                                 |
| Widget de ancho de banda de paso del filtro | Arrastre el borde inferior o superior para establecer un ancho de banda de paso personalizado. Use valores preestablecidos para anchos estándar.                                                                               | —                                                                                                                                                                                                                                                                                                                                                                                 |
| Modo                         | Anchos preestablecidos (Hz)                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                   |
| ---                          | ---                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                   |
| USB, LSB                     | 1800, 2100, 2400, 2700, 2900, 3300                                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                   |
| AM, SAM                      | 5600, 6000, 8000, 10000, 12000, 14000                                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                   |
| CW                           | 50, 100, 250, 400                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                   |
| DIGU, DIGL, NT               | 100, 300, 600, 1000, 1500, 2000                                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                   |
| RTTY                         | 250, 300, 350, 400, 500, 1000                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                   |
| FM, NFM, DFM                 | Sin valores preestablecidos (botones ocultos)                                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                   |

## Estrechar y ensanchar el ancho de banda de paso del filtro mediante pasos

El método `stepFilterWidth(direction)` le permite recorrer la lista de valores preestablecidos por modo desde cualquier acceso directo de la aplicación o combinación de teclas. Use `+1` para ensanchar el ancho de banda de paso al siguiente valor preestablecido más grande, o `-1` para estrechar al siguiente valor preestablecido más pequeño. Debido a que `stepFilterWidth` se enruta a través de `applyFilterPreset`, todos los modos (incluyendo LSB, CWL, DIGL, RTTY, AM y CW) utilizan la geometría de borde correcta para ese modo en lugar de una suposición simétrica.

Internamente, el método encuentra el valor preestablecido cuyo ancho es más cercano al ancho de banda de paso actual del slice, luego se mueve a la entrada siguiente o anterior en la lista (limitada a los límites válidos). Si el ancho actual ya es igual al valor preestablecido más cercano y el paso se movería más allá de la lista, la operación se ignora.

## Formato de almacenamiento de valores preestablecidos de filtro (v0.9.5.1)

A partir de v0.9.5.1, los valores preestablecidos de filtro almacenados en `FilterPresets` pueden representar un ancho de banda simple o un ancho de banda de paso completamente especificado con desplazamientos de borde inferior y superior explícitos. Ambos formatos son aceptados al cargar valores preestablecidos guardados.

- **Formato solo de ancho** — Un único entero que representa el ancho de banda en Hz (por ejemplo, `2700`). Al aplicarse, la radio posiciona el ancho de banda de paso simétricamente alrededor de la portadora según las reglas de desplazamiento predeterminadas del modo.
- **Formato Lo:Hi** — Dos enteros separados por dos puntos que representan los desplazamientos de los bordes inferior y superior del ancho de banda de paso en Hz (por ejemplo, `300:3000`). El ancho se deriva como `hi − lo`. El valor `hi` debe ser mayor que el valor `lo` o la entrada se ignora.

Las entradas en cualquier formato pueden aparecer en la misma lista de valores preestablecidos guardados para un modo determinado. La lista está separada por comas. Se cargan hasta seis entradas para el applet de Controles de RX (coincidiendo con el número máximo de botones de valores preestablecidos mostrados).

Si una lista de valores preestablecidos guardados se modifica externamente o una reconexión hace que la radio reporte un número diferente de slices, los botones de valores preestablecidos se reconstruyen automáticamente para reflejar los valores almacenados.

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

## Pestañas de slice y colores de la insignia (v0.9.3)

A partir de v0.9.3, los botones de las pestañas de slice y la insignia de slice utilizan colores por slice gestionados por el singleton `SliceColorManager` en lugar de una tabla de colores fija. El borde activo, el resaltado de fondo en los botones de pestaña y el fondo de la insignia reflejan todos el color asignado a ese slice. Los colores persisten entre sesiones y también se reflejan en los widgets de VFO y las tiras de medidores. No se requiere ninguna acción; los colores se actualizan automáticamente cuando un slice se conecta.

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

Cuando AetherSDR se desconecta de la radio y se vuelve a conectar, o cuando cambia el número de slices disponibles, la fila de pestañas de slice se reconstruye correctamente. Específicamente:

- Si el número de slices reportados por la radio difiere del número de botones de pestaña mostrados actualmente, `clearSliceButtons()` elimina todos los botones de pestaña existentes y la fila se reconstruye desde cero.
- Mientras la fila de pestañas se elimina, la insignia de slice estática se restaura para que el applet siga mostrando qué slice está vinculado.
- Las conexiones de señal de los botones de pestaña al controlador de activación de slice se establecen solo una vez por instancia del applet, evitando la acumulación de controladores duplicados a través de reconexiones.

No se requiere ninguna acción del usuario. Si el número de slices cambia (por ejemplo, después de un ciclo de desconexión y reconexión), la fila de pestañas se actualiza automáticamente.

## Mejoras en la selección de antena RX (v26.5.2.1)

En v26.5.2.1, se mejoró el menú de selección de antena RX para mostrar la lista de antenas RX dedicadas del slice cuando está disponible, en lugar de la lista de antenas global del estado del panadapter. Si el slice tiene una lista de antenas RX, el menú muestra esas entradas; de lo contrario, recurre a la lista de antenas global. Cada elemento del menú ahora:

- Utiliza el identificador de antena como su valor de datos subyacente (`act->setData(ant)`)
- Muestra una etiqueta legible mediante `antennaMenuLabel()`
- Muestra el identificador de antena sin procesar en la información sobre herramientas y la sugerencia de estado

El menú de selección de antena TX también se actualizó para usar el método `txAntennaOptions()` y `antennaMenuLabel()`. Ambos menús ahora usan `sel->data().toString()` al establecer la antena, por lo que el texto de la etiqueta es secundario al identificador de antena.

No se necesita configuración. Los menús se actualizan automáticamente cuando se reconectan a la radio.

## Cambio en la lógica de desactivación del modo RADE (v26.5.2.1)

En v26.5.2.1, se corrigió el comportamiento de la señal de desactivación del modo RADE. Anteriormente, al cambiar del modo RADE mediante el combo de modo, el applet verificaba `m_slice->mode() == "RADE"` antes de emitir `radeActivated(false)`. Esta verificación ya no funciona correctamente porque RADE es un modo solo del lado del cliente: la radio refleja el modo real (DIGL/DIGU) inmediatamente, por lo que `mode()` nunca devuelve "RADE" en el punto de la verificación. La verificación obsoleta se ha eliminado.

La opción RADE permanece disponible en el combo de modo solo cuando `HAVE_RADE` está definido en el momento de la compilación.

## Persistencia del nivel de squelch manual (v26.5.2.1)

A partir de v26.5.2.1, el umbral de squelch manual se guarda y restaura entre sesiones mediante la clave de configuración de la aplicación `LastManualSquelchLevel`. Esto evita que el valor sea sobrescrito por la lógica de squelch de modo automático que aplica la radio. El umbral se recuerda cuando se construye el applet de Controles de RX.

## Consejos

- Si necesita un ancho que no coincida con ningún valor preestablecido, arrastre los bordes del widget de ancho de banda de paso del filtro para establecer un valor arbitrario, luego haga clic con el botón derecho en un botón de valor preestablecido para guardar ese ancho para uso futuro.
- Al guardar un valor preestablecido haciendo clic con el botón derecho en un botón de valor preestablecido, el ancho de banda de paso se almacena en formato lo:hi si los bordes del ancho de banda de paso actual se han establecido explícitamente, o en formato solo de ancho en caso contrario. Ambos formatos se cargan correctamente en todas las sesiones posteriores.
- Los valores preestablecidos son por modo. Cambiar de modo reforma el filtro y muestra los botones de valores preestablecidos para el nuevo modo.
- Los modos NT y RTTY utilizan los mismos valores preestablecidos de filtro y comportamiento de squelch que DIGU y DIGL. El squelch está deshabilitado en los modos NT, DIGU, DIGL y RTTY, y la desactivación del squelch se envía a la radio automáticamente si el squelch estaba previamente habilitado. El modo RTTY se agregó a la lista de desactivación automática en v26.5.1 para evitar que el squelch recortara los caracteres FSK (#2504).
- Use el método `stepFilterWidth` desde combinaciones de teclas o scripts de macros para ensanchar y estrechar el ancho de banda de paso del filtro sin hacer clic directamente en los botones de valores preestablecidos. El método siempre se posiciona en un valor preestablecido apropiado para el modo.

## Solución de problemas

- **Los botones de valores preestablecidos no son visibles** — El modo activo es FM, NFM o DFM. Estos modos no exponen valores preestablecidos de filtro. Cambie el modo usando el combo Modo a un modo que admita valores preestablecidos (por ejemplo, USB o CW).
- **Hacer clic derecho en un botón de valor preestablecido no hace nada visible** — Confirme que el slice esté conectado a la radio. El applet de RX requiere una conexión de radio activa para guardar los valores preestablecidos.
- **El botón NRL no es visible en una radio de la serie 6000** — Confirme que está ejecutando V0.9.4 o posterior. Las versiones anteriores restringían NRL solo a radios de la serie 8000.
- **Los controles de squelch están atenuados** — El modo activo es DIGU, DIGL, NT, RTTY, CW o CWL. El squelch está deshabilitado en estos modos. En modos digitales (incluyendo NT y RTTY) el squelch se desactiva automáticamente; en modos CW la radio gestiona el estado del squelch directamente.
- **La fila de pestañas de slice está en blanco después de reconectar** — Esto podría ocurrir en versiones anteriores a v0.9.5.1. Actualice a v0.9.5.1 o posterior. La fila de pestañas ahora se reconstruye automáticamente cuando el número de slices cambia en la reconexión.

## Relacionado

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Descripción general de Controles de RX](overview.md)
- [Cambiar entre múltiples slices mediante la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
<!-- docmesh:llm version=v0.9.8 date=2026-05-01 -->
