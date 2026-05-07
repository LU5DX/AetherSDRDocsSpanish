# Conectarse a un clúster DX

El diálogo SpotHub de AetherSDR le permite conectarse a un clúster DX por telnet y mostrar los avisos entrantes como superposiciones en el panadapter. Use esta página para realizar su primera conexión y, opcionalmente, reconectarse automáticamente en cada inicio.

## Antes de empezar

- Conozca el nombre del host (o dirección IP) y el puerto telnet del clúster DX que haya elegido (por ejemplo, `dxc.k0xm.net` en el puerto `7373`).
- Conozca el indicativo que usará para iniciar sesión en el clúster.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster**.
3. En el campo **Server:**, escriba el nombre del host o la dirección IP del clúster. Esto se guarda en `ClusterHost`.
4. En el campo **Port:**, establezca el puerto telnet (1–65535). Esto se guarda en `ClusterPort`.
5. En el campo **Callsign:**, escriba su indicativo. Esto se guarda en `ClusterCallsign`.
6. Haga clic en **Connect**.
   - El indicador de estado cambia a **Connected** y la etiqueta del botón cambia a **Disconnect**.
   - El tráfico entrante del clúster aparece en la pantalla de solo lectura **Cluster Console**.
7. Para reconectarse automáticamente cada vez que se inicie AetherSDR, active **Auto-connect on startup**. Esto se guarda en `ClusterAutoConnect`.

## Qué hace cada control

| Control                                                               | Descripción                                                                                                                                                                                                                                         | Clave de configuración |
|-----------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| **Server:**                                                           | Nombre del host o dirección IP del servidor telnet del clúster DX.                                                                                                                                                                                  | `ClusterHost`          |
| **Port:**                                                             | Puerto telnet. Rango válido: 1–65535.                                                                                                                                                                                                               | `ClusterPort`          |
| **Callsign:**                                                         | Indicativo de inicio de sesión enviado al clúster al conectarse.                                                                                                                                                                                    | `ClusterCallsign`      |
| **Connect / Disconnect**                                              | Activa o desactiva la conexión telnet. La etiqueta muestra la acción actual.                                                                                                                                                                        | —                      |
| **Auto-connect on startup**                                           | Se conecta al clúster automáticamente cuando AetherSDR se inicia.                                                                                                                                                                                   | `ClusterAutoConnect`   |
| **Cluster Console**                                                   | Pantalla de solo lectura del tráfico telnet sin procesar del clúster.                                                                                                                                                                               | —                      |
| **Send** (línea de comandos)                                          | Envía un comando escrito al clúster mientras está conectado.                                                                                                                                                                                        | —                      |
| **Spot Color:**                                                       | Abre un selector de color para las superposiciones de avisos del clúster en el panadapter.                                                                                                                                                          | `ClusterSpotColor`     |
| **Auto Mode:**                                                        | Cambia automáticamente el modo del slice al hacer clic en un aviso que incluye información de modo (p. ej., CW, FT8, RTTY). Activado por defecto.                                                                                                  | `SpotsAutoMode`        |
| **Spot Lines:**                                                       | Dibuja líneas verticales desde el espectro hasta cada etiqueta de aviso. Desactívelo durante concursos para reducir el desorden visual. Nuevo en v0.9.7.                                                                                            | `IsSpotsLinesEnabled`  |
| **Enable FreeDV Reporter reporting when RADE is active**              | Activa el informe de estación al mapa público de FreeDV Reporter (qso.freedv.org) cuando el módem RADE esté activo. Requiere un indicativo y un cuadrado de cuadrícula válidos; la casilla de verificación se niega a activarse y muestra una advertencia si algún campo está vacío o no se puede resolver. | `FreeDvAutoReport`     |
| **Callsign:** (FreeDV Reporter)                                       | Indicativo para informar al mapa de FreeDV Reporter. Solo lectura cuando **Use radio** está marcado. Se actualiza automáticamente si el indicativo configurado de la radio cambia mientras **Use radio** está marcado.                              | `FreeDvMyCallsign`     |
| **Use radio** (indicativo)                                            | Rellena previamente el campo de indicativo desde el indicativo configurado de la radio y bloquea el campo como solo lectura. Activado por defecto.                                                                                                 | `FreeDvUseRadioCallsign`|
| **Grid Square:** (FreeDV Reporter)                                    | Cuadrado de cuadrícula Maidenhead para informar (hasta seis caracteres). Solo lectura cuando **Use GPS** está marcado.                                                                                                                              | `FreeDvMyGrid`         |
| **Use GPS** (cuadrícula)                                              | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS.                                                                       | `FreeDvUseGpsGrid`     |
| **Station Msg:** (FreeDV Reporter)                                    | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter.                                                                                                                                           | `FreeDvMyMessage`      |
| **Total Spots:**                                                      | Lectura en vivo de cuántos avisos se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o borran avisos. Se restablece a 0 cuando se presiona **Clear All Spots**.                                                    | —                      |

