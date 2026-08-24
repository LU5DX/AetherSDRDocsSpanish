# SpotHub (antes Diálogo de DX Cluster)

Centro central para conectarse a fuentes de spots DX — DX cluster, Reverse Beacon Network, WSJT-X, SpotCollector, POTA, FreeDV y otras — y para configurar cómo se muestran los spots en el panadapter.

## Antes de comenzar

- Las fuentes de spots que usan WebSocket (FreeDV) están disponibles solo en compilaciones creadas con soporte WebSocket (`HAVE_WEBSOCKETS`). Si la pestaña FreeDV no aparece, su compilación no la incluye.
- Los spots aparecen en el panadapter solo cuando la superposición maestra de spots está habilitada (consulte la pestaña **Display** > conmutador **Spots:**). Si los spots no son visibles después de conectarse, verifique que ese conmutador esté activado.
- El diálogo recuerda la geometría de su ventana entre sesiones (guardada en `DxClusterDialogGeometry`).

## Abrir SpotHub

1. Abra **Settings > SpotHub...**.

El diálogo se abre como una ventana sin marco y redimensionable. Arrastre cualquier borde para cambiar su tamaño.

## Resumen de pestañas

SpotHub tiene ocho pestañas, cada una correspondiente a una fuente de spots o a una configuración de visualización:

- **Cluster** — Conexión telnet a DX cluster, consola y color de spots
- **RBN** — Fuente telnet de Reverse Beacon Network con límite de velocidad
- **WSJT-X** — Receptor UDP de WSJT-X con filtros y asignación de colores
- **SpotCollector** — Receptor UDP para transmisiones de SpotCollector de Ham Radio Deluxe
- **POTA** — Consulta `api.pota.app` para activaciones actuales
- **FreeDV** — Fuente WebSocket de spots del reporte de QSO de FreeDV
- **Spot List** — Tabla unificada y buscable de todos los spots activos
- **Display** — Visualización de spots en el panadapter, historial de señales y coloración DXCC

## Pestaña Cluster

### Configuración de conexión

| Control | Tipo | Clave de ajuste | Comportamiento |
|---------|------|-------------|----------|
| **Server:** | Campo de texto | `ClusterHost` | Nombre de host del DX cluster al que conectarse. |
| **Port:** | Spinbox (1-65535) | `ClusterPort` | Puerto telnet del DX cluster. |
| **Callsign:** | Campo de texto | `ClusterCallsign` | Indicativo de inicio de sesión enviado al cluster. |

### Controles de conexión

1. Complete la configuración de conexión anterior.
2. Haga clic en **Connect** para abrir la sesión telnet. La etiqueta del botón cambia a **Disconnect** mientras está conectado; haga clic nuevamente para cerrar.
3. Haga clic en **Auto-connect on startup** para que AetherSDR se conecte al iniciar. Ajuste: `ClusterAutoConnect`.

### Consola y comandos del cluster

- **Cluster Console** — Campo de texto de solo lectura que muestra el tráfico telnet sin procesar del cluster.
- Para enviar un comando, escriba en el campo de texto debajo de la consola y haga clic en **Send**.
- Haga clic en **Startup Commands…** para abrir un editor de comandos que se envían automáticamente después de cada inicio de sesión. Ingrese un comando por línea, por ejemplo:
  ```
  SET/NAME YOUR_NAME
  SET/QTH YOUR_QTH
  ACCEPT/SPOT
  ```
  Los comandos se guardan en `DxClusterStartupCommands` y se reproducen cada vez que la conexión al cluster se restablece (no solo en el inicio de sesión inicial). Nuevo en v26.5.2.1.

### Color de spots

- **Spot Color:** — Abre un selector de color para los spots del cluster. Ajuste: `ClusterSpotColor`.

## Pestaña RBN

### Configuración de conexión

| Control | Tipo | Clave de ajuste | Comportamiento |
|---------|------|-------------|----------|
| **Server:** | Campo de texto | `RbnHost` | Nombre de host telnet de RBN. |
| **Port:** | Spinbox (1-65535) | `RbnPort` | Puerto telnet de RBN. |
| **Callsign:** | Campo de texto | `RbnCallsign` | Indicativo de inicio de sesión en RBN. |
| **Rate Limit:** | Spinbox | `RbnRateLimit` | Limita los spots de RBN por segundo. |

### Controles de conexión

1. Complete la configuración de conexión anterior.
2. Haga clic en **Connect** para abrir la sesión telnet. La etiqueta del botón cambia a **Disconnect** mientras está conectado; haga clic nuevamente para cerrar.
3. Haga clic en **Auto-connect on startup** para que AetherSDR se conecte al iniciar. Ajuste: `RbnAutoConnect`.

### Consola y comandos de RBN

