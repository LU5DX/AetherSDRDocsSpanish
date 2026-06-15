# Audio DAX

El applet **DAX Audio** muestra medidores RX por canal y controles deslizantes de ganancia para DAX 1-4, junto con un medidor TX único, con un interruptor maestro de habilitación que persiste como `AutoStartDAX`. En v0.9.7 (Linux), la latencia RX de DAX se reduce de ~400 ms a ~200 ms mediante una ruta de origen `pw_stream` nativa de PipeWire, reemplazando el anterior cliente PulseAudio.

## Abrir DAX Audio

Haga clic en el botón **DAX Audio** en la barra de herramientas.

## Disposición de DAX Audio

La ventana DAX Audio contiene controles para habilitar el puente de audio DAX, establecer la ganancia RX por canal, la ganancia TX y ver las asignaciones de slices.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **DAX Enable** | desactivado | activado/desactivado | `AutoStartDAX` | Inicia el puente de audio DAX; emite `daxToggled`. La etiqueta del botón es "Enable"; interruptor maestro para todos los flujos RX y TX de DAX. |
| **DAX 1 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain1` | Medidor/control deslizante combinado; arrastre para establecer la ganancia RX en el canal DAX 1. Emite `daxRxGainChanged(1, g)` y persiste. |
| **DAX 2 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain2` | Medidor/control deslizante combinado; arrastre para establecer la ganancia RX en el canal DAX 2. |
| **DAX 3 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain3` | Medidor/control deslizante combinado; arrastre para establecer la ganancia RX en el canal DAX 3. |
| **DAX 4 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain4` | Medidor/control deslizante combinado; arrastre para establecer la ganancia RX en el canal DAX 4. |
| **TX gain+meter** | 0.5 | 0.0–1.0 | `DaxTxGain` | Medidor/control deslizante combinado para el flujo TX de DAX. |

### Indicadores de Asignación de Slice

Cada canal DAX muestra qué slice (si lo hay) está actualmente enrutado a él.

| Indicador | Estados | Significado |
|-----------|--------|---------|
| **DAX 1 assignment** | —, Slice A..H | El slice (si lo hay) actualmente asignado a este canal DAX. |
| **DAX 2 assignment** | —, Slice A..H | El slice (si lo hay) actualmente asignado a este canal DAX. |
| **DAX 3 assignment** | —, Slice A..H | El slice (si lo hay) actualmente asignado a este canal DAX. |
| **DAX 4 assignment** | —, Slice A..H | El slice (si lo hay) actualmente asignado a este canal DAX. |
| **TX assignment** | —, Slice A..H | El slice que actualmente tiene privilegios TX (controla DAX TX). |

# Control CAT

El applet **CAT Control** ejecuta hasta cuatro servidores TCP compatibles con `rigctld` (y enlaces simbólicos PTY en Linux/macOS) para que el software de registro y concurso externo pueda controlar un slice por canal. AetherSDR implementa un protocolo `rigctl` nativo de Hamlib NET, eliminando la necesidad de un puente `rigctld` independiente.

## Abrir Control CAT

Haga clic en el botón **CAT Control** en la barra de herramientas, o presione `Ctrl+Shift+C`.

## Disposición de Control CAT

La ventana CAT Control contiene controles para habilitar los servidores TCP y TTY, configurar el puerto base y monitorear el estado por canal.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Enable TCP** | desactivado | activado/desactivado | `CatTcpPort` | Inicia/detiene los cuatro servidores TCP `rigctld` en `Base..Base+3`. También persiste el puerto base actual. |
| **Enable TTY** | desactivado | activado/desactivado | — | Inicia/detiene los cuatro enlaces simbólicos PTY en `$XDG_RUNTIME_DIR/aethersdr/cat-A..D` (Linux) o `~/Library/Caches/AetherSDR/cat-A..D` (macOS). |
| **Base** | 4532 | 1024–65535 | `CatTcpPort` | Puerto TCP base; los canales se enlazan al puerto, puerto+1, puerto+2, puerto+3. Los valores fuera de rango vuelven a 4532; los servidores se reinician con el nuevo puerto si están actualmente habilitados. |

