# Borrar todos los spots del panadapter

Elimina todos los spots que se muestran actualmente en el panadapter en una sola acción. Úsalo cuando la pantalla esté saturada y quieras empezar de nuevo sin desconectar ninguna fuente de spots.

## Antes de comenzar

- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe haber entregado spots; de lo contrario, no hay nada que borrar.
- Los spots continúan llegando desde cualquier fuente conectada o activa inmediatamente después de limpiar, por lo que las fuentes permanecen activas.

## Pasos

1. Abre `Settings > SpotHub...`.
2. Haz clic en la pestaña `Display`.
3. Haz clic en `Clear All Spots`.

Todos los spots se eliminan del panadapter y de la lista de spots al instante. Las fuentes conectadas no se desconectan y continuarán entregando nuevos spots.

## Consejos

- Para eliminar spots banda por banda en lugar de todos a la vez, usa la pestaña `Spot List`. Marca o desmarca bandas individuales bajo `Bands:` para ocultar spots de una banda específica sin descartarlos permanentemente.
- Para borrar solo la tabla de la lista de spots, ve a la pestaña `Spot List` y haz clic en `Clear`. Esto vacía la visualización de la tabla, pero el efecto en la superposición del panadapter sigue los mismos datos de spots en vivo.
- Si los spots reaparecen inmediatamente y deseas una pantalla limpia por más tiempo, reduce `Spot Lifetime:` en la pestaña `Display` (`SpotsLifetime`) o desconecta la fuente correspondiente antes de limpiar.

## Reporte de FreeDV Reporter

La pestaña FreeDV incluye una sección **Station Reporting** que permite que AetherSDR transmita tu actividad al mapa público de FreeDV Reporter en `qso.freedv.org` cuando el módem RADE está activo.

### Habilitación del reporte

1. Abre `Settings > SpotHub...` y haz clic en la pestaña `FreeDV`.
2. En el grupo **Station Reporting**, completa tu indicativo y cuadrícula Maidenhead (consulta los campos a continuación).
3. Marca `Enable FreeDV Reporter reporting when RADE is active`.

Si el indicativo o la cuadrícula están en blanco cuando marques la casilla, AetherSDR mostrará una advertencia y dejará el reporte deshabilitado. Ambos campos deben contener un valor antes de que se pueda activar el reporte. Esta protección evita que datos en blanco o de marcador de posición aparezcan en el mapa público compartido.

La configuración se guarda como `FreeDvAutoReport`.

### Campos de Station Reporting

| Campo | Clave de configuración | Descripción |
|---|---|---|
| `Callsign:` | `FreeDvMyCallsign` | Indicativo reportado al mapa de FreeDV Reporter. El campo es de solo lectura cuando se marca `Use radio`. |
| `Use radio` | `FreeDvUseRadioCallsign` | Rellena previamente el indicativo desde el indicativo configurado de la radio y bloquea el campo. Habilitado por defecto. Cuando el indicativo se cambia posteriormente en Radio Setup, el campo se actualiza automáticamente. |
| `Grid Square:` | `FreeDvMyGrid` | Cuadrícula Maidenhead (hasta 6 caracteres) reportada al mapa. El campo es de solo lectura cuando se marca `Use GPS`. |
| `Use GPS` | `FreeDvUseGpsGrid` | Rellena previamente la cuadrícula desde el módulo GPS de la radio y bloquea el campo. Solo se muestra en modelos de radio que tienen hardware GPS. Habilitado por defecto. |
| `Station Msg:` | `FreeDvMyMessage` | Mensaje de texto libre opcional que se muestra junto a tu indicativo en el mapa público. |

### Cómo AetherSDR resuelve el indicativo y la cuadrícula

Cuando habilitas el reporte, AetherSDR determina el indicativo y la cuadrícula efectivos en este orden:

1. **Indicativo** — utiliza el indicativo configurado de la radio si `Use radio` está marcado y la radio tiene un indicativo no vacío; de lo contrario, utiliza el valor escrito en el campo `Callsign:`.
2. **Cuadrícula** — utiliza la cuadrícula GPS de la radio si `Use GPS` está marcado, el hardware GPS está presente y el GPS tiene una posición; de lo contrario, utiliza el valor escrito en el campo `Grid Square:`.

Si algún valor resuelto está vacío, se bloquea la habilitación de la casilla y se muestra un diálogo de advertencia.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Ajusta la densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintoniza un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