- **RBN Console** — Campo de texto de solo lectura que muestra el tráfico RBN sin procesar.
- Para enviar un comando, escriba en el campo de texto debajo de la consola y haga clic en **Send**.
- Haga clic en **Startup Commands…** para abrir un editor de comandos que se envían automáticamente después de cada inicio de sesión. Ingrese un comando por línea. Los comandos se guardan en `RbnStartupCommands` y se reproducen cada vez que la conexión RBN se restablece. Nuevo en v26.5.2.1.

### Color de spots

- **Spot Color:** — Abre un selector de color para los spots de RBN. Ajuste: `RbnSpotColor`.

## Pestaña WSJT-X

### Configuración del receptor

| Control | Tipo | Clave de ajuste | Comportamiento |
|---------|------|-------------|----------|
| **Address:** | Campo de texto | `WsjtxAddress` | Dirección de enlace UDP para mensajes de WSJT-X. |
| **Port:** | Spinbox (1-65535) | `WsjtxPort` | Puerto UDP para WSJT-X. |

### Controles de conexión

1. Configure la dirección y el puerto para que coincidan con la configuración de Reporting de WSJT-X.
2. Haga clic en **Start** para comenzar a escuchar las transmisiones UDP de WSJT-X. La etiqueta del botón cambia a **Stop** mientras está escuchando.
3. Haga clic en **Auto-start on startup** para que AetherSDR comience a escuchar al iniciar. Ajuste: `WsjtxAutoStart`.

### Filtros

Marque cualquiera de las siguientes casillas para restringir qué decodificaciones de WSJT-X aparecen:

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **CQ** | `WsjtxFilterCQ` | Mostrar solo llamadas CQ. |
| **CQ POTA** | `WsjtxFilterPOTA` | Mostrar solo llamadas CQ POTA. |
| **Calling Me** | `WsjtxFilterCallingMe` | Mostrar solo decodificaciones dirigidas a su indicativo. |

### Configuración de colores

Haga clic en cada muestra de color para abrir un selector de color para esa categoría:

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **CQ color** | `WsjtxColorCQ` | Color para spots CQ. |
| **POTA color** | `WsjtxColorPOTA` | Color para spots CQ POTA. |
| **Calling Me color** | `WsjtxColorCallingMe` | Color para decodificaciones dirigidas a su indicativo. |
| **Default color** | `WsjtxColorDefault` | Color para todos los demás spots de WSJT-X. |

### Consola de decodificaciones y vida del spot

- **WSJT-X Decodes** — Campo de texto de solo lectura que muestra las transmisiones decodificadas.
- **Spot Life:** — Spinbox que controla cuántos segundos permanecen los spots de WSJT-X en el panadapter. Ajuste: `WsjtxSpotLife`.

## Pestaña SpotCollector

### Configuración del receptor

| Control | Tipo | Clave de ajuste | Comportamiento |
|---------|------|-------------|----------|
| **UDP Port:** | Spinbox (1-65535) | `SpotCollectorPort` | Puerto UDP en el que transmite SpotCollector. |

### Controles de conexión

1. Configure el puerto para que coincida con el puerto de transmisión de su SpotCollector.
2. Haga clic en **Start** para comenzar a escuchar. La etiqueta del botón cambia a **Stop** mientras está escuchando.
3. Haga clic en **Auto-start on startup** para que AetherSDR comience a escuchar al iniciar. Ajuste: `SpotCollectorAutoStart`.

### Consola de spots

- **SpotCollector Spots** — Campo de texto de solo lectura que muestra los spots recibidos.

## Pestaña POTA

### Configuración de conexión

| Control | Tipo | Clave de ajuste | Comportamiento |
|---------|------|-------------|----------|
| **Server:** | Indicador | Ninguna | Punto final fijo: `api.pota.app (HTTP polling)`. |
| **Poll Interval:** | Spinbox | `PotaPollInterval` | Segundos entre consultas a POTA. |

### Controles de conexión

1. Haga clic en **Start** para comenzar a consultar las activaciones actuales. La etiqueta del botón cambia a **Stop** mientras está consultando.
2. Haga clic en **Auto-start on startup** para que AetherSDR comience a consultar al iniciar. Ajuste: `PotaAutoStart`.

### Consola de activaciones y color

- **POTA Activations** — Campo de texto de solo lectura que muestra el flujo de activaciones.
- **Spot Color:** — Abre un selector de color para los spots de POTA. Ajuste: `PotaSpotColor`.

## Pestaña FreeDV

### Configuración de conexión

| Control | Tipo | Clave de ajuste | Comportamiento |
|---------|------|-------------|----------|
| **Server:** | Indicador | Ninguna | Punto final fijo: `qso.freedv.org (WebSocket)`. |

### Controles de conexión

1. Haga clic en **Start** para conectarse al WebSocket de FreeDV. El indicador de estado cambia a **Connected** cuando el handshake de WebSocket tiene éxito.
2. Haga clic en **Auto-start on startup** para que AetherSDR se conecte al iniciar. Ajuste: `FreeDvAutoStart`.