### Estado por Canal

Cada canal (A/B/C/D) muestra su estado en una fila:

| Canal | Estado TCP | Ruta PTY |
|---------|------------|----------|
| **A** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **B** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **C** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **D** | (detenido) | Ruta al enlace simbólico o "detenido" |

El **Estado TCP** muestra:
- `(detenido)` cuando el servidor no está en ejecución
- `:<puerto> (1 cliente)` cuando un cliente está conectado
- `:<puerto> (N clientes)` cuando varios clientes están conectados

La **Ruta PTY** muestra la ruta del enlace simbólico que el software de registro puede abrir como un dispositivo serie:
- Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D`
- macOS: `~/Library/Caches/AetherSDR/cat-A` a `cat-D`
- Muestra "detenido" cuando el servidor TTY no está en ejecución

## Notas de Seguridad

En v26.5.3, la ubicación del enlace simbólico PTY se trasladó de `/tmp` a directorios de tiempo de ejecución por usuario para corregir una vulnerabilidad de enlace simbólico entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico de enlaces simbólicos mediante `symlink(.tmp) + rename(.tmp, final)` cierra la ventana TOCTOU.

# SpotHub

El diálogo **SpotHub** es el centro central para conectarse a fuentes de spots DX — DX cluster, Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV — y configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

Haga clic en el botón **SpotHub** en la barra de herramientas, o presione `Ctrl+Shift+S`.

## Disposición de SpotHub

El diálogo SpotHub contiene una interfaz de múltiples pestañas. Cada pestaña de fuente proporciona controles de conexión, una consola de datos y un selector de color de spot. Una pestaña **Display** separada controla la visualización de spots en el panadapter, los ajustes de Signal History y el coloreado de DXCC.

### Pestaña Cluster

La pestaña **Cluster** proporciona una conexión telnet a un DX cluster.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Server:** | — | — | `ClusterHost` | Nombre de host del DX cluster al que conectarse. |
| **Port:** | — | 1–65535 | `ClusterPort` | Puerto Telnet en el DX cluster. |
| **Callsign:** | — | — | `ClusterCallsign` | Indicativo de inicio de sesión enviado al cluster. |
| **Connect / Disconnect** | Connect | — | — | Activa/desactiva la conexión telnet al cluster. |
| **Auto-connect on startup** | — | — | `ClusterAutoConnect` | Conecta automáticamente el cluster al iniciar. |
| **Cluster Console** | — | — | — | Consola telnet de solo lectura del tráfico bruto del cluster. |
| **Send** | — | — | — | Envía un comando escrito al cluster. |
| **Spot Color:** | — | — | `ClusterSpotColor` | Abre un selector de color para los spots del cluster. |

### Pestaña RBN

La pestaña **RBN** proporciona una fuente telnet de Reverse Beacon Network con limitación de velocidad.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Server:** | — | — | `RbnHost` | Nombre de host telnet de RBN. |
| **Port:** | — | 1–65535 | `RbnPort` | Puerto telnet de RBN. |
| **Callsign:** | — | — | `RbnCallsign` | Indicativo de inicio de sesión a RBN. |
| **Rate Limit:** | — | — | `RbnRateLimit` | Limita los spots de RBN por segundo. |
| **Connect / Disconnect (RBN)** | Connect | — | — | Activa/desactiva la conexión RBN. |
| **Auto-connect on startup (RBN)** | — | — | `RbnAutoConnect` | Inicia RBN automáticamente. |
| **RBN Console** | — | — | — | Consola de solo lectura del tráfico de RBN. |
| **Send (RBN)** | — | — | — | Envía un comando a RBN. |
| **Spot Color: (RBN)** | — | — | `RbnSpotColor` | Selector de color para spots de RBN. |

### Pestaña WSJT-X

La pestaña **WSJT-X** proporciona un listener UDP para decodificaciones de WSJT-X con filtros y colores.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Address:** | — | — | `WsjtxAddress` | Dirección de enlace UDP para mensajes de WSJT-X. |
| **Port:** | — | 1–65535 | `WsjtxPort` | Puerto UDP para WSJT-X. |
| **Start / Stop** | — | — | — | Inicia o detiene el listener UDP. |
| **Auto-start on startup (WSJT-X)** | — | — | `WsjtxAutoStart` | Inicia automáticamente el listener al iniciar. |
| **CQ** | — | — | `WsjtxFilterCQ` | Muestra solo llamadas CQ de WSJT-X. |
| **CQ POTA** | — | — | `WsjtxFilterPOTA` | Muestra llamadas CQ POTA. |
| **Calling Me** | — | — | `WsjtxFilterCallingMe` | Muestra solo decodificaciones dirigidas a su indicativo. |
| **CQ color / POTA color / Calling Me color / Default color** | — | — | `WsjtxColorCQ` / `WsjtxColorPOTA` / `WsjtxColorCallingMe` / `WsjtxColorDefault` | Selectores de color para cada categoría de spot de WSJT-X. |
| **WSJT-X Decodes** | — | — | — | Consola de transmisiones decodificadas. |
| **Spot Life:** | — | — | `WsjtxSpotLife` | Segundos que los spots de WSJT-X permanecen en el panadapter. |

### Pestaña SpotCollector

La pestaña **SpotCollector** proporciona un listener UDP para transmisiones de Ham Radio Deluxe SpotCollector.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **UDP Port:** | — | 1–65535 | `SpotCollectorPort` | Puerto UDP en el que SpotCollector transmite. |
| **Start / Stop (SpotCollector)** | — | — | — | Inicia o detiene el listener UDP. |
| **Auto-start on startup (SpotCollector)** | — | — | `SpotCollectorAutoStart` | Inicia automáticamente el listener al iniciar. |
| **SpotCollector Spots** | — | — | — | Consola de spots recibidos de SpotCollector. |

### Pestaña POTA

La pestaña **POTA** consulta api.pota.app para activaciones actuales.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Server:** | api.pota.app (consulta HTTP) | — | — | Muestra el punto final fijo de POTA. |
| **Poll Interval:** | — | — | `PotaPollInterval` | Segundos entre consultas a POTA. |
| **Start / Stop (POTA)** | — | — | — | Inicia o detiene la consulta a POTA. |
| **Auto-start on startup (POTA)** | — | — | `PotaAutoStart` | Inicia automáticamente POTA al iniciar. |
| **POTA Activations** | — | — | — | Consola del feed de activaciones. |
| **Spot Color: (POTA)** | — | — | `PotaSpotColor` | Selector de color para spots de POTA. |

### Pestaña FreeDV

La pestaña **FreeDV** proporciona un feed WebSocket de spots del reportero de QSO FreeDV. Esta pestaña solo está disponible cuando AetherSDR se compila con soporte WebSocket.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Server:** | qso.freedv.org (WebSocket) | — | — | Muestra el punto final fijo de FreeDV. |
| **Start / Stop (FreeDV)** | — | — | — | Conecta o desconecta el WebSocket de FreeDV. |
| **Auto-start on startup (FreeDV)** | — | — | `FreeDvAutoStart` | Inicia automáticamente FreeDV al iniciar. |
| **FreeDV Spots** | — | — | — | Consola de actividad de FreeDV. |
| **Spot Color: (FreeDV)** | — | — | `FreeDvSpotColor` | Selector de color para spots de FreeDV. |

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y buscable de todos los spots activos de todas las fuentes.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Bands:** | — | — | — | Casillas de verificación por banda para alternar la visibilidad en la tabla. Una casilla por banda (160m
