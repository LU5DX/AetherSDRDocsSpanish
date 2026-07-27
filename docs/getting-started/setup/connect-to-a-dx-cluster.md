# Conectarse a un clúster DX

El diálogo SpotHub de AetherSDR le permite conectarse a un clúster DX por telnet, a la Reverse Beacon Network, a WSJT-X, a SpotCollector, a POTA y a FreeDV, así como configurar cómo se muestran los spots entrantes como superposiciones en el panadapter.

## Antes de empezar

- Conozca el nombre de host (o dirección IP) y el puerto telnet de su clúster DX elegido (por ejemplo, `dxc.k0xm.net` en el puerto `7373`).
- Conozca el indicativo que usará para iniciar sesión en el clúster.

## Abrir SpotHub

1. Abra `Settings > SpotHub...`.

## Pestaña Cluster

### Conectarse a un clúster DX

1. Haga clic en la pestaña **Cluster**.
2. En el campo **Server:**, escriba el nombre de host o la dirección IP del clúster. Esto se guarda en `ClusterHost`.
3. En el campo **Port:**, establezca el puerto telnet (1–65535). Esto se guarda en `ClusterPort`.
4. En el campo **Callsign:**, escriba su indicativo. Esto se guarda en `ClusterCallsign`.
5. Haga clic en **Connect**.
   - El indicador de estado cambia a **Connected** y la etiqueta del botón cambia a **Disconnect**.
   - El tráfico entrante del clúster aparece en la pantalla de solo lectura **Cluster Console**.
6. Para reconectarse automáticamente cada vez que AetherSDR se inicie, active **Auto-connect on startup**. Esto se guarda en `ClusterAutoConnect`.

### Configurar comandos de inicio para el clúster DX

Puede configurar una lista de comandos que se envían automáticamente después de cada inicio de sesión en el clúster DX (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).

1. Haga clic en **Startup Commands…**.
2. En el diálogo, introduzca un comando por línea.
3. Haga clic en **OK** para guardar. Los comandos se almacenan en la configuración `DxClusterStartupCommands` y el cliente los reenvía después de cada inicio de sesión exitoso.

### Función de cada control en la pestaña Cluster

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host o dirección IP del servidor telnet del clúster DX. | `ClusterHost` |
| **Port:** | Puerto telnet. Rango válido: 1–65535. | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster al conectar. | `ClusterCallsign` |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet. La etiqueta muestra la acción actual. | — |
| **Auto-connect on startup** | Se conecta al clúster automáticamente cuando AetherSDR se inicia. | `ClusterAutoConnect` |
| **Startup Commands…** | Abre un diálogo para editar comandos enviados automáticamente después de cada inicio de sesión. Un comando por línea. Nuevo en v26.5.2.1. | `DxClusterStartupCommands` |
| **Cluster Console** | Pantalla de solo lectura del tráfico telnet sin procesar del clúster. | — |
| **Send** (línea de comandos) | Envía un comando escrito al clúster mientras está conectado. | — |
| **Spot Color:** | Abre un selector de color para las superposiciones de spots del clúster en el panadapter. | `ClusterSpotColor` |

## Pestaña RBN

### Conectarse a la Reverse Beacon Network

1. Haga clic en la pestaña **RBN**.
2. En el campo **Server:**, escriba el nombre de host telnet de RBN. Esto se guarda en `RbnHost`.
3. En el campo **Port:**, establezca el puerto telnet de RBN (1–65535). Esto se guarda en `RbnPort`.
4. En el campo **Callsign:**, escriba su indicativo de inicio de sesión. Esto se guarda en `RbnCallsign`.
5. Establezca el **Rate Limit:** para limitar el número de spots RBN procesados por segundo. Esto se guarda en `RbnRateLimit`.
6. Haga clic en **Connect**.
7. Para reconectarse automáticamente al iniciar, active **Auto-connect on startup**. Esto se guarda en `RbnAutoConnect`.

### Configurar comandos de inicio para RBN

Puede configurar una lista de comandos que se envían automáticamente después de cada inicio de sesión en RBN (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).

1. Haga clic en **Startup Commands…**.
2. En el diálogo, introduzca un comando por línea.
3. Haga clic en **OK** para guardar. Los comandos se almacenan en la configuración `RbnStartupCommands` y el cliente RBN los reenvía después de cada inicio de sesión exitoso.

### Función de cada control en la pestaña RBN

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host telnet de RBN. | `RbnHost` |
| **Port:** | Puerto telnet de RBN. Rango válido: 1–65535. | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión para RBN. | `RbnCallsign` |
| **Rate Limit:** | Limita los spots RBN por segundo. | `RbnRateLimit` |
| **Connect / Disconnect** | Activa o desactiva la conexión RBN. | — |
| **Auto-connect on startup** | Inicia RBN automáticamente al iniciar. | `RbnAutoConnect` |
| **Startup Commands…** | Abre un diálogo para editar comandos enviados automáticamente después de cada inicio de sesión en RBN. Un comando por línea. Nuevo en v26.5.2.1. | `RbnStartupCommands` |
| **RBN Console** | Consola de solo lectura del tráfico RBN. | — |
| **Send** | Envía un comando a RBN. | — |
| **Spot Color:** | Selector de color para spots RBN. | `RbnSpotColor` |