### Consola de spots y color

- **FreeDV Spots** — Campo de texto de solo lectura que muestra la actividad entrante de FreeDV.
- **Spot Color:** — Abre un selector de color para los spots de FreeDV. Ajuste: `FreeDvSpotColor`.

### Station Reporting

El grupo **Station Reporting** en la parte inferior de la pestaña FreeDV le permite transmitir su actividad al mapa público de FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo.

#### Requisitos antes de habilitar

- Debe haber un indicativo válido en el campo **Callsign:** (o proveniente de la radio).
- Debe haber un cuadrado Maidenhead válido en el campo **Grid Square:** (o proveniente del GPS de la radio).

Si alguno de los valores está vacío cuando marca **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra una advertencia y deja la casilla sin marcar. Esto evita que se transmitan valores vacíos o de marcador de posición al mapa público compartido.

#### Pasos de configuración

1. En el grupo **Station Reporting**, revise el campo **Callsign:**.
   - Si **Use radio** está marcado (valor predeterminado), el campo se rellena previamente con el indicativo configurado en su radio y es de solo lectura. Los cambios al indicativo de la radio en Radio Setup se reflejan automáticamente.
   - Desmarque **Use radio** para ingresar un indicativo manualmente. El valor ingresado se guarda en `FreeDvMyCallsign` y se convierte a mayúsculas al guardar.
2. Revise el campo **Grid Square:**.
   - Si su radio tiene hardware GPS y **Use GPS** está marcado (valor predeterminado en modelos con capacidad GPS), el campo se rellena previamente desde la posición GPS de la radio y es de solo lectura. La casilla **Use GPS** está oculta en modelos de radio sin hardware GPS.
   - Desmarque **Use GPS** (o si la casilla no está presente) para ingresar un cuadrado Maidenhead manualmente. El valor se guarda en `FreeDvMyGrid` y se convierte a mayúsculas al guardar.
3. Opcionalmente, complete **Station Msg:** con una nota breve de texto libre. Este mensaje aparece junto a su indicativo en el mapa público de FreeDV Reporter y se guarda en `FreeDvMyMessage`.
4. Marque **Enable FreeDV Reporter reporting when RADE is active**. AetherSDR valida el indicativo y el cuadrado antes de aceptar el cambio, luego guarda `FreeDvAutoReport` = `True` y emite la señal de reporte habilitado.

#### Controles de Station Reporting

| Control | Tipo | Comportamiento |
|---------|------|----------|
| **Callsign:** | Campo de texto | Indicativo a reportar. Solo lectura cuando **Use radio** está marcado. Guardado en `FreeDvMyCallsign`. |
| **Use radio** | Casilla de verificación | Rellena previamente el indicativo desde el indicativo configurado en la radio. Guardado en `FreeDvUseRadioCallsign`. |
| **Grid Square:** | Campo de texto | Cuadrado Maidenhead a reportar. Solo lectura cuando **Use GPS** está marcado. Guardado en `FreeDvMyGrid`. |
| **Use GPS** | Casilla de verificación | Rellena previamente el cuadrado desde el módulo GPS de la radio. Se muestra solo en modelos con capacidad GPS. Guardado en `FreeDvUseGpsGrid`. |
| **Station Msg:** | Campo de texto | Mensaje opcional que se muestra junto a su indicativo en el mapa público. Guardado en `FreeDvMyMessage`. |
| **Enable FreeDV Reporter reporting when RADE is active** | Casilla de verificación | Habilita el reporte al mapa público. Guardado en `FreeDvAutoReport`. |

## Pestaña Spot List

La tabla unificada de spots muestra todos los spots activos de cada fuente conectada.

### Filtrado por banda

Una fila de casillas de verificación en la parte superior le permite mostrar u ocultar spots en bandas específicas (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Desmarque una banda para eliminar sus spots de la tabla.

Las casillas de verificación de banda usan un diseño de flujo que se ajusta a una nueva fila cuando el diálogo se estrecha, manteniendo cada casilla legible en lugar de comprimir las etiquetas.

### Borrar spots

Haga clic en **Clear** para vaciar la lista actual de spots.

### Tabla de spots

La tabla principal se puede ordenar haciendo clic en los encabezados de columna. Columnas:

- **Time** — Cuándo se recibió el spot (ordenable; haga clic para reordenar)
- **Freq** — Frecuencia en MHz (ordenable)
- **DX Call** — El indicativo del spot
- **Comment** — Comentario del spot (puede incluir modo, nombre, etc.)
- **Spotter** — Quién reportó la estación DX
- **Band** — Banda (por ejemplo, 20m)
- **Mode** — Modo si se incluye en el spot
- **Source** — Qué fuente proporcionó este spot (Cluster, RBN, WSJT-X, SpotCollector, POTA, FreeDV, EIBI, N1MM)

Ambas
