# Activar el coloreado DXCC desde un registro ADIF

El coloreado DXCC superpone el estado de trabajado, confirmado y pendiente sobre los spots del panadapter, comparando el indicativo de cada spot con su registro ADIF. Esto permite ver de un vistazo qué estaciones representan nuevas entidades, nuevas combinaciones de banda, o contactos ya realizados.

## Antes de comenzar

- AetherSDR está en ejecución y al menos una fuente de spots está configurada y generando spots. Los spots deben ser visibles en el panadapter para que el coloreado tenga algún efecto visible.
- Tiene un archivo de registro ADIF exportado desde su software de registro y accesible en el sistema de archivos local.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **DXCC Coloring** para activarlo. El interruptor habilita el coloreado de spots basado en DXCC.
4. Haga clic en **Log File (ADIF):** para abrir un explorador de archivos.
5. Navegue hasta su archivo de registro ADIF y selecciónelo. La ruta se guarda en `DxccAdifPath`. El indicador de estadísticas DXCC en el diálogo mostrará el número de QSO importados una vez que se lea el archivo.
6. Si su software de registro actualiza el archivo ADIF mientras AetherSDR está en ejecución, haga clic en **Auto-Reload Log:** para habilitar la recarga automática cuando el archivo cambie. Esto se guarda en `DxccAutoReload`.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **DXCC Coloring** | Interruptor principal. Colorea los spots del panadapter según el estado de trabajado/confirmado/pendiente. | `DxccColoringEnabled` |
| **Log File (ADIF):** | Abre un explorador de archivos para seleccionar el archivo de registro ADIF que controla el coloreado DXCC. | `DxccAdifPath` |
| **Auto-Reload Log:** | Cuando está habilitado, vuelve a leer el archivo ADIF automáticamente cada vez que cambia en el disco. | `DxccAutoReload` |

## Consejos

- El indicador de estadísticas DXCC en el diálogo SpotHub muestra la cantidad de QSO importados desde el archivo ADIF seleccionado. Si el contador muestra cero después de seleccionar un archivo, verifique que el archivo sea una exportación ADIF válida y que no esté vacío.
- Habilite **Auto-Reload Log:** si su software de registro escribe en el archivo ADIF en tiempo real. El coloreado se actualizará en cuestión de segundos después de que se registre un nuevo QSO, sin necesidad de ninguna acción manual.
- El coloreado DXCC se aplica sobre la capa de spots. Asegúrese de que **Spots:** esté configurado como Enabled en la pestaña **Display**; de lo contrario, no aparecerá ningún spot independientemente de la configuración de coloreado.

## Solución de problemas

- **Los spots aparecen pero no muestran coloreado DXCC** — Confirme que **DXCC Coloring** esté activado y que haya una ruta de archivo ADIF válida establecida en **Log File (ADIF):**. Compruebe el indicador de estadísticas DXCC para verificar que el recuento de QSO no sea cero.
- **Las estadísticas DXCC muestran 0 QSO después de cargar un archivo** — Es posible que el archivo no tenga un formato ADIF válido o que esté vacío. Vuelva a exportar desde su software de registro y seleccione el nuevo archivo nuevamente usando **Log File (ADIF):**.
- **El coloreado no se actualiza después de registrar nuevos QSO** — Habilite **Auto-Reload Log:**. Si ya está habilitado, confirme que su software de registro esté escribiendo en la misma ruta de archivo almacenada en `DxccAdifPath`.

## Relacionados

- [Recarga automática del registro ADIF cuando es actualizado por un software de registro](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Seleccionar colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
