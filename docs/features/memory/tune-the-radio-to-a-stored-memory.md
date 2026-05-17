# Sintonizar la radio a una memoria almacenada

Abra el diálogo de Canales de Memoria para encontrar una frecuencia almacenada y enviarla directamente al receptor de slice activo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo de Canales de Memoria requiere una conexión activa a la radio.
- Debe tener al menos una memoria ya almacenada. Consulte [Añadir una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si no tiene ninguna.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el diálogo de Canales de Memoria.
2. Localice la memoria que desea. Utilice el campo `Search:` para filtrar por nombre, o use el cuadro combinado `Profile:` para reducir la lista por perfil.
3. Haga clic en la fila de la tabla de memorias para seleccionarla.
4. Haga clic en `Tune`.

El slice activo se sintoniza a la frecuencia, modo y configuración de filtro almacenados en esa memoria.

**Atajo:** Haga doble clic en cualquier fila de la tabla de memorias para sintonizar inmediatamente sin hacer clic en `Tune`.

## Qué hace cada control

| Control                     | Comportamiento                                                                                                                                                                                                                                                                                                           | Notas                                                                                                                                                   |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Search:`                   | Filtra la tabla de memorias a las filas cuyo nombre coincida con el texto que escribe. Presione Enter o borre el campo para restablecer. Ctrl+F enfoca el campo de búsqueda.                                                                                                                                               | Tiene botón de borrar.                                                                                                                                  |
| `Profile:`                  | Filtra la tabla a las memorias que pertenecen al perfil global o de transmisión seleccionado.                                                                                                                                                                                                                             | Recopila nombres de perfil de los perfiles globales y de transmisión de RadioModel.                                                                      |
| Tabla de memorias           | Muestra y edita filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frecuencia, Nombre, Modo). Columnas: Grupo, Propietario, Frecuencia, Nombre, Modo, Paso, Dirección de desplazamiento TX FM, Desplazamiento de repetidor, Modo de tono, Valor de tono, Silenciador, Nivel de silenciador, Filtro RX Bajo, Filtro RX Alto, Marca RTTY, Desplazamiento RTTY, Desplazamiento DIGL, Desplazamiento DIGU. | Selección extendida; modo de edición en línea mediante el botón Editar o F2/Ctrl+E. Suprimir/Retroceso elimina las filas seleccionadas. Doble clic sintoniza. Ctrl+Shift+A selecciona todo. |
| `Import...`                 | Importa memorias desde un archivo CSV con un diálogo de progreso.                                                                                                                                                                                                                                                        | Muestra el progreso de la importación y un resumen con las filas omitidas.                                                                               |
| `Export...`                 | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                                                                                                                                                                                                                                   | Valida el CSV generado antes de guardarlo.                                                                                                               |
| `Add`                       | Crea una nueva memoria a partir del slice activo actual. Atajo de Ctrl+N.                                                                                                                                                                                                                                                 | Sin selección por letra; siempre apunta al slice activo.                                                                                                 |
| `Edit`                      | Entra en modo de edición en línea en el campo Nombre de la memoria seleccionada. F2 o Ctrl+E también activan la edición.                                                                                                                                                                                                  | Solo se habilita cuando está seleccionada exactamente una memoria.                                                                                      |
| `Tune`                      | Sintoniza el slice activo a la memoria seleccionada. Requiere que esté seleccionada exactamente una fila.                                                                                                                                                                                                                |                                                                                                                                                         |
| `Select All`                | Selecciona todas las filas visibles (respetando la búsqueda/filtro). Atajo de Ctrl+Shift+A.                                                                                                                                                                                                                                |                                                                                                                                                         |
| `Remove`                    | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para la eliminación por lotes. La tecla Suprimir/Retroceso también lo activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay más de 1 fila seleccionada.                                                                               |                                                                                                                                                         |
| Barra de título — Memory Channels | Barra de título sin marco con degradado de 18 px, con un ícono de agarre a la izquierda y el título del diálogo. La posición y el tamaño de la ventana se guardan y restauran automáticamente entre sesiones.                                                                                                                | Utiliza la clase base `PersistentDialog`. La geometría del diálogo se guarda bajo la clave de configuración `MemoryDialogGeometry`.                       |
| — (Minimizar)               | Minimiza el diálogo.                                                                                                                                                                                                                                                                                                     |                                                                                                                                                         |
| □ (Maximizar)               | Maximiza o restaura el diálogo.                                                                                                                                                                                                                                                                                           |                                                                                                                                                         |
| × (Cerrar)                  | Cierra el diálogo. Escape primero borra la búsqueda, luego cierra.                                                                                                                                                                                                                                                        |                                                                                                                                                         |
| Arrastrar para mover        | Haga clic y arrastre la barra de título para mover el diálogo.                                                                                                                                                                                                                                                            | Haga doble clic en la barra de título para alternar entre maximizar y restaurar.                                                                        |
| Recuento de selección       | Muestra '<N> of <M> selected'.                                                                                                                                                                                                                                                                                           |                                                                                                                                                         |

## Consejos

- Si no ve la memoria que desea, verifique si `Profile:` está configurado en un filtro que la excluya. Configure `Profile:` para mostrar todas las entradas.
- En Linux y Windows, mantenga presionada la tecla Ctrl y haga clic para seleccionar filas individuales sin deseleccionar otras. En macOS, use Comando-clic. Solo se utiliza la primera memoria seleccionada cuando hace clic en `Tune`.
- Use el botón `Add` o Ctrl+N para almacenar rápidamente la frecuencia del slice actual como una nueva memoria.
- Use los botones `Import...` y `Export...` para transferir memorias entre radios o compartirlas con otros operadores.
- El diálogo recuerda su posición y tamaño entre sesiones — no necesita reposicionarlo cada vez que lo abre.

## Solución de problemas

- **`Tune` no tiene efecto o está deshabilitado** — Confirme que una sola fila está seleccionada en la tabla de memorias y que AetherSDR está conectado a la radio.
- **La memoria que desea no aparece en la tabla** — El filtro `Search:` o `Profile:` puede estar ocultándola. Borre el campo `Search:` y configure `Profile:` para mostrar todas las entradas.
- **No se puede añadir una memoria** — Asegúrese de que la radio esté conectada y que haya un slice activo disponible.
- **La posición del diálogo se restablece inesperadamente** — La geometría se guarda cuando cierra el diálogo. Si otra ventana o la configuración de la pantalla cambió, la posición guardada puede ser inválida. Reposicione y cierre el diálogo para guardar la nueva ubicación.

## Relacionados

- [Añadir una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Recuperar una memoria de repetidor FM y restaurar el desplazamiento y el tono CTCSS](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Resumen de Canales de Memoria](overview.md)
