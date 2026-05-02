# Borrar todos los spots del panadapter

Elimine todos los spots que se muestran actualmente en el panadapter en una sola acción. Use esto cuando la pantalla esté saturada y desee comenzar de cero sin desconectar ninguna fuente de spots.

## Antes de comenzar

- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe haber entregado spots; de lo contrario, no hay nada que borrar.
- Los spots continúan llegando desde cualquier fuente conectada o activa inmediatamente después de borrar, por lo que las fuentes permanecen activas.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Haga clic en `Clear All Spots`.

Todos los spots se eliminan del panadapter y de la lista de spots al instante. Las fuentes conectadas no se desconectan y continuarán entregando nuevos spots.

## Consejos

- Para eliminar spots banda por banda en lugar de todos a la vez, use la pestaña `Spot List`. Active o desactive bandas individuales en `Bands:` para ocultar los spots de una banda específica sin descartarlos de forma permanente.
- Para borrar solo la tabla de la lista de spots, vaya a la pestaña `Spot List` y haga clic en `Clear`. Esto vacía la visualización de la tabla, pero el efecto sobre la superposición del panadapter sigue los mismos datos de spots en tiempo real.
- Si los spots reaparecen de inmediato y desea mantener la pantalla limpia por más tiempo, reduzca `Spot Lifetime:` en la pestaña `Display` (`SpotsLifetime`) o desconecte la fuente correspondiente antes de borrar.

## Cambio en el valor predeterminado de Auto Mode

A partir de la versión v0.9.5.1, `Auto Mode:` (`SpotAutoSwitchMode`) está habilitado por defecto (**Enabled**). En versiones anteriores, el valor predeterminado era Disabled. Si no ha guardado previamente esta configuración, AetherSDR cambiará automáticamente el modo del radio al hacer clic en un spot en el panadapter. Para desactivar esto, abra la pestaña `Display` y haga clic en `Auto Mode:` para establecerlo en Disabled.

## Reporte a FreeDV Reporter

La pestaña FreeDV incluye una sección **Station Reporting** que permite a AetherSDR transmitir su actividad al mapa público de FreeDV Reporter en `qso.freedv.org` cuando el módem RADE está activo.

### Habilitar el reporte

1. Abra `Settings > SpotHub...` y haga clic en la pestaña `FreeDV`.
2. En el grupo **Station Reporting**, ingrese su indicativo y cuadrado de cuadrícula (consulte los campos a continuación).
3. Active `Enable FreeDV Reporter reporting when RADE is active`.

Si el indicativo o el cuadrado de cuadrícula está vacío al activar la casilla, AetherSDR mostrará una advertencia y dejará el reporte deshabilitado. Ambos campos deben contener un valor antes de que se pueda activar el reporte. Esta validación evita que datos vacíos o de marcador de posición aparezcan en el mapa público compartido.

La configuración se guarda como `FreeDvAutoReport`.

### Campos de Station Reporting

| Campo | Clave de configuración | Descripción |
|---|---|---|
| `Callsign:` | `FreeDvMyCallsign` | Indicativo reportado al mapa de FreeDV Reporter. El campo es de solo lectura cuando `Use radio` está activado. |
| `Use radio` | `FreeDvUseRadioCallsign` | Completa automáticamente el indicativo a partir del indicativo configurado en el radio y bloquea el campo. Habilitado por defecto. Cuando el indicativo se modifica posteriormente en Radio Setup, el campo se actualiza automáticamente. |
| `Grid Square:` | `FreeDvMyGrid` | Cuadrado de cuadrícula Maidenhead (hasta 6 caracteres) reportado al mapa. El campo es de solo lectura cuando `Use GPS` está activado. |
| `Use GPS` | `FreeDvUseGpsGrid` | Completa automáticamente la cuadrícula a partir del módulo GPS del radio y bloquea el campo. Solo se muestra en modelos de radio que tienen hardware GPS. Habilitado por defecto. |
| `Station Msg:` | `FreeDvMyMessage` | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público. |

### Cómo AetherSDR determina el indicativo y la cuadrícula

Al habilitar el reporte, AetherSDR determina el indicativo y el cuadrado de cuadrícula efectivos en este orden:

1. **Indicativo** — usa el indicativo configurado en el radio si `Use radio` está activado y el radio tiene un indicativo no vacío; de lo contrario, usa el valor escrito en el campo `Callsign:`.
2. **Cuadrado de cuadrícula** — usa la cuadrícula GPS del radio si `Use GPS` está activado, el hardware GPS está presente y el GPS tiene una señal de posición fija; de lo contrario, usa el valor escrito en el campo `Grid Square:`.

Si alguno de los valores resueltos está vacío, la activación de la casilla queda bloqueada y se muestra un cuadro de diálogo de advertencia.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
