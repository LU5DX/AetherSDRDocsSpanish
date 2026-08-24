# Conectarse a un cluster de DX

El diálogo SpotHub de AetherSDR le permite conectarse a un cluster de DX por telnet, a la Reverse Beacon Network, a WSJT-X, a SpotCollector, a POTA, a FreeDV, a EiBi y al N1MM Logger+ Spot Collector, y configurar cómo se muestran los spots entrantes como superposiciones en el panadapter.

## Antes de comenzar

- Conozca el nombre de host (o dirección IP) y el puerto telnet del cluster de DX elegido (por ejemplo, `dxc.k0xm.net` en el puerto `7373`).
- Conozca el indicativo que usará para iniciar sesión en el cluster.

## Abrir SpotHub

1. Abra `Settings > SpotHub...`.

## Pestaña Cluster

### Conectarse a un cluster de DX

1. Haga clic en la pestaña **Cluster**.
2. En el campo **Server:**, escriba el nombre de host o la dirección IP del cluster. Esto se guarda en `ClusterHost`.
3. En el campo **Port:**, establezca el puerto telnet (1–65535). Esto se guarda en `ClusterPort`.
4. En el campo **Callsign:**, escriba su indicativo. Esto se guarda en `ClusterCallsign`.
5. Haga clic en **Connect**.
   - El indicador de estado cambia a **Connected** y la etiqueta del botón cambia a **Disconnect**.
   - El tráfico entrante del cluster aparece en la pantalla de solo lectura **Cluster Console**.
6. Para reconectarse automáticamente cada vez que AetherSDR se inicie, active **Auto-connect on startup**. Esto se guarda en `ClusterAutoConnect`.

### Configurar comandos de inicio para el cluster de DX

Puede configurar una lista de comandos que se envían automáticamente después de cada inicio de sesión en el cluster de DX (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).

1. Haga clic en **Startup Commands…**.
2. En el diálogo, introduzca un comando por línea.
3. Haga clic en **OK** para guardar. Los comandos se almacenan en la configuración `DxClusterStartupCommands` y el cliente los reproduce después de cada inicio de sesión exitoso.

### Qué hace cada control en la pestaña Cluster

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host o dirección IP del servidor telnet del cluster de DX. | `ClusterHost` |
| **Port:** | Puerto telnet. Rango válido: 1–65535. | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al cluster al conectar. | `ClusterCallsign` |
| **Connect / Disconnect** | Alterna la conexión telnet. La etiqueta muestra la acción actual. | — |
| **Auto-connect on startup** | Se conecta al cluster automáticamente cuando AetherSDR se inicia. | `ClusterAutoConnect` |
| **Startup Commands…** | Abre un diálogo para editar los comandos enviados automáticamente después de cada inicio de sesión. Un comando por línea. Nuevo en v26.5.2.1. | `DxClusterStartupCommands` |
| **Cluster Console** | Pantalla de solo lectura del tráfico telnet crudo del cluster. | — |
| **Send** (línea de comandos) | Envía un comando escrito al cluster mientras está conectado. | — |
| **Spot Color:** | Abre un selector de color para las superposiciones de spots del cluster en el panadapter. | `ClusterSpotColor` |

## Pestaña RBN

### Conectarse a la Reverse Beacon Network

1. Haga clic en la pestaña **RBN**.
2. En el campo **Server:**, escriba el nombre de host telnet de RBN. Esto se guarda en `RbnHost`.
3. En el campo **Port:**, establezca el puerto telnet de RBN (1–65535). Esto se guarda en `RbnPort`.
4. En el campo **Callsign:**, escriba su indicativo de inicio de sesión. Esto se guarda en `RbnCallsign`.
5. Establezca **Rate Limit:** para limitar el número de spots de RBN procesados por segundo. Esto se guarda en `RbnRateLimit`.
6. Haga clic en **Connect**.
7. Para reconectarse automáticamente al iniciar, active **Auto-connect on startup**. Esto se guarda en `RbnAutoConnect`.

### Configurar comandos de inicio para RBN

Puede configurar una lista de comandos que se envían automáticamente después de cada inicio de sesión en RBN (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).

