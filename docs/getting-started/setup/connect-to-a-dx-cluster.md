# Conectarse a un clúster DX

El diálogo SpotHub de AetherSDR permite conectarse a un clúster DX por telnet y mostrar los spots entrantes como superposiciones en el panadapter. Use esta página para realizar su primera conexión y, opcionalmente, reconectarse de forma automática en cada inicio.

## Antes de comenzar

- Conozca el nombre de host (o dirección IP) y el puerto telnet del clúster DX que desea usar (por ejemplo, `dxc.k0xm.net` en el puerto `7373`).
- Conozca el indicativo con el que iniciará sesión en el clúster.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster**.
3. En el campo **Server:**, escriba el nombre de host o la dirección IP del clúster. Esto se guarda en `ClusterHost`.
4. En el campo **Port:**, establezca el puerto telnet (1–65535). Esto se guarda en `ClusterPort`.
5. En el campo **Callsign:**, escriba su indicativo. Esto se guarda en `ClusterCallsign`.
6. Haga clic en **Connect**.
   - El indicador de estado cambia a **Connected** y la etiqueta del botón cambia a **Disconnect**.
   - El tráfico entrante del clúster aparece en la pantalla de solo lectura **Cluster Console**.
7. Para reconectarse automáticamente cada vez que AetherSDR se inicie, active **Auto-connect on startup**. Esto se guarda en `ClusterAutoConnect`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host o dirección IP del servidor telnet del clúster DX. | `ClusterHost` |
| **Port:** | Puerto telnet. Rango válido: 1–65535. | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster al conectarse. | `ClusterCallsign` |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet. La etiqueta muestra la acción actual. | — |
| **Auto-connect on startup** | Conecta al clúster automáticamente cuando AetherSDR se inicia. | `ClusterAutoConnect` |
| **Cluster Console** | Pantalla de solo lectura del tráfico telnet sin procesar del clúster. | — |
| **Send** (línea de comandos) | Envía un comando escrito al clúster mientras está conectado. | — |
| **Spot Color:** | Abre un selector de color para las superposiciones de spots del clúster en el panadapter. | `ClusterSpotColor` |
| **Enable FreeDV Reporter reporting when RADE is active** | Activa el reporte de la estación al mapa público FreeDV Reporter (qso.freedv.org) cuando el módem RADE está activo. Requiere un indicativo y un localizador de cuadrícula válidos; la casilla no se puede activar y muestra una advertencia si alguno de los campos está en blanco o no se puede resolver. | `FreeDvAutoReport` |
| **Callsign:** (FreeDV Reporter) | Indicativo que se reporta al mapa FreeDV Reporter. Es de solo lectura cuando **Use radio** está marcado. Se actualiza automáticamente si el indicativo configurado en el equipo cambia mientras **Use radio** está marcado. | `FreeDvMyCallsign` |
| **Use radio** (indicativo) | Rellena el campo del indicativo con el indicativo configurado en el equipo y bloquea el campo como de solo lectura. Activado por defecto. | `FreeDvUseRadioCallsign` |
| **Grid Square:** (FreeDV Reporter) | Localizador Maidenhead que se reporta (hasta seis caracteres). Es de solo lectura cuando **Use GPS** está marcado. | `FreeDvMyGrid` |
| **Use GPS** (cuadrícula) | Rellena el campo de cuadrícula con los datos del módulo GPS del equipo y bloquea el campo como de solo lectura. Solo se muestra en modelos de equipo que disponen de hardware GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** (FreeDV Reporter) | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público FreeDV Reporter. | `FreeDvMyMessage` |

## Reporte en FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público FreeDV Reporter en qso.freedv.org mientras el módem RADE está activo.

### Requisitos

- La pestaña FreeDV y todos los controles de reporte solo están presentes en compilaciones compiladas con `HAVE_WEBSOCKETS`. En Windows, la casilla **Enable FreeDV Reporter reporting when RADE is active** también requiere `HAVE_RADE`.
- Tanto el indicativo como el localizador de cuadrícula deben estar disponibles antes de poder activar el reporte. Si alguno está en blanco al marcar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra un diálogo de advertencia y deja la casilla sin marcar.

