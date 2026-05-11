# Seleccione un ancho de filtro predefinido para el modo actual

Use los botones de predefinidos de ancho de filtro en el applet de Controles RX para aplicar rápidamente un ancho de banda estándar para el modo activo. Los valores predefinidos se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles RX requiere una conexión de radio activa.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.
- Establezca primero el modo del slice. Los valores predefinidos varían según el modo y no se muestran para los modos FM, NFM o DFM.

## Pasos

1. Abra el applet de Controles RX. Si no está visible, haga clic en el botón de la bandeja RX en la barra lateral derecha.
2. Si la fila de pestañas de slice está visible, haga clic en la pestaña (A a H) para el slice que desea ajustar.
3. Confirme que el modo mostrado en el combo Modo sea el correcto. Los filtros predefinidos cambian cuando cambia el modo.
4. Haga clic en cualquiera de los botones de predefinidos de ancho de filtro para aplicar ese ancho de banda inmediatamente. El ancho de filtro actual que se muestra en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el predefinido aplicado.
5. Para guardar el ancho de banda de paso del filtro actual como un predefinido, haga clic derecho en cualquier botón de predefinido de ancho de filtro y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control                     | Comportamiento                                                                                                                                                                                                                               | Predefinidos predeterminados según el modo                                                                                                                                                                                                                                                                                                   |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Predefinidos de ancho de filtro | Haga clic para aplicar un ancho de filtro predefinido; haga clic derecho para guardar el ancho actual como un predefinido.                                                                                                                   | Los botones están ocultos para modos FM/NFM/DFM; los predefinidos son por modo. La lectura de ancho (compartida con VfoWidget a través de RxApplet::formatFilterWidth) utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de predefinidos por modo para un ensanche/estrechamiento correcto según el modo (#2208). |
| Etiqueta de ancho de filtro | Indicador de solo lectura que muestra el ancho de banda del filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un predefinido o cuando se arrastran los bordes de la banda de paso.                                | —                                                                                                                                                                                                                                                                                                                                         |
| Widget de banda de paso del filtro | Arrastre el borde inferior o superior para establecer una banda de paso personalizada. Use los predefinidos para anchos estándar.                                                                                                            | —                                                                                                                                                                                                                                                                                                                                         |
| Modo                        | Anchuras predefinidas (Hz)                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                           |
| ---                         | ---                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                           |
| USB, LSB                    | 1800, 2100, 2400, 2700, 2900, 3300                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                           |
| AM, SAM                     | 5600, 6000, 8000, 10000, 12000, 14000                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                           |
| CW                          | 50, 100, 250, 400                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                           |
| DIGU, DIGL, NT              | 100, 300, 600, 1000, 1500, 2000                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                           |
| RTTY                        | 250, 300, 350, 400, 500, 1000                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                           |
| FM, NFM, DFM                | Sin predefinidos (botones ocultos)                                                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                           |

## Estrechamiento y ensanchamiento de la banda de paso del filtro mediante pasos

El método `stepFilterWidth(direction)` le permite recorrer la lista de predefinidos por modo desde cualquier acceso directo de aplicación o enlace de tecla. Pase `+1` para ensanchar la banda de paso al siguiente valor predefinido más grande, o `-1` para estrecharla al siguiente valor predefinido más pequeño. Dado que `stepFilterWidth` se direcciona a través de `applyFilterPreset`, todos los modos, incluidos LSB, CWL, DIGL, RTTY, AM y CW, utilizan la geometría de borde correcta para ese modo en lugar de una suposición simétrica.

Internamente, el método encuentra el predefinido cuyo ancho está más cerca de la banda de paso del slice actual, luego se mueve a la entrada siguiente o anterior en la lista (limitado a los límites válidos). Si el ancho actual ya es igual al predefinido más cercano y el paso se movería más allá de la lista, la operación se ignora.

## Formato de almacenamiento de predefinidos de filtro (v0.9.5.1)

A partir de la versión v0.9.5.1, los predefinidos de filtro almacenados en `FilterPresets` pueden representar un ancho de banda simple o una banda de paso completamente especificada con desplazamientos de borde inferior y superior explícitos. Ambos formatos se aceptan al cargar predefinidos guardados.

- **Formato solo de ancho** — Un único entero que representa el ancho de banda en Hz (por ejemplo, `2700`). Al aplicarlo, la radio posiciona la banda de paso simétricamente alrededor de la portadora según las reglas de desplazamiento predeterminadas del modo.
- **Formato Lo:Hi** — Dos enteros separados por dos puntos que representan los desplazamientos del borde inferior y superior de la banda de paso en Hz (por ejemplo, `300:3000`). El ancho se deriva como `hi − lo`. El valor `hi` debe ser mayor que el valor `lo`, de lo contrario, la entrada se ignora.

Las entradas en cualquiera de los formatos pueden aparecer en la misma lista guardada de predefinidos para un modo determinado. La lista está separada por comas. Se cargan hasta seis entradas para el applet de Controles RX (coincidiendo con el número máximo de botones de predefinidos mostrados).

Si una lista de predefinidos guardados se modifica externamente o una reconexión hace que la radio informe un número diferente de slices, los botones de predefinidos se reconstruyen automáticamente para reflejar los valores almacenados.

## Reducción de ruido y visibilidad del botón de filtro DSP

La siguiente tabla resume qué botones de reducción de ruido y filtro DSP están visibles según la serie de radio y el modo.

| Botón | Serie 6000 | Serie 8000 (DSP extendido) | Oculto cuando |
|-------|------------|----------------------------|----------------|
| NR    | Sí         | Sí                         | Modo FM        |
| NR2   | Sí         | Sí                         | Modo FM        |
| NB    | Sí         | Sí                         | Modo FM        |
| NRL   | Sí         | Sí                         | Modo FM        |
| NRS   | No         | Sí                         | Modo FM        |
| RNN   | No         | Sí                         | Modo CW o FM   |
| NRF   | No         | Sí                         | Modo FM        |

Antes de V0.9.4, el botón NRL solo se mostraba en radios de la serie 8000 (DSP extendido). A partir de V0.9.4, NRL también está disponible en radios de la serie 6000. NRS, RNN y NRF siguen siendo exclusivos de la serie 8000.

## Colores de pestañas de slice y distintivos (v0.9.3)

A partir de la versión v0.9.3, los botones de pestañas de slice y el distintivo de slice utilizan colores por slice administrados por el singleton `SliceColorManager` en lugar de una tabla de colores fija. El borde activo, el resaltado de fondo en los botones de pestaña y el fondo del distintivo reflejan el color asignado a ese slice. Los colores persisten entre sesiones y también se reflejan en los widgets VFO y las tiras de medidor. No se requiere ninguna acción; los colores se actualizan automáticamente cuando un slice está conectado.

## Comportamiento de las pestañas de slice al reconectar (v0.9.5.1)

Cuando AetherSDR se desconecta de la radio y se vuelve a conectar, o cuando cambia el número de slices disponibles, la fila de pestañas de slice se reconstruye correctamente. Específicamente:

- Si el número de slices informados por la radio difiere del número de botones de pestaña que se muestran actualmente, `clearSliceButtons()` elimina todos los botones de pestaña existentes y la fila se reconstruye desde cero.
- Mientras la fila de pestañas está eliminada, se restaura el distintivo de slice estático para que el applet continúe mostrando qué slice está vinculado.
- Las conexiones de señal de los botones de pestaña al controlador de activación de slice se establecen solo una vez por instancia de applet, evitando la acumulación de controladores duplicados a través de reconexiones.

No se requiere ninguna acción del usuario. Si el recuento de slices cambia (por ejemplo, después de un ciclo de desconexión y reconexión), la fila de pestañas se actualiza automáticamente.

## Consejos

- Si necesita un ancho que no coincida con ningún predefinido, arrastre los bordes del widget de banda de paso del filtro para establecer un valor arbitrario, luego haga clic derecho en un botón de predefinido para guardar ese ancho para uso futuro.
- Al guardar un predefinido haciendo clic derecho en un botón de predefinido, la banda de paso se almacena en formato lo:hi si los bordes de la banda de paso actual se han establecido explícitamente, o en formato solo de ancho en caso contrario. Ambos formatos se cargan correctamente en todas las sesiones posteriores.
- Los predefinidos son por modo. Cambiar de modo remodela el filtro y muestra los botones de predefinidos para el nuevo modo.
- Los modos NT y RTTY utilizan los mismos predefinidos de filtro y comportamiento de squelch que DIGU y DIGL. El squelch está deshabilitado en los modos NT, DIGU, DIGL y RTTY, y el squelch apagado se envía a la radio automáticamente si el squelch estaba previamente habilitado. El modo RTTY se agregó a la lista de desactivación automática en la versión v26.5.1 para evitar que el squelch recorte los caracteres FSK (#2504).
- Use el método `stepFilterWidth` desde enlaces de teclas o scripts de macros para ensanchar y estrechar la banda de paso del filtro sin hacer clic directamente en los botones de predefinidos. El método siempre se posiciona en un predefinido apropiado para el modo.

## Solución de problemas

- **Los botones de predefinidos no son visibles** — El modo activo es FM, NFM o DFM. Estos modos no exponen predefinidos de filtro. Cambie el modo usando el combo Modo a un modo que admita predefinidos (por ejemplo, USB o CW).
- **Hacer clic derecho en un botón de predefinido no hace nada visible** — Confirme que el slice esté conectado a la radio. El applet RX requiere una conexión de radio activa para guardar valores predefinidos.
- **El botón NRL no es visible en una radio de la serie 6000** — Confirme que está ejecutando V0.9.4 o posterior. Las versiones anteriores restringían NRL solo a radios de la serie 8000.
- **Los controles de squelch están atenuados** — El modo activo es DIGU, DIGL, NT, RTTY, CW o CWL. El squelch está deshabilitado en estos modos. En modos digitales (incluidos NT y RTTY), el squelch se apaga automáticamente; en modos CW, la radio administra el estado del squelch directamente.
- **La fila de pestañas de slice está en blanco después de reconectar** — Esto podría ocurrir en versiones anteriores a v0.9.5.1. Actualice a v0.9.5.1 o posterior. La fila de pestañas ahora se reconstruye automáticamente cuando el recuento de slices cambia al reconectar.

## Relacionados

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Descripción general de los Controles RX](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
<!-- docmesh:llm version=v0.9.8 date=2026-05-01 -->
