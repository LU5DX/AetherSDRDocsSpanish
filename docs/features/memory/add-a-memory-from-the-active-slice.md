# Añadir una memoria desde la franja activa

Guarde la frecuencia, el modo y otros parámetros actuales de la franja activa como un nuevo canal de memoria para recuperarlo posteriormente.

## Antes de empezar

- Debe haber una radio conectada y al menos una franja activa.
- Abra el cuadro de diálogo Canales de memoria: **Settings > Memory...**

## Pasos

1. En el cuadro de diálogo Canales de memoria, haga clic en **Add**.
   - O pulse **Ctrl+N**.
2. Aparece una nueva fila en la tabla de memoria con la frecuencia, el modo y otros parámetros actuales de la franja activa.
3. (Opcional) Edite el nombre de la memoria u otros campos:
   - Haga clic en **Edit** para activar la edición en línea del campo Nombre.
   - Haga clic directamente en otras celdas para modificar sus valores.

## Función de cada control

| Control | Etiqueta | Comportamiento |
|---|---|---|
| Barra de título | Memory Channels | Barra de título sin marco con degradado de 18 píxeles, tirador de arrastre a la izquierda y título del cuadro de diálogo. Haga clic y arrastre para mover; haga doble clic para alternar entre maximizar/restaurar. |
| Botón Minimizar | — (Minimizar) | Minimiza el cuadro de diálogo. |
| Botón Maximizar | □ (Maximizar) | Maximiza o restaura el cuadro de diálogo. |
| Botón Cerrar | × (Cerrar) | Cierra el cuadro de diálogo. Escape borra primero el campo de búsqueda y luego cierra el cuadro de diálogo. |
| Arrastrar para mover | — | Haga clic y arrastre la barra de título para mover el cuadro de diálogo. Haga doble clic para alternar entre maximizar/restaurar. |
| Redimensionar en 8 ejes | — | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento. Zona de redimensionamiento de 12 píxeles. |
| Campo de búsqueda | Search: | Filtra la tabla por nombre de memoria. Tiene un botón de borrar; pulse Enter para aplicar. Ctrl+F enfoca este campo. |
| Filtro de perfil | Profile: | Filtra las memorias por perfil de transmisión global o activo. Valor predeterminado: "All Memories". |
| Tabla de memorias | — | Muestra las filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. Haga doble clic para sintonizar. Ctrl+Shift+A selecciona todas las filas. Ctrl+F enfoca el campo de búsqueda. El fondo de la tabla usa el color del tema `dialog/memory`. |
| Contador de selección | — | Muestra "<N> de <M> seleccionados". |
| Botón Add | Add | Crea una nueva memoria a partir de los parámetros actuales de la franja activa. Acceso directo: Ctrl+N. |
| Botón Edit | Edit | Activa la edición en línea del campo Nombre de la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. Acceso directo: F2 o Ctrl+E. |
| Botón Tune | Tune | Sintoniza la franja activa en la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. |
| Botón Select All | Select All | Selecciona todas las filas visibles (respetando búsqueda/filtro). Acceso directo: Ctrl+Shift+A. |
| Botón Remove | Remove | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso en eliminaciones por lotes. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. Acceso directo: Delete o Backspace. |
| Botón Import | Import... | Importa memorias desde un archivo CSV con cuadro de diálogo de progreso. Muestra el progreso de la importación y un resumen con las filas omitidas. |
| Botón Export | Export... | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |

## Consejos

- La memoria recibe automáticamente un número de índice secuencial. Para renombrarla, seleccione la fila y haga clic en **Edit** o pulse **F2**.
- La memoria captura la frecuencia, modo, paso, configuración de filtro y cualquier parámetro de repetidor FM (dirección de desplazamiento, desplazamiento, modo de tono, valor de tono, configuración de squelch) de la franja activa.
- El cuadro de diálogo recuerda su tamaño y posición entre sesiones.
- El botón Add siempre apunta a la franja activa; no hay selección por letra de franja.
- El cuadro de diálogo usa el color del tema establecido para `dialog/memory`. Los colores alternos de fila en la tabla de memorias siguen el color de fondo del tema.

## Relacionados

- [Edit a memory's name inline](edit-a-memory-s-name-inline.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
- [Use Ctrl+N to add a memory quickly](use-ctrl-n-to-add-a-memory-quickly.md)