1. Haga clic en **Startup Commands…**.
2. En el diálogo, introduzca un comando por línea.
3. Haga clic en **OK** para guardar. Los comandos se almacenan en la configuración `RbnStartupCommands` y el cliente de RBN los reproduce después de cada inicio de sesión exitoso.

### Qué hace cada control en la pestaña RBN

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host telnet de RBN. | `RbnHost` |
| **Port:** | Puerto telnet de RBN. Rango válido: 1–65535. | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión para RBN. | `RbnCallsign` |
| **Rate Limit:** | Limita los spots de RBN por segundo. | `RbnRateLimit` |
| **Connect / Disconnect** | Alterna la conexión RBN. | — |
| **Auto-connect on startup** | Inicia RBN automáticamente al lanzar. | `RbnAutoConnect` |
| **Startup Commands…** | Abre un diálogo para editar los comandos enviados automáticamente después de cada inicio de sesión en RBN. Un comando por línea. Nuevo en v26.5.2.1. | `RbnStartupCommands` |
| **RBN Console** | Consola de solo lectura del tráfico de RBN. | — |
| **Send** | Envía un comando a RBN. | — |
| **Spot Color:** | Selector de color para los spots de RBN. | `RbnSpotColor` |

## Pestaña WSJT-X

### Escuchar spots de WSJT-X

1. Haga clic en la pestaña **WSJT-X**.
2. En el campo **Address:**, introduzca la dirección de enlace UDP para los mensajes de WSJT-X. Esto se guarda en `WsjtxAddress`.
3. En el campo **Port:**, establezca el puerto UDP. Esto se guarda en `WsjtxPort`.
4. Haga clic en **Start** para comenzar a escuchar. El estado cambia a **Listening**.
5. Para iniciar automáticamente al lanzar, active **Auto-start on startup**. Esto se guarda en `WsjtxAutoStart`.

### Filtrar decodificaciones de WSJT-X

Use las casillas de verificación para filtrar qué decodificaciones aparecen como spots:

- **CQ** — Muestra solo llamadas CQ. Se guarda en `WsjtxFilterCQ`.
- **CQ POTA** — Muestra llamadas CQ POTA. Se guarda en `WsjtxFilterPOTA`.
- **Calling Me** — Muestra solo decodificaciones dirigidas a su indicativo. Se guarda en `WsjtxFilterCallingMe`.

### Personalizar colores de spots de WSJT-X

Haga clic en cualquier muestra de color para abrir un selector de color:

- **CQ color** — Se guarda en `WsjtxColorCQ`.
- **POTA color** — Se guarda en `WsjtxColorPOTA`.
- **Calling Me color** — Se guarda en `WsjtxColorCallingMe`.
- **Default color** — Se guarda en `WsjtxColorDefault`.

### Qué hace cada control en la pestaña WSJT-X

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Puerto UDP para WSJT-X. Rango válido: 1–65535. | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el listener UDP. | — |
| **Auto-start on startup** | Inicia el listener automáticamente al lanzar. | `WsjtxAutoStart` |
| **CQ** | Muestra solo llamadas CQ de WSJT-X. | `WsjtxFilterCQ` |
| **CQ POTA** | Muestra llamadas CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **CQ color** | Selector de color para spots CQ. | `WsjtxColorCQ` |
| **POTA color** | Selector de color para spots POTA. | `WsjtxColorPOTA` |
| **Calling Me color** | Selector de color para spots Calling Me. | `WsjtxColorCallingMe` |
| **Default color** | Selector de color para otros spots de WSJT-X. | `WsjtxColorDefault` |
| **WSJT-X Decodes** | Consola de transmisiones decodificadas. | — |
| **Spot Life:** | Segundos que los spots de WSJT-X permanecen en el panadapter. | `WsjtxSpotLife` |

## Pestaña SpotCollector

### Escuchar transmisiones de SpotCollector

1. Haga clic en la pestaña **SpotCollector**.
2. En el campo **UDP Port:**, establezca el puerto en el que SpotCollector transmite. Esto se guarda en `SpotCollectorPort`.
3. Haga clic en **Start** para comenzar a escuchar. El estado cambia a **Listening**.
4. Para iniciar automáticamente al lanzar, active **Auto-start on startup**. Esto se guarda en `SpotCollectorAutoStart`.

