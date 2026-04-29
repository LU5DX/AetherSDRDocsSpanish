# Activar coloración DXCC desde un registro ADIF

La coloración DXCC permite que AetherSDR marque los spots del panadapter según si la entidad DX ha sido trabajada, confirmada o sigue siendo necesaria, basándose en los contactos de su archivo de registro ADIF. Esto le ayuda a distinguir rápidamente las entidades nuevas de las que ya ha registrado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un equipo de radio para configurar esta función.
- Necesita un archivo de registro ADIF exportado desde su software de registro. El archivo debe usar el formato estándar `.adi` o `.adif`.
- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, POTA, etc.) debe estar activa para que los spots aparezcan en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en el botón de alternancia **DXCC Coloring** para activarlo. El botón habilita la coloración DXCC (`DxccColoringEnabled`).
4. Haga clic en **Log File (ADIF):** para abrir un selector de archivos. Seleccione su archivo de registro ADIF. La ruta se almacena en `DxccAdifPath`.
5. Confirme que el indicador de estadísticas DXCC se actualiza para mostrar el número de QSOs importados desde el archivo.
6. Si su software de registro actualiza el archivo ADIF mientras AetherSDR está en ejecución y desea que los spots reflejen los nuevos contactos automáticamente, active **Auto-Reload Log:** (`DxccAutoReload`).

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **DXCC Coloring** | Interruptor principal. Colorea los spots del panadapter según el estado DXCC: trabajado, confirmado o necesario. | `DxccColoringEnabled` |
| **Log File (ADIF):** | Abre un selector de archivos. El archivo ADIF seleccionado se lee para determinar el estado DXCC. | `DxccAdifPath` |
| **Auto-Reload Log:** | Cuando está activo, vuelve a leer el archivo ADIF cada vez que cambia en el disco. | `DxccAutoReload` |

## Consejos

- El indicador de estadísticas DXCC en el diálogo muestra cuántos QSOs se importaron desde el archivo ADIF. Si muestra cero después de cargarlo, verifique que el archivo sea un ADIF válido.
- El botón **Log File (ADIF):** almacena la ruta de forma persistente. No es necesario volver a seleccionar el archivo después de reiniciar AetherSDR.
- Activar **Auto-Reload Log:** elimina la necesidad de reabrir el diálogo después de registrar un nuevo contacto: los colores de los spots en el panadapter se actualizan en cuanto su software de registro escribe en el archivo.
- La coloración DXCC es independiente de los colores de spots por fuente. Si **Override Colors:** también está activo, consulte [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md) para conocer cómo interactúan esas configuraciones.

## Solución de problemas

- **Las estadísticas DXCC muestran 0 QSOs después de seleccionar un archivo** — Es posible que el archivo no sea un ADIF válido, esté vacío o use una codificación que AetherSDR no pueda leer. Exporte un ADIF nuevo desde su software de registro e inténtelo de nuevo.
- **Los colores de los spots no cambian después de activar DXCC Coloring** — Confirme que el interruptor **Spots:** en la pestaña **Display** está habilitado (`IsSpotsEnabled`). Verifique también que **Override Colors:** (`IsSpotsOverrideColorsEnabled`) no esté activo, ya que fuerza un único color para todos los spots independientemente del estado DXCC.
- **Los nuevos contactos no se reflejan en los spots** — Active **Auto-Reload Log:** para que AetherSDR detecte los cambios en el archivo, o vuelva a seleccionar manualmente el archivo de registro con **Log File (ADIF):** para forzar una nueva importación.

## Relacionados

- [Recarga automática del registro ADIF cuando lo actualiza un software de registro](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Descripción general de SpotHub](overview.md)