## Sintonizar un aviso haciendo doble clic

Al hacer doble clic en una fila de la pestaña **Spot List**, se sintoniza el slice activo en la frecuencia del aviso. A partir de v0.9.7, AetherSDR también reenvía la información de modo extraída del comentario del aviso, por lo que el slice cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el aviso, en lugar de solo cambiar la frecuencia.

## Informes de FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org mientras el módem RADE esté activo.

### Requisitos

- La pestaña FreeDV y todos los controles de informe solo están presentes en las compilaciones realizadas con `HAVE_WEBSOCKETS`. En Windows, la casilla **Enable FreeDV Reporter reporting when RADE is active** requiere adicionalmente `HAVE_RADE`.
- Tanto un indicativo como un cuadrado de cuadrícula deben ser resolubles antes de que se pueda activar el informe. Si alguno está vacío cuando marca **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra un diálogo de advertencia y deja la casilla sin marcar.

### Configuración de informes

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme o ingrese su indicativo:
   - Si **Use radio** está marcado (por defecto), el campo **Callsign:** se llena automáticamente desde el indicativo configurado de la radio y es de solo lectura. Desmarque **Use radio** para escribir un indicativo diferente.
3. Confirme o ingrese su cuadrado de cuadrícula:
   - Si **Use GPS** está marcado (por defecto, solo en radios con capacidad GPS), el campo **Grid Square:** se llena desde el GPS de la radio y es de solo lectura. Desmarque **Use GPS** para escribir un cuadrado de cuadrícula manualmente.
4. Opcionalmente, ingrese un mensaje corto en **Station Msg:** para que aparezca junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si tanto el indicativo como la cuadrícula están presentes, el informe se activa y se guarda en `FreeDvAutoReport`.
   - Si falta alguno, aparece un diálogo de advertencia y la casilla permanece sin marcar. Complete el campo faltante e intente nuevamente.

### Controles de informes

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Interruptor principal para informes de mapas públicos. Bloqueado si el indicativo o el cuadrado de cuadrícula están en blanco. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo enviado al mapa de FreeDV Reporter. | `FreeDvMyCallsign` |
| **Use radio** | Copia el indicativo de la radio y bloquea el campo como solo lectura. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Localizador Maidenhead enviado al mapa de FreeDV Reporter. | `FreeDvMyGrid` |
| **Use GPS** | Copia la cuadrícula del GPS de la radio y bloquea el campo como solo lectura. Visible solo en modelos de radio con capacidad GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Línea de estado de texto libre opcional que se muestra en el mapa público. | `FreeDvMyMessage` |

## Pestaña Display: cambio del valor predeterminado de Auto Mode