## Pestaña WSJT-X

### Escuchar spots de WSJT-X

1. Haga clic en la pestaña **WSJT-X**.
2. En el campo **Address:**, introduzca la dirección de enlace UDP para mensajes de WSJT-X. Esto se guarda en `WsjtxAddress`.
3. En el campo **Port:**, establezca el puerto UDP. Esto se guarda en `WsjtxPort`.
4. Haga clic en **Start** para comenzar a escuchar. El estado cambia a **Listening**.
5. Para iniciar automáticamente al iniciar, active **Auto-start on startup**. Esto se guarda en `WsjtxAutoStart`.

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

### Función de cada control en la pestaña WSJT-X

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Puerto UDP para WSJT-X. Rango válido: 1–65535. | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Inicia automáticamente el receptor al iniciar. | `WsjtxAutoStart` |
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
2. En el campo **UDP Port:**, establezca el puerto en el que transmite SpotCollector. Esto se guarda en `SpotCollectorPort`.
3. Haga clic en **Start** para comenzar a escuchar. El estado cambia a **Listening**.
4. Para iniciar automáticamente al iniciar, active **Auto-start on startup**. Esto se guarda en `SpotCollectorAutoStart`.

### Función de cada control en la pestaña SpotCollector

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que transmite SpotCollector. Rango válido: 1–65535. | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Inicia automáticamente el receptor al iniciar. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola de spots recibidos de SpotCollector. | — |

## Pestaña POTA

### Consultar activaciones de POTA

1. Haga clic en la pestaña **POTA**.
2. Establezca **Poll Interval:** en los segundos entre consultas. Esto se guarda en `PotaPollInterval`.
3. Haga clic en **Start** para comenzar a consultar. El estado cambia a **Polling**.
4. Para iniciar automáticamente al iniciar, active **Auto-start on startup**. Esto se guarda en `PotaAutoStart`.

### Función de cada control en la pestaña POTA

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: `api.pota.app` (consulta HTTP). | — |
| **Poll Interval:** | Segundos entre consultas POTA. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene la consulta POTA. | — |
| **Auto-start on startup** | Inicia POTA automáticamente al iniciar. | `PotaAutoStart` |
| **POTA Activations** | Consola del feed de activaciones. | — |
| **Spot Color:** | Selector de color para spots POTA. | `PotaSpotColor` |

## Pestaña FreeDV

### Conectarse a FreeDV

> **Nota:** La pestaña FreeDV solo está presente en compilaciones compiladas con soporte WebSocket (`HAVE_WEBSOCKETS`).

1. Haga clic en la pestaña **FreeDV**.
2. Haga clic en **Start** para conectarse al feed WebSocket de FreeDV. El estado cambia a **Connected**.
3. Para iniciar automáticamente al iniciar, active **Auto-start on startup**. Esto se guarda en `FreeDvAutoStart`.

### Función de cada control en la pestaña FreeDV

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: `qso.freedv.org` (WebSocket). | — |
| **Start / Stop** | Conecta o desconecta el WebSocket de FreeDV. | — |
| **Auto-start on startup** | Inicia FreeDV automáticamente al iniciar. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola de actividad de FreeDV. | — |
| **Spot Color:** | Selector de color para spots FreeDV. | `FreeDvSpotColor` |

## Pestaña Spot List

### Ver y filtrar spots

1. Haga clic en la pestaña **Spot List**.
2. Use las casillas de verificación de banda para alternar la visibilidad de los spots en cada banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Las casillas de verificación usan un diseño de flujo que se envuelve a líneas adicionales cuando el diálogo es demasiado estrecho para mostrarlas todas en una fila.
3. Haga clic en **Clear** para vaciar la lista de spots actual.

### Sintonizar un spot

Haga doble clic en una fila de la tabla de spots para sintonizar el slice activo a la frecuencia del spot. A partir de v0.9.7, AetherSDR también reenvía la información de modo extraída del comentario del spot, por lo que el slice cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el spot, en lugar de solo cambiar la frecuencia.

### Personalizar columnas de la tabla

Haga clic derecho en el encabezado de la tabla para abrir un menú de visibilidad de columnas. El menú permanece abierto mientras alterna columnas seleccionables, para que pueda mostrar u ocultar varias columnas (por ejemplo, Spotter, Band, Mode) de una sola vez sin que el menú se cierre después de cada alternancia.

### Función de cada control en la pestaña Spot List

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Bands:** | Casillas de verificación por banda que alternan la visibilidad en la tabla. Las casillas de verificación se envuelven a filas adicionales cuando el diálogo es estrecho. | — |
| **Clear** | Vacía la lista de spots actual. | — |
| **Spot table** | Tabla de spots ordenable. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga clic derecho en el encabezado para mostrar/ocultar columnas sin que el menú se cierre entre alternancias. | — |

## Pestaña Display

### Configurar la apariencia de la superposición de spots

La pestaña **Display** controla cómo se visualizan los spots en el panadapter.

#### Alternancias maestras

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Spots:** | Alternancia maestra para la superposición de spots DX en el panadapter. Predeterminado: Habilitado. | `IsSpotsEnabled` |
| **Memories:** | Alterna
