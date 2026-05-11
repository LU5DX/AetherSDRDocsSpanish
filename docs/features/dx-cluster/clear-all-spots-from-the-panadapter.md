# Eliminar todas las marcas del panadapter

Elimine todas las marcas que se muestran actualmente en el panadapter con una sola acción. Use esta función cuando la pantalla esté abarrotada y desee empezar de nuevo sin desconectar ninguna fuente de marcas.

## Antes de comenzar

- Al menos una fuente de marcas (DX cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe haber entregado marcas; de lo contrario, no hay nada que eliminar.
- Las marcas continúan llegando desde cualquier fuente conectada o en ejecución inmediatamente después de eliminar, por lo que las fuentes permanecen activas.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Haga clic en `Clear All Spots`.

Todas las marcas se eliminan del panadapter y de la lista de marcas al instante. Las fuentes conectadas no se desconectan y seguirán entregando nuevas marcas.

## Consejos
- Para eliminar marcas por banda en lugar de todas a la vez, use la pestaña `Spot List`. Marque o desmarque bandas individuales en `Bands:` para ocultar marcas de una banda específica sin descartarlas permanentemente.
- Para eliminar solo la tabla de la lista de marcas, vaya a la pestaña `Spot List` y haga clic en `Clear`. Esto vacía la visualización de la tabla, pero el efecto en la superposición del panadapter sigue los mismos datos de marcas en vivo.
- Si las marcas reaparecen inmediatamente y desea una pizarra limpia por más tiempo, reduzca `Spot Lifetime:` en la pestaña `Display` (`DxClusterSpotLifetimeSec`) o desconecte la fuente relevante antes de eliminar.
- `Auto:` ahora está habilitado de forma predeterminada. Cuando hace doble clic en una marca que incluye información de modo (por ejemplo, CW, FT8, RTTY), el modo del slice cambia automáticamente a menos que deshabilite esta opción.

## Cambio predeterminado de Auto:

A partir de la v0.9.5.1, `Auto:` (`SpotAutoSwitchMode`) tiene como valor predeterminado **Habilitado**. En versiones anteriores, el valor predeterminado era Deshabilitado. Si no ha guardado previamente esta configuración, AetherSDR ahora cambiará automáticamente el modo de la radio cuando haga clic en una marca en el panadapter. Para desactivar esto, abra la pestaña `Display` y haga clic en `Auto:` para establecerlo en Deshabilitado.

## Líneas de marcas

A partir de la v0.9.7, la pestaña `Display` incluye una opción `Spot Lines:` (clave de configuración `IsSpotsLinesEnabled`). Cuando está habilitada, AetherSDR dibuja una línea vertical desde el espectro hasta cada etiqueta de marca para que la frecuencia exacta sea fácil de leer. La opción tiene como valor predeterminado **Habilitado**.

Deshabilite `Spot Lines:` durante concursos o cuando la banda esté ocupada para reducir el desorden visual en el panadapter.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña `Display`.
2. Haga clic en `Spot Lines:` para alternar entre **Habilitado** y **Deshabilitado**.

El cambio se aplica inmediatamente en el panadapter sin necesidad de reiniciar ninguna fuente de marcas.

## Sintonizar una marca haciendo doble clic en la lista de marcas

Al hacer doble clic en una fila de la tabla de marcas en la pestaña `Spot List`, se sintoniza el slice activo a la frecuencia de la marca. A partir de la v0.9.7, AetherSDR también lee cualquier información de modo incrustada en el comentario de la marca y la reenvía junto con la frecuencia. Si se encuentra un modo reconocible (como CW, FT8 o SSB) en el comentario, y `Auto:` está habilitado en la pestaña `Display`, el modo del slice cambia automáticamente para coincidir con la marca.

No se requiere configuración adicional. El comportamiento se activa cada vez que hace doble clic en una fila de marcas.

## Ventana de SpotHub y modo sin marco

A partir de la v26.5.1, el diálogo de SpotHub utiliza una barra de título de ventana sin marco. Esto proporciona una apariencia más limpia y consistente con otras ventanas de AetherSDR. La ventana admite redimensionamiento de 8 ejes cuando el modo sin marco está activo.

El modo sin marco se controla globalmente mediante la configuración `FramelessWindow` (predeterminado: `True`). Cuando está habilitado, la ventana muestra una barra de título personalizada con controles de ventana. Cuando está deshabilitado, la ventana utiliza la barra de título estándar del sistema operativo.

### Pasos para alternar el modo sin marco

1. Abra `Settings > AetherSDR Settings...`.
2. Navegue a la sección `Appearance` o `General`.
3. Alterne `Frameless Window` según lo desee.

La ventana de SpotHub respeta la configuración global y se actualiza automáticamente.

## Marcadores de Historial de Señal y QRM

A partir de la v26.5.1, la pestaña Display incluye dos nuevas opciones para la visualización del Historial de Señal:

- **Signals** (`SHistoryMarkersEnabled`): Muestra marcadores dorados en el panadapter para señales de ancho de voz detectadas. Esta opción es la misma que `View > Signal History Markers`.
- **QRM** (`SHistoryQrmEnabled`): Muestra marcadores rojos para portadoras estrechas persistentes e interferencia de banda ancha. Esta opción es la misma que `View > QRM History Markers`.

Ambas opciones tienen como valor predeterminado **Deshabilitado**.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña `Display`.
2. Haga clic en `Signals:` o `QRM:` para activar o desactivar cada tipo de marcador.

Los marcadores aparecen y desaparecen inmediatamente en el panadapter.

### Ajustes del Historial de Señal

Debajo de las opciones de marcadores, la sección Historial de Señal proporciona controles de ajuste:

| Control | Clave de Configuración | Predeterminado | Rango | Comportamiento |
|---------|------------------------|----------------|-------|----------------|
| Marker Lifetime: | `SHistoryLifetimeS` | 60 | 15-300 seg | Cuánto tiempo persiste un marcador de Historial de Señal inactivo antes de ser eliminado. |
| QRM Gate: | `SHistoryQrmGateS` | 6 | 3-30 seg | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM. |
| Edge Threshold: | `SHistorySoftEdgeDb` | 3.0 | 1.0-10.0 dB | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History. Más bajo = más cerca de la portadora pero más sensible al ruido. |

### Colores del Historial de Señal

Dos selectores de color están disponibles en la sección Historial de Señal:

- **Signals** (`SHistoryColorSignals`, predeterminado `#FFC800`): Color dorado para marcadores de señal de voz.
- **QRM** (`SHistoryColorQrm`, predeterminado `#FF0000`): Color rojo para marcadores de QRM.

Haga clic en cada muestra de color para abrir un selector de color y elegir un color personalizado.

### Snap to Step

`Snap to Step:` (`SHistorySnapToStep`) redondea la frecuencia de clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo. Esto oculta el pequeño desplazamiento de portadora que puede aparecer al hacer clic en un marcador de Historial de Señal. Predeterminado: **Deshabilitado**.

## Botón Clear All

El botón `Clear All` en la pestaña Display elimina todas las marcas DX, la alimentación de memoria, los marcadores de Historial de Señal y los marcadores de QRM del espectro simultáneamente. Esto es útil cuando la pantalla está abarrotada y desea una vista completamente nueva sin reiniciar ninguna fuente de marcas.

## Coloreado por DXCC

A partir de la v26.5.1, la pestaña Display incluye una sección de Coloreado por DXCC en la columna izquierda debajo del divisor.

### Habilitar el Coloreado por DXCC

1. Abra `Settings > SpotHub...` y haga clic en la pestaña `Display`.
2. En la sección de Coloreado por DXCC, haga clic en `DXCC Colors:` (`IsDxccColoringEnabled`) para habilitar o deshabilitar el coloreado de marcas según el estado DXCC.

Cuando está habilitado, las marcas se colorean según si la entidad DXCC es nueva, trabajada en una nueva banda, trabajada en un nuevo modo o ya trabajada completamente.

### Cargar un archivo ADIF

Para impulsar el coloreado por DXCC, cargue un archivo de registro ADIF:

1. Haga clic en `Log File (ADIF):` (`DxccAdifFilePath`).
2. Seleccione un archivo ADIF de su sistema.
3. AetherSDR supervisa automáticamente el archivo en busca de cambios y lo recarga cuando se modifica. No se necesita una opción separada para la recarga automática.

Después de cargar, el indicador `Imported:` muestra el número de QSOs y entidades, por ejemplo: `1200 QSOs / 85 entities`.

### Muestras de color DXCC

Cuatro selectores de color están disponibles para cada categoría de estado DXCC:

| Estado | Clave de Configuración | Descripción |
|--------|------------------------|-------------|
| New DXCC | `DxccColorNewEntity` | Color para entidades aún no trabajadas. |
| New Band | `DxccColorNewBand` | Color para entidades trabajadas en otras bandas pero no en esta. |
| New Mode | `DxccColorNewMode` | Color para entidades trabajadas en otros modos pero no en este. |
| Worked | `DxccColorWorked` | Color para entidades completamente trabajadas. |

Haga clic en cada muestra de color para abrir un selector de color y elegir un color personalizado. Estos reemplazan el esquema de color DXCC fijo anterior.

## Reporte a FreeDV Reporter

La pestaña FreeDV incluye una sección **Station Reporting** que permite a AetherSDR transmitir su actividad al mapa público de FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo.

### Habilitar el reporte

1. Abra `Settings > SpotHub...` y haga clic en la pestaña `FreeDV`.
2. En el grupo **Station Reporting**, complete su indicativo y cuadrícula (consulte los campos a continuación).
3. Marque `Enable FreeDV Reporter reporting when RADE is active`.

Si el indicativo o la cuadrícula están en blanco cuando marca la casilla, AetherSDR mostrará una advertencia y dejará el reporte deshabilitado. Ambos campos deben contener un valor antes de que se pueda activar el reporte. Esta protección evita que aparezcan datos en blanco o de marcador de posición en el mapa público compartido.

La configuración se guarda como `FreeDvAutoReport`.

### Campos de Station Reporting

| Campo | Clave de configuración | Descripción |
|-------|------------------------|-------------|
| `Callsign:` | `FreeDvMyCallsign` | Indicativo reportado al mapa de FreeDV Reporter. El campo es de solo lectura cuando `Use radio` está marcado. |
| `Use radio` | `FreeDvUseRadioCallsign` | Rellena previamente el indicativo desde el indicativo configurado en la radio y bloquea el campo. El valor predeterminado está habilitado. Cuando el indicativo se cambia más tarde en Radio Setup, el campo se actualiza automáticamente. |
| `Grid Square:` | `FreeDvMyGrid` | Cuadrícula Maidenhead (hasta 6 caracteres) reportada al mapa. El campo es de solo lectura cuando `Use GPS` está marcado. |
| `Use GPS` | `FreeDvUseGpsGrid` | Rellena previamente la cuadrícula desde el módulo GPS de la radio y bloquea el campo. Solo se muestra en modelos de radio que tienen hardware GPS. El valor predeterminado está habilitado. |
| `Station Msg:` | `FreeDvMyMessage` | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público. |

### Cómo AetherSDR resuelve el indicativo y la cuadrícula

Cuando habilita el reporte, AetherSDR determina el indicativo y la cuadrícula efectivos en este orden:

1. **Indicativo** — usa el indicativo configurado en la radio si `Use radio` está marcado y la radio tiene un indicativo no vacío; de lo contrario, usa el valor escrito en el campo `Callsign:`.
2. **Cuadrícula** — usa la cuadrícula GPS de la radio si `Use GPS` está marcado, hay hardware GPS presente y el GPS tiene una posición fija; de lo contrario, usa el valor escrito en el campo `Grid Square:`.

Si alguno de los valores resueltos está vacío, se bloquea la activación de la casilla de verificación y se muestra un diálogo de advertencia.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de las marcas](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar una marca haciendo doble clic en la lista de marcas](tune-to-a-spot-by-double-clicking-the-spot-list.md)
