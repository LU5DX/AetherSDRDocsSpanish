# Conectarse a un clúster DX

El diálogo SpotHub de AetherSDR le permite conectarse a un clúster DX por telnet y mostrar los spots entrantes como superposiciones en el panadapter. Utilice esta página para hacer su primera conexión y opcionalmente reconectarse automáticamente en cada lanzamiento.

## Antes de comenzar

- Conozca el nombre de host (o dirección IP) y el puerto telnet de su clúster DX elegido (por ejemplo, `dxc.k0xm.net` en el puerto `7373`).
- Conozca el indicativo que utilizará para iniciar sesión en el clúster.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster**.
3. En el campo **Server:**, escriba el nombre de host o la dirección IP del clúster. Esto se guarda en `ClusterHost`.
4. En el campo **Port:**, establezca el puerto telnet (1–65535). Esto se guarda en `ClusterPort`.
5. En el campo **Callsign:**, escriba su indicativo. Esto se guarda en `ClusterCallsign`.
6. Haga clic en **Connect**.
   - El indicador de estado cambia a **Connected** y la etiqueta del botón cambia a **Disconnect**.
   - El tráfico entrante del clúster aparece en la pantalla de solo lectura **Cluster Console**.
7. Para reconectarse automáticamente cada vez que se inicia AetherSDR, habilite **Auto-connect on startup**. Esto se guarda en `ClusterAutoConnect`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host o dirección IP del servidor telnet del clúster DX. | `ClusterHost` |
| **Port:** | Puerto telnet. Rango válido: 1–65535. | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster al conectar. | `ClusterCallsign` |
| **Connect / Disconnect** | Alterna la conexión telnet. La etiqueta muestra la acción actual. | — |
| **Auto-connect on startup** | Se conecta al clúster automáticamente cuando se inicia AetherSDR. | `ClusterAutoConnect` |
| **Cluster Console** | Pantalla de solo lectura del tráfico telnet sin procesar del clúster. | — |
| **Send** (línea de comandos) | Envía un comando escrito al clúster mientras está conectado. | — |
| **Spot Color:** | Abre un selector de color para las superposiciones de spots del clúster en el panadapter. | `ClusterSpotColor` |
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de estaciones al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo válido y una casilla de cuadrícula; la casilla se niega a habilitar y muestra una advertencia si alguno de los campos está en blanco o no se puede resolver. | `FreeDvAutoReport` |
| **Callsign:** (FreeDV Reporter) | Indicativo a reportar al mapa de FreeDV Reporter. Solo lectura cuando **Use radio** está marcado. Se actualiza automáticamente si el indicativo configurado de la radio cambia mientras **Use radio** está marcado. | `FreeDvMyCallsign` |
| **Use radio** (indicativo) | Rellena el campo de indicativo con el indicativo configurado de la radio y bloquea el campo como solo lectura. Habilitado de forma predeterminada. | `FreeDvUseRadioCallsign` |
| **Grid Square:** (FreeDV Reporter) | Casilla de cuadrícula Maidenhead a reportar (hasta seis caracteres). Solo lectura cuando **Use GPS** está marcado. | `FreeDvMyGrid` |
| **Use GPS** (cuadrícula) | Rellena el campo de cuadrícula con el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** (FreeDV Reporter) | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

## Reporte de FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org mientras el módem RADE esté activo.

### Requisitos

- La pestaña FreeDV y todos los controles de reporte solo están presentes en compilaciones compiladas con `HAVE_WEBSOCKETS`. En Windows, la casilla **Enable FreeDV Reporter reporting when RADE is active** además requiere `HAVE_RADE`.
- Tanto un indicativo como una casilla de cuadrícula deben ser resolubles antes de que se pueda habilitar el reporte. Si alguno está en blanco cuando marca **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra un diálogo de advertencia y deja la casilla sin marcar.

### Configurar el reporte

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme o ingrese su indicativo:
   - Si **Use radio** está marcado (predeterminado), el campo **Callsign:** se completa automáticamente con el indicativo configurado de la radio y es solo lectura. Desmarque **Use radio** para escribir un indicativo diferente.
3. Confirme o ingrese su casilla de cuadrícula:
   - Si **Use GPS** está marcado (predeterminado, solo radios con GPS), el campo **Grid Square:** se completa con el GPS de la radio y es solo lectura. Desmarque **Use GPS** para escribir una casilla de cuadrícula manualmente.
4. Opcionalmente, ingrese un mensaje corto en **Station Msg:** para que aparezca junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si tanto el indicativo como la casilla de cuadrícula están presentes, el reporte se habilita y se guarda en `FreeDvAutoReport`.
   - Si falta alguno, aparece un diálogo de advertencia y la casilla permanece sin marcar. Complete el campo faltante e intente de nuevo.

### Controles de reporte

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Interruptor maestro para reporte en el mapa público. Bloqueado si el indicativo o la casilla de cuadrícula está en blanco. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo enviado al mapa de FreeDV Reporter. | `FreeDvMyCallsign` |
| **Use radio** | Copia el indicativo de la radio y bloquea el campo como solo lectura. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Localizador Maidenhead enviado al mapa de FreeDV Reporter. | `FreeDvMyGrid` |
| **Use GPS** | Copia la cuadrícula del GPS de la radio y bloquea el campo como solo lectura. Visible solo en modelos de radio con capacidad GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Línea de estado de texto libre opcional que se muestra en el mapa público. | `FreeDvMyMessage` |

## Consejos

- Mientras está conectado, escriba un comando del clúster en el campo junto a **Send** y haga clic en **Send** para interactuar directamente con el clúster (por ejemplo, `set/dx` o `sh/dx 20`).
- Las superposiciones de spots aparecen en el panadapter solo cuando el interruptor maestro **Spots:** en la pestaña **Display** está habilitado (predeterminado: Habilitado, guardado en `IsSpotsEnabled`).
- Para revisar el tráfico reciente del clúster anterior a la apertura de SpotHub, desplácese hacia arriba en **Cluster Console** — AetherSDR carga hasta las últimas 500 líneas del archivo de registro del clúster cuando se abre el diálogo.
- Si el indicativo de su radio cambia en Radio Setup mientras **Use radio** está marcado, el campo **Callsign:** en la sección FreeDV Reporter se actualiza automáticamente.

## Solución de problemas

- **El estado muestra "Error: ..."** — El nombre de host o el puerto es incorrecto, o el servidor del clúster es inaccesible. Verifique la dirección y el puerto, luego haga clic en **Connect** nuevamente.
- **Cluster Console está vacío después de conectar** — Algunos clústeres requieren que envíe su indicativo como el primer comando. Escriba su indicativo en el campo de comandos y haga clic en **Send**.
- **Los spots no aparecen en el panadapter** — Abra la pestaña **Display** y confirme que **Spots:** está habilitado.
- **La casilla Enable FreeDV Reporter reporting when RADE is active no se puede marcar** — Un diálogo de advertencia explicará que falta el indicativo o la casilla de cuadrícula. Complete ambos campos (u habilite **Use radio** / **Use GPS** para que se completen automáticamente) e intente de nuevo.
- **La pestaña FreeDV no es visible** — Su compilación de AetherSDR se compiló sin soporte WebSocket (`HAVE_WEBSOCKETS`). Contacte a su proveedor de paquetes para obtener una compilación que incluya características de FreeDV.

## Relacionado

- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectarse a la Red de Balizas Inversa](connect-to-the-reverse-beacon-network.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Habilitar coloración DXCC desde un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
- [Borrar todos los spots del panadapter](../../features/dx-cluster/clear-all-spots-from-the-panadapter.md)