### Qué hace cada control en la pestaña SpotCollector

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que SpotCollector transmite. Rango válido: 1–65535. | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el listener UDP. | — |
| **Auto-start on startup** | Inicia el listener automáticamente al lanzar. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola de spots recibidos de SpotCollector. | — |

## Pestaña POTA

### Consultar activaciones de POTA

1. Haga clic en la pestaña **POTA**.
2. Establezca **Poll Interval:** en los segundos entre consultas. Esto se guarda en `PotaPollInterval`.
3. Haga clic en **Start** para comenzar a consultar. El estado cambia a **Polling**.
4. Para iniciar automáticamente al lanzar, active **Auto-start on startup**. Esto se guarda en `PotaAutoStart`.

### Qué hace cada control en la pestaña POTA

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: `api.pota.app` (consultas HTTP). | — |
| **Poll Interval:** | Segundos entre consultas a POTA. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene las consultas a POTA. | — |
| **Auto-start on startup** | Inicia POTA automáticamente al lanzar. | `PotaAutoStart` |
| **POTA Activations** | Consola del flujo de activaciones. | — |
| **Spot Color:** | Selector de color para spots de POTA. | `PotaSpotColor` |

## Pestaña FreeDV

### Conectarse a FreeDV

> **Nota:** La pestaña FreeDV solo está presente en compilaciones compiladas con soporte de WebSocket (`HAVE_WEBSOCKETS`).

1. Haga clic en la pestaña **FreeDV**.
2. Haga clic en **Start** para conectarse al flujo WebSocket de FreeDV. El estado cambia a **Connected**.
3. Para iniciar automáticamente al lanzar, active **Auto-start on startup**. Esto se guarda en `FreeDvAutoStart`.

### Qué hace cada control en la pestaña FreeDV

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: `qso.freedv.org` (WebSocket). | — |
| **Start / Stop** | Conecta o desconecta el WebSocket de FreeDV. | — |
| **Auto-start on startup** | Inicia FreeDV automáticamente al lanzar. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola de actividad de FreeDV. | — |
| **Spot Color:** | Selector de color para spots de FreeDV. | `FreeDvSpotColor` |

## Pestaña EiBi

### Conectarse a EiBi

1. Haga clic en la pestaña **EiBi**.
2. En el campo **Server:**, escriba el nombre de host del servidor EiBi. Esto se guarda en `EibiHost`.
3. En el campo **Port:**, establezca el puerto (1–65535). Esto se guarda en `EibiPort`.
4. En el campo **Callsign:**, escriba su indicativo de inicio de sesión. Esto se guarda en `EibiCallsign`.
5. Haga clic en **Connect** para establecer la conexión telnet. El estado cambia a **Connected**.
6. Para reconectarse automáticamente al lanzar, active **Auto-connect on startup**. Esto se guarda en `EibiAutoConnect`.

### Qué hace cada control en la pestaña EiBi

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host telnet de EiBi. | `EibiHost` |
| **Port:** | Puerto telnet de EiBi. Rango válido: 1–65535. | `EibiPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado a EiBi. | `EibiCallsign` |
| **Connect / Disconnect** | Alterna la conexión telnet. | — |
| **Auto-connect on startup** | Inicia EiBi automáticamente al lanzar. | `EibiAutoConnect` |
| **EiBi Spots** | Consola de spots recibidos de EiBi. | — |
| **Spot Color:** | Selector de color para spots de EiBi. | `EibiSpotColor` |

## Pestaña N1MM

### Conectarse al N1MM Logger+ Spot Collector

1. Haga clic en la pestaña **N1MM**.
2. En el campo **Port:**, establezca el puerto UDP en el que N1MM Logger+ transmite mensajes de Spot Collector. Esto se guarda en `N1mmPort`.
3. Haga clic en **Start** para comenzar a escuchar. El estado cambia a **Listening**.
4. Para iniciar automáticamente al lanzar, active **Auto-start on startup**. Esto se guarda en `N1mmAutoStart`.

### Qué hace cada control en la pestaña N1MM

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Port:** | Puerto UDP para