A partir de v0.9.5.1, la opción **Auto Mode:** tiene como valor predeterminado **Enabled**. En versiones anteriores, el valor predeterminado era **Disabled**. `SpotsAutoMode` se guarda como `True` a menos que lo haya establecido de otra manera anteriormente. Si prefería el comportamiento anterior, abra la pestaña **Display** y desactive **Auto Mode:**.

## Pestaña Display: Spot Lines (nuevo en v0.9.7)

La opción **Spot Lines:** en la pestaña **Display** controla si AetherSDR dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de aviso en el panadapter. El interruptor tiene como valor predeterminado **Enabled** y se guarda en `IsSpotsLinesEnabled`.

Desactive **Spot Lines:** durante concursos o cuando el panadapter esté muy poblado de avisos para reducir el desorden visual.

## Consejos

- Mientras esté conectado, escriba un comando del clúster en el campo junto a **Send** y haga clic en **Send** para interactuar directamente con el clúster (por ejemplo, `set/dx` o `sh/dx 20`).
- Las superposiciones de avisos aparecen en el panadapter solo cuando el interruptor principal **Spots:** en la pestaña **Display** está activado (predeterminado: Enabled, guardado en `IsSpotsEnabled`).
- Para revisar el tráfico reciente del clúster anterior a abrir SpotHub, desplácese hacia arriba en **Cluster Console** — AetherSDR carga hasta las últimas 500 líneas del archivo de registro del clúster cuando se abre el diálogo.
- Si el indicativo de su radio cambia en Radio Setup mientras **Use radio** está marcado, el campo **Callsign:** en la sección FreeDV Reporter se actualiza automáticamente.
- **Auto Mode** tiene el valor predeterminado Enabled. Cuando hace doble clic en un aviso que contiene información de modo (p. ej., CW, FT8, RTTY), AetherSDR cambia automáticamente el slice a ese modo. A partir de v0.9.7, la información de modo se analiza del comentario del aviso mediante un resolvedor compartido, por lo que la detección de modo es consistente en todas las fuentes de avisos.
- Desactive **Spot Lines:** en la pestaña **Display** durante concursos para reducir el desorden del panadapter mientras mantiene visibles las etiquetas de los avisos.

## Solución de problemas

- **El estado muestra "Error: ..."** — El nombre del host o el puerto son incorrectos, o el servidor del clúster es inalcanzable. Verifique la dirección y el puerto, luego haga clic en **Connect** nuevamente.
- **Cluster Console está vacía después de conectar** — Algunos clústeres requieren que envíe su indicativo como primer comando. Escriba su indicativo en el campo de comando y haga clic en **Send**.
- **Los avisos no aparecen en el panadapter** — Abra la pestaña **Display** y confirme que **Spots:** esté activado.
- **Al hacer doble clic en un aviso no cambia el modo** — Confirme que **Auto Mode:** esté activado en la pestaña **Display**. El cambio de modo requiere que el comentario del aviso contenga un token de modo reconocible (p. ej., CW, FT8, SSB).
- **No se puede marcar la casilla Enable FreeDV Reporter reporting when RADE is active** — Un cuadro de diálogo de advertencia explicará que falta el indicativo o el cuadrado de cuadrícula. Complete ambos campos (o active **Use radio** / **Use GPS** para que se llenen automáticamente) e intente nuevamente.
- **La pestaña FreeDV no es visible** — Su compilación de AetherSDR se compiló sin soporte WebSocket (`HAVE_WEBSOCKETS`). Contacte a su proveedor de paquetes para obtener una compilación que incluya las funciones FreeDV.

## Relacionado

- [Información general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectarse a la Reverse Beacon Network](connect-to-the-reverse-beacon-network.md)
- [Sintonizar un aviso haciendo doble clic en la lista de avisos](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de avisos](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los avisos](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Activar el coloreado por DXCC desde un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
- [Borrar todos los avisos del panadapter](../../features/dx-cluster/clear-all-spots-from-the-panadapter.md)
<!-- docmesh:llm version=V0.9.7 date=2026-05-03 -->