### Configurar el reporte

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme o ingrese su indicativo:
   - Si **Use radio** está marcado (por defecto), el campo **Callsign:** se rellena automáticamente con el indicativo configurado en el equipo y es de solo lectura. Desmarque **Use radio** para escribir un indicativo diferente.
3. Confirme o ingrese su localizador de cuadrícula:
   - Si **Use GPS** está marcado (por defecto, solo en equipos con GPS), el campo **Grid Square:** se rellena con los datos del GPS del equipo y es de solo lectura. Desmarque **Use GPS** para escribir un localizador manualmente.
4. Opcionalmente, ingrese un mensaje breve en **Station Msg:** para que aparezca junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si tanto el indicativo como el localizador de cuadrícula están presentes, el reporte se activa y se guarda en `FreeDvAutoReport`.
   - Si alguno falta, aparece un diálogo de advertencia y la casilla permanece sin marcar. Complete el campo faltante y vuelva a intentarlo.

### Controles de reporte

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Interruptor principal para el reporte al mapa público. Bloqueado si el indicativo o el localizador de cuadrícula está en blanco. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo enviado al mapa FreeDV Reporter. | `FreeDvMyCallsign` |
| **Use radio** | Copia el indicativo del equipo y bloquea el campo como de solo lectura. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Localizador Maidenhead enviado al mapa FreeDV Reporter. | `FreeDvMyGrid` |
| **Use GPS** | Copia la cuadrícula del GPS del equipo y bloquea el campo como de solo lectura. Solo visible en modelos de equipo con GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Línea de estado de texto libre opcional que se muestra en el mapa público. | `FreeDvMyMessage` |

## Pestaña Display: cambio en el valor predeterminado de Auto Mode

A partir de la v0.9.5.1, el interruptor **Auto Mode:** tiene como valor predeterminado **Enabled**. En versiones anteriores, el valor predeterminado era **Disabled**. `SpotAutoSwitchMode` se guarda como `True` a menos que usted lo haya cambiado previamente. Si prefiere el comportamiento anterior, abra la pestaña **Display** y desactive **Auto Mode:**.

## Consejos

- Mientras está conectado, escriba un comando del clúster en el campo junto a **Send** y haga clic en **Send** para interactuar directamente con el clúster (por ejemplo, `set/dx` o `sh/dx 20`).
- Las superposiciones de spots aparecen en el panadapter solo cuando el interruptor principal **Spots:** en la pestaña **Display** está activado (por defecto: activado, guardado en `IsSpotsEnabled`).
- Para revisar el tráfico reciente del clúster de antes de abrir SpotHub, desplácese hacia arriba en la **Cluster Console** — AetherSDR carga hasta las últimas 500 líneas del archivo de registro del clúster al abrir el diálogo.
- Si el indicativo del equipo cambia en Radio Setup mientras **Use radio** está marcado, el campo **Callsign:** en la sección FreeDV Reporter se actualiza automáticamente.

## Resolución de problemas

- **El estado muestra "Error: ..."** — El nombre de host o el puerto son incorrectos, o el servidor del clúster no es accesible. Verifique la dirección y el puerto, luego haga clic en **Connect** nuevamente.
- **Cluster Console está vacía después de conectarse** — Algunos clústeres requieren que envíe su indicativo como primer comando. Escriba su indicativo en el campo de comandos y haga clic en **Send**.
- **Los spots no aparecen en el panadapter** — Abra la pestaña **Display** y confirme que **Spots:** esté activado.
- **La casilla Enable FreeDV Reporter reporting when RADE is active no se puede marcar** — Un diálogo de advertencia explicará que el indicativo o el localizador de cuadrícula falta. Complete ambos campos (o active **Use radio** / **Use GPS** para que se rellenen automáticamente) y vuelva a intentarlo.
- **La pestaña FreeDV no es visible** — Su compilación de AetherSDR fue compilada sin soporte WebSocket (`HAVE_WEBSOCKETS`). Contacte a su proveedor de paquetes para obtener una compilación que incluya las funciones FreeDV.

## Relacionado

- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectarse a la Red de Balizas Inversas (Reverse Beacon Network)](connect-to-the-reverse-beacon-network.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Ajustar la densidad, posición, tamaño de fuente y tiempo de vida de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Activar el coloreado DXCC desde un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
- [Borrar todos los spots del panadapter](../../features/dx-cluster/clear-all-spots-from-the-panadapter.md)
