# Sintonizar la radio a una memoria almacenada

Abra el cuadro de diálogo Canales de memoria para encontrar una frecuencia almacenada y enviarla directamente al receptor de slice activo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo Canales de memoria requiere una conexión activa con la radio.
- Debe tener al menos una memoria ya almacenada. Consulte [Añadir una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si no tiene ninguna.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el cuadro de diálogo Canales de memoria.
2. Localice la memoria que desea. Use el campo `Search:` para filtrar por nombre, o use el cuadro combinado `Profile:` para reducir la lista por perfil.
3. Haga clic en la fila de la tabla de memorias para seleccionarla.
4. Haga clic en `Tune`.

El slice activo se sintoniza a la frecuencia, modo y configuración de filtro almacenados en esa memoria.

**Atajo:** Haga doble clic en cualquier fila de la tabla de memorias para sintonizar inmediatamente sin hacer clic en `Tune`.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Search:` | Filtra la tabla de memorias a las filas cuyo nombre coincida con el texto que escribe. Presione Enter o limpie el campo para restablecer. |
| `Profile:` | Filtra la tabla a las memorias que pertenecen al perfil global seleccionado. |
| Tabla de memorias | Muestra todas las memorias almacenadas. Las columnas incluyen Grupo, Propietario, Frecuencia, Nombre, Modo, Paso, Dir. despl. TX FM, Desplazamiento repetidor, Modo tono, Valor tono, Silenciador, Nivel silenciador, Filtro RX Bajo, Filtro RX Alto, Marca RTTY, Desplazamiento RTTY, Despl. DIGL y Despl. DIGU. Haga clic en un encabezado de columna para ordenar por esa columna. |
| `Tune` | Sintoniza el slice activo a la memoria seleccionada. Requiere que exactamente una fila esté seleccionada. |

## Consejos

- Si no puede ver la memoria que desea, verifique si `Profile:` está configurado con un filtro que la excluye. Configure `Profile:` para mostrar todas las entradas.
- En Linux y Windows, mantenga presionada la tecla Ctrl y haga clic para seleccionar filas individuales sin anular la selección de otras. En macOS, use Comando-clic. Solo la primera memoria seleccionada se usa cuando hace clic en `Tune`.

## Solución de problemas

- **`Tune` no tiene efecto o está deshabilitado** — Confirme que una sola fila esté seleccionada en la tabla de memorias y que AetherSDR esté conectado a la radio.
- **La memoria que desea no aparece en la tabla** — El filtro `Search:` o `Profile:` puede estar ocultándola. Limpie el campo `Search:` y configure `Profile:` para mostrar todas las entradas.

## Relacionados

- [Añadir una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Recuperar una memoria de repetidor FM y restaurar el desplazamiento y el tono CTCSS](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Resumen de canales de memoria](overview.md)
