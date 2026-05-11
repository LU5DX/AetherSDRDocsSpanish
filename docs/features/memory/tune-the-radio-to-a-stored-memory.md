# Sintonizar la Radio a una Memoria Almacenada

Abra el cuadro de diálogo Canales de Memoria para encontrar una frecuencia almacenada y enviarla directamente al receptor de slice activo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo Canales de Memoria requiere una conexión activa con la radio.
- Debe tener al menos una memoria ya almacenada. Consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si no tiene ninguna.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el cuadro de diálogo Canales de Memoria.
2. Localice la memoria que desea. Utilice el campo `Search:` para filtrar por nombre, o use el cuadro combinado `Profile:` para reducir la lista por perfil.
3. Haga clic en la fila de la tabla de memorias para seleccionarla.
4. Haga clic en `Tune`.

El slice activo se sintoniza a la frecuencia, modo y configuración de filtro almacenados en esa memoria.

**Atajo:** Haga doble clic en cualquier fila de la tabla de memorias para sintonizar inmediatamente sin hacer clic en `Tune`.

## Qué hace cada control

| Control                     | Comportamiento                                                                                                                                                                                                                                                                                                         | Notas                                                                                                                                                   |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Search:`                   | Filtra la tabla de memorias a las filas cuyo nombre coincida con el texto que escribe. Presione Enter o limpie el campo para restablecer. Ctrl+F enfoca el campo de búsqueda.                                                                                                                                          | Tiene botón de limpiar.                                                                                                                                 |
| `Profile:`                  | Filtra la tabla a las memorias que pertenecen al perfil global o de transmisión seleccionado.                                                                                                                                                                                                                          | Recolecta nombres de perfil de los perfiles globales y de transmisión de RadioModel.                                                                    |
| Tabla de memorias           | Muestra y edita filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frecuencia, Nombre, Modo). Columnas: Grupo, Propietario, Frecuencia, Nombre, Modo, Paso, Dirección de desplazamiento FM TX, Desplazamiento del repetidor, Modo de tono, Valor de tono, Squelch, Nivel de squelch, Filtro RX bajo, Filtro RX alto, RTTY Mark, RTTY Shift, Offset DIGL, Offset DIGU. | ExtendedSelection; modo de edición en línea mediante el botón Edit o F2/Ctrl+E. Delete/Retroceso elimina las filas seleccionadas. Doble clic sintoniza. Ctrl+Shift+A selecciona todo. |
| `Import...`                 | Importa memorias desde un archivo CSV con cuadro de diálogo de progreso.                                                                                                                                                                                                                                               | Muestra el progreso de importación y un resumen con las filas omitidas.                                                                                |
| `Export...`                 | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                                                                                                                                                                                                                                | Valida el CSV generado antes de guardarlo.                                                                                                              |
| `Add`                       | Crea una nueva memoria desde el slice actual (activo). Atajo Ctrl+N.                                                                                                                                                                                                                                                   | Sin selección por letra; siempre apunta al slice activo.                                                                                                |
| `Edit`                      | Activa el modo de edición en línea en el campo Nombre de la memoria seleccionada. F2 o Ctrl+E también activan la edición.                                                                                                                                                                                              | Solo habilitado cuando exactamente una memoria está seleccionada.                                                                                       |
| `Tune`                      | Sintoniza el slice activo a la memoria seleccionada. Requiere que exactamente una fila esté seleccionada.                                                                                                                                                                                                              |                                                                                                                                                         |
| `Select All`                | Selecciona todas las filas visibles (respetando la búsqueda/filtro). Atajo Ctrl+Shift+A.                                                                                                                                                                                                                               |                                                                                                                                                         |
| `Remove`                    | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para eliminación por lotes. La tecla Delete/Retroceso también activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay >1 fila seleccionada.                                                                                          |                                                                                                                                                         |
| Barra de título — Canales de Memoria | Barra de título sin bordes de 18 px con degradado, glifo de agarre a la izquierda y el título del diálogo.                                                                                                                                                                                                           | Agregado en v26.5.1 (#2509). Utiliza FramelessWindowTitleBar; cambio de tamaño en 8 ejes mediante FramelessResizer.                                     |
| — (Minimizar)              | Minimiza el cuadro de diálogo.                                                                                                                                                                                                                                                                                         |                                                                                                                                                         |
| □ (Maximizar)              | Maximiza o restaura el cuadro de diálogo.                                                                                                                                                                                                                                                                              |                                                                                                                                                         |
| × (Cerrar)                 | Cierra el cuadro de diálogo. Escape primero limpia la búsqueda, luego cierra.                                                                                                                                                                                                                                          |                                                                                                                                                         |
| Arrastrar para mover        | Haga clic y arrastre la barra de título para mover el cuadro de diálogo.                                                                                                                                                                                                                                               | Haga doble clic en la barra de título para alternar maximizar/restaurar.                                                                                |
| Cambio de tamaño en 8 ejes  | Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para cambiar su tamaño. El cursor cambia para indicar la dirección del cambio de tamaño.                                                                                                                                                          | Zona de cambio de tamaño de 12 px mediante FramelessResizer.                                                                                            |
| Recuento de selección       | Muestra '<N> de <M> seleccionados'.                                                                                                                                                                                                                                                                                    |                                                                                                                                                         |

## Consejos

- Si no puede ver la memoria que desea, verifique si `Profile:` está configurado con un filtro que la excluye. Configure `Profile:` para mostrar todas las entradas.
- En Linux y Windows, mantenga presionado Ctrl y haga clic para seleccionar filas individuales sin deseleccionar otras. En macOS, use Comando-clic. Solo la primera memoria seleccionada se usa al hacer clic en `Tune`.
- Use el botón `Add` o Ctrl+N para almacenar rápidamente la frecuencia del slice actual como una nueva memoria.
- Use los botones `Import...` y `Export...` para transferir memorias entre radios o compartirlas con otros operadores.

## Solución de problemas

- **`Tune` no tiene efecto o está deshabilitado** — Confirme que una sola fila esté seleccionada en la tabla de memorias y que AetherSDR esté conectado a la radio.
- **La memoria que desea no aparece en la tabla** — El filtro `Search:` o `Profile:` puede estar ocultándola. Limpie el campo `Search:` y configure `Profile:` para mostrar todas las entradas.
- **No se puede agregar una memoria** — Asegúrese de que la radio esté conectada y que haya un slice activo disponible.

## Relacionado

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Recuperar una memoria de repetidor FM y restaurar el desplazamiento y el tono CTCSS](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Resumen de Canales de Memoria](overview.md)
