# Borrar todos los spots del panadapter

Elimine todos los spots que se muestran actualmente en el panadapter en una sola acción. Utilice esto cuando la pantalla esté saturada y desee empezar de nuevo sin desconectar ninguna fuente de spots.

## Antes de comenzar

- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe haber entregado spots; de lo contrario, no hay nada que borrar.
- Los spots continúan llegando desde cualquier fuente conectada o en ejecución inmediatamente después de borrar, por lo que las fuentes permanecen activas.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Haga clic en `Clear All Spots`.

Todos los spots se eliminan del panadapter y de la lista de spots al instante. Las fuentes conectadas no se desconectan y continuarán entregando nuevos spots.

## Consejos
- Para eliminar spots por banda en lugar de todos a la vez, use la pestaña `Spot List`. Marque o desmarque bandas individuales en `Bands:` para ocultar spots de una banda específica sin descartarlos permanentemente.
- Para borrar solo la tabla de la lista de spots, vaya a la pestaña `Spot List` y haga clic en `Clear`. Esto vacía la visualización de la tabla, pero el efecto en la superposición del panadapter sigue los mismos datos de spots en vivo.
- Si los spots reaparecen inmediatamente y desea un estado limpio por más tiempo, reduzca `Spot Lifetime:` en la pestaña `Display` (`SpotsLifetime`) o desconecte la fuente relevante antes de borrar.
- `Auto Mode:` ahora está habilitado por defecto. Cuando hace doble clic en un spot que incluye información de modo (por ejemplo, CW, FT8, RTTY), el modo del slice cambia automáticamente a menos que desactive esta opción.

## Cambio del valor predeterminado de Auto Mode

A partir de v0.9.5.1, `Auto Mode:` (`SpotAutoSwitchMode`) tiene como valor predeterminado **Enabled**. En versiones anteriores, su valor predeterminado era Disabled. Si no ha guardado previamente esta configuración, AetherSDR ahora cambiará automáticamente el modo de radio cuando haga clic en un spot en el panadapter. Para desactivar esto, abra la pestaña `Display` y haga clic en `Auto Mode:` para establecerlo en Disabled.

## Líneas de spot (Spot Lines)

A partir de v0.9.7, la pestaña `Display` incluye una opción `Spot Lines:` (clave de configuración `IsSpotsLinesEnabled`). Cuando está habilitada, AetherSDR dibuja una línea vertical desde el espectro hasta cada etiqueta de spot para que la frecuencia exacta sea fácil de leer. La opción tiene como valor predeterminado **Enabled**.

Desactive `Spot Lines:` durante concursos o cuando la banda esté ocupada para reducir el desorden visual en el panadapter.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña `Display`.
2. Haga clic en `Spot Lines:` para alternar entre **Enabled** y **Disabled**.

El cambio tiene efecto inmediato en el panadapter sin necesidad de reiniciar ninguna fuente de spots.

## Sintonizar un spot haciendo doble clic en la lista de spots

Hacer doble clic en una fila de la tabla de spots en la pestaña `Spot List` sintoniza el slice activo en la frecuencia del spot. A partir de v0.9.7, AetherSDR también lee cualquier información de modo incrustada en el comentario del spot y la reenvía junto con la frecuencia. Si se encuentra un modo reconocible (como CW, FT8 o SSB) en el comentario, y `Auto Mode:` está habilitado en la pestaña `Display`, el modo del slice cambia para coincidir con el spot automáticamente.

No se requiere configuración adicional. El comportamiento se activa cada vez que hace doble clic en una fila de spot.

## Reporte de FreeDV Reporter

La pestaña FreeDV incluye una sección **Station Reporting** que permite a AetherSDR transmitir su actividad al mapa público de FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo.

### Habilitar el reporte

1. Abra `Settings > SpotHub...` y haga clic en la pestaña `FreeDV`.
2. En el grupo **Station Reporting**, complete su indicativo y su cuadrado de cuadrícula (consulte los campos a continuación).
3. Marque `Enable FreeDV Reporter reporting when RADE is active`.

Si el indicativo o el cuadrado de cuadrícula están en blanco cuando marca la casilla, AetherSDR mostrará una advertencia y dejará el reporte deshabilitado. Ambos campos deben contener un valor antes de que se pueda activar el reporte. Esta protección evita que aparezcan datos en blanco o provisionales en el mapa público compartido.

La configuración se guarda como `FreeDvAutoReport`.

### Campos de Station Reporting

| Campo            | Clave de configuración    | Descripción                                                                                                                                                                                              |
|------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Callsign:`      | `FreeDvMyCallsign`        | Indicativo reportado al mapa de FreeDV Reporter. El campo es de solo lectura cuando `Use radio` está marcado.                                                                                            |
| `Use radio`      | `FreeDvUseRadioCallsign`  | Rellena previamente el indicativo desde el indicativo configurado en la radio y bloquea el campo. El valor predeterminado es habilitado. Cuando el indicativo se cambia posteriormente en Radio Setup, el campo se actualiza automáticamente. |
| `Grid Square:`   | `FreeDvMyGrid`            | Cuadrado de cuadrícula Maidenhead (hasta 6 caracteres) reportado al mapa. El campo es de solo lectura cuando `Use GPS` está marcado.                                                                     |
| `Use GPS`        | `FreeDvUseGpsGrid`        | Rellena previamente la cuadrícula desde el módulo GPS de la radio y bloquea el campo. Solo se muestra en modelos de radio que tienen hardware GPS. El valor predeterminado es habilitado.                 |
| `Station Msg:`   | `FreeDvMyMessage`         | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público.                                                                                                                |

### Cómo resuelve AetherSDR el indicativo y la cuadrícula

Cuando habilita el reporte, AetherSDR determina el indicativo y el cuadrado de cuadrícula efectivos en este orden:

1. **Indicativo** — utiliza el indicativo configurado en la radio si `Use radio` está marcado y la radio tiene un indicativo no vacío; de lo contrario, utiliza el valor escrito en el campo `Callsign:`.
2. **Cuadrado de cuadrícula** — utiliza la cuadrícula GPS de la radio si `Use GPS` está marcado, hay hardware GPS presente y el GPS tiene una posición fija; de lo contrario, utiliza el valor escrito en el campo `Grid Square:`.

Si alguno de los valores resueltos está vacío, se bloquea la activación de la casilla de verificación y se muestra un cuadro de diálogo de advertencia.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y vida útil de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
<!-- docmesh:llm version=V0.9.7 date=2026-05-03 -->
