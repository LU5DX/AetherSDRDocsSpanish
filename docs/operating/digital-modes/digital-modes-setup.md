# DAX Audio

El applet **DAX Audio** muestra medidores de RX por canal y controles deslizantes de ganancia para DAX 1-4, junto con un medidor de TX único, con un interruptor maestro de habilitación que persiste como `AutoStartDAX`. En v0.9.7 (Linux), la latencia de RX de DAX se reduce de ~400 ms a ~200 ms mediante una ruta de fuente `pw_stream` nativa de PipeWire, reemplazando el cliente PulseAudio anterior.

> **Nota para usuarios de Windows:** AetherSDR no incluye un puente DAX incorporado en Windows. El applet DAX Audio muestra únicamente un mensaje informativo. Utilice los controladores TCI o SmartSDR DAX de FlexRadio. Consulte Ayuda > Configuración de modos de datos para obtener instrucciones de configuración.

## Abrir DAX Audio

Haga clic en el botón **DAX Audio** en la barra de herramientas.

## Diseño de DAX Audio

La ventana DAX Audio contiene controles para habilitar el puente de audio DAX, ajustar la ganancia de RX por canal, la ganancia de TX y ver las asignaciones de los slices.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **DAX Enable** | desactivado | activado/desactivado | `AutoStartDAX` | Inicia el puente de audio DAX; emite `daxToggled`. La etiqueta del botón refleja el estado actual: "Enabled" cuando está activo, "Disabled" cuando está desactivado. Interruptor maestro para todos los flujos DAX RX y TX. |
| **DAX 1 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain1` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 1. Emite `daxRxGainChanged(1, g)` y persiste. |
| **DAX 2 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain2` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 2. |
| **DAX 3 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain3` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 3. |
| **DAX 4 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain4` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 4. |
| **TX gain+meter** | 0.5 | 0.0–1.0 | `DaxTxGain` | Medidor/control deslizante combinado para el flujo DAX TX. |

### Indicadores de asignación de slice

Cada canal DAX muestra qué slice (si lo hay) está actualmente enrutado a él.

| Indicador | Estados | Significado |
|-----------|--------|---------|
| **DAX 1 assignment** | —, Slice A..H | El slice (si lo hay) actualmente asignado a este canal DAX. |
| **DAX 2 assignment** | —, Slice A..H | El slice (si lo hay) actualmente asignado a este canal DAX. |
| **DAX 3 assignment** | —, Slice A..H | El slice (si lo hay) actualmente asignado a este canal DAX. |
| **DAX 4 assignment** | —, Slice A..H | El slice (si lo hay) actualmente asignado a este canal DAX. |
| **TX assignment** | —, Slice A..H | El slice que actualmente posee los privilegios de TX (controla DAX TX). |

### Comportamiento en plataforma Windows

En Windows, el applet DAX Audio muestra únicamente una nota informativa: "No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX." No se incluyen controles, medidores ni indicadores. Los establecedores de estado interno del applet (`setDaxEnabled`, `setDaxRxLevel`, `setDaxTxLevel`) están protegidos y no realizan ninguna acción.

# CAT Control

El applet **CAT Control** ejecuta hasta cuatro servidores TCP compatibles con `rigctld` (y enlaces simbólicos PTY en Linux/macOS) para que el software de registro y concurso externo pueda controlar un slice por canal. AetherSDR implementa un protocolo Hamlib NET `rigctl` nativo, eliminando la necesidad de un puente `rigctld` independiente.

## Abrir CAT Control

Haga clic en el botón **CAT Control** en la barra de herramientas, o presione `Ctrl+Shift+C`.

## Diseño de CAT Control

La ventana CAT Control contiene controles para habilitar los servidores TCP y TTY, configurar el puerto base y monitorear el estado por canal.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Enable TCP** | desactivado | activado/desactivado | `CatTcpPort` | Inicia/detiene los cuatro servidores TCP `rigctld` en `Base..Base+3`. También persiste el puerto base actual. |
| **Enable TTY** | desactivado | activado/desactivado | — | Inicia/detiene los cuatro enlaces simbólicos PTY bajo `$XDG_RUNTIME_DIR/aethersdr/cat-A..D` (Linux) o `~/Library/Caches/AetherSDR/cat-A..D` (macOS). |
| **Base** | 4532 | 1024–65535 | `CatTcpPort` | Puerto base TCP; los canales se vinculan al puerto, puerto+1, puerto+2, puerto+3. Los valores fuera de rango vuelven a 4532; los servidores se reinician con el nuevo puerto si está habilitado actualmente. |

### Estado por canal

Cada canal (A/B/C/D) muestra su estado en una fila:

| Canal | Estado TCP | Ruta PTY |
|---------|------------|----------|
| **A** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **B** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **C** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **D** | (detenido) | Ruta al enlace simbólico o "detenido" |

El **Estado TCP** muestra:
- `(stopped)` cuando el servidor no está en ejecución
- `:<port> (1 client)` cuando un cliente está conectado
- `:<port> (N clients)` cuando varios clientes están conectados

La **Ruta PTY** muestra la ruta del enlace simbólico que el software de registro puede abrir como un dispositivo serie:
- Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` hasta `cat-D`
- macOS: `~/Library/Caches/AetherSDR/cat-A` hasta `cat-D`
- Muestra "detenido" cuando el servidor TTY no está en ejecución

## Notas de seguridad

En v26.5.3, la ubicación del enlace simbólico PTY se movió de `/tmp` a directorios de ejecución por usuario para corregir una vulnerabilidad de enlace simbólico entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico del enlace simbólico mediante `symlink(.tmp) + rename(.tmp, final)` cierra la ventana TOCTOU.

# SpotHub

El diálogo **SpotHub** es el centro central para conectarse a fuentes de spots DX — DX cluster, Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV — y configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

Haga clic en el botón **SpotHub** en la barra de herramientas, o presione `Ctrl+Shift+S`.

## Diseño de SpotHub

El diálogo SpotHub contiene una interfaz de múltiples pestañas. Cada pestaña de fuente proporciona controles de conexión, una consola de datos y un selector de color de spot. Una pestaña **Display** separada controla la visualización de spots en el panadapter, parámetros ajustables de Signal History y el coloreado de DXCC.

### Pestaña Cluster

La pestaña **Cluster** proporciona una conexión telnet a un DX cluster.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Server:** | — | — | `ClusterHost` | Nombre de host del DX cluster al que conectarse. |
| **Port:** | — | 1–65535 | `ClusterPort` | Puerto Telnet del DX cluster. |
| **Callsign:** | — | — | `ClusterCallsign` | Indicativo de inicio de sesión enviado al cluster. |
| **Connect / Disconnect** | Conectar | — | — | Alterna la conexión telnet al cluster. |
| **Auto-connect on startup** | — | — | `ClusterAutoConnect` | Conecta automáticamente el cluster al iniciar. |
| **Cluster Console** | — | — | — | Consola telnet de solo lectura del tráfico sin procesar del cluster. |
| **Send** | — | — | — | Envía un comando escrito al cluster. |
| **Spot Color:** | — | — | `ClusterSpotColor` | Abre un selector de color para los spots del cluster. |

### Pestaña RBN

La pestaña **RBN** proporciona una fuente telnet de Reverse Beacon Network con limitación de velocidad.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Server:** | — | — | `RbnHost` | Nombre de host telnet de RBN. |
| **Port:** | — | 1–65535 | `RbnPort` | Puerto telnet de RBN. |
| **Callsign:** | — | — | `RbnCallsign` | Indicativo de inicio de sesión para RBN. |
| **Rate Limit:** | — | — | `RbnRateLimit` | Limita los spots de RBN por segundo. |
| **Connect / Disconnect (RBN)** | Conectar | — | — | Alterna la conexión RBN. |
| **Auto-connect on startup (RBN)** | — | — | `RbnAutoConnect` | Inicia RBN automáticamente. |
| **RBN Console** | — | — | — | Consola de solo lectura del tráfico de RBN. |
| **Send (RBN)** | — | — | — | Envía un comando a RBN. |
| **Spot Color: (RBN)** | — | — | `RbnSpotColor` | Selector de color para spots de RBN. |

### Pestaña WSJT-X

La pestaña **WSJT-X** proporciona un listener UDP para decodificaciones de WSJT-X con filtros y colores.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Address:** | — | — | `WsjtxAddress` | Dirección de enlace UDP para mensajes WSJT-X. |
| **Port:** | — | 1–65535 | `WsjtxPort` | Puerto UDP para WSJT-X. |
| **Start / Stop** | — | — | — | Inicia o detiene el listener UDP. |
| **Auto-start on startup (WSJT-X)** | — | — | `WsjtxAutoStart` | Inicia automáticamente el listener al iniciar. |
| **CQ** | — | — | `WsjtxFilterCQ` | Mostrar solo llamadas CQ de WSJT-X. |
| **CQ POTA** | — | — | `WsjtxFilterPOTA` | Mostrar llamadas CQ POTA. |
| **Calling Me** | — | — | `WsjtxFilterCallingMe` | Mostrar solo decodificaciones dirigidas a su indicativo. |
| **CQ color / POTA color / Calling Me color / Default color** | — | — | `WsjtxColorCQ` / `WsjtxColorPOTA` / `WsjtxColorCallingMe` / `WsjtxColorDefault` | Selectores de color para cada categoría de spot de WSJT-X. |
| **WSJT-X Decodes** | — | — | — | Consola de transmisiones decodificadas. |
| **Spot Life:** | — | — | `WsjtxSpotLife` | Segundos que los spots de WSJT-X permanecen en el panadapter. |

### Pestaña SpotCollector

La pestaña **SpotCollector** proporciona un listener UDP para transmisiones de Ham Radio Deluxe SpotCollector.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **UDP Port:** | — | 1–65535 | `SpotCollectorPort` | Puerto UDP en el que transmite SpotCollector. |
| **Start / Stop (SpotCollector)** | — | — | — | Inicia o detiene el listener UDP. |
| **Auto-start on startup (SpotCollector)** | — | — | `SpotCollectorAutoStart` | Inicia automáticamente el listener al iniciar. |
| **SpotCollector Spots** | — | — | — | Consola de spots recibidos de SpotCollector. |

### Pestaña POTA

La pestaña **POTA** consulta api.pota.app para obtener activaciones actuales.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Server:** | api.pota.app (sondeo HTTP) | — | — | Muestra el punto final fijo de POTA. |
| **Poll Interval:** | — | — | `PotaPollInterval` | Segundos entre sondeos de POTA. |
| **Start / Stop (POTA)** | — | — | — | Inicia o detiene el sondeo de POTA. |
| **Auto-start on startup (POTA)** | — | — | `PotaAutoStart` | Inicia automáticamente POTA al iniciar. |
| **POTA Activations** | — | — | — | Consola del feed de activaciones. |
| **Spot Color: (POTA)** | — | — | `PotaSpotColor` | Selector de color para spots de POTA. |

### Pestaña FreeDV

La pestaña **FreeDV** proporciona un feed WebSocket de spots del reportero QSO de FreeDV. Esta pestaña solo está disponible cuando AetherSDR se compila con soporte WebSocket.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Server:** | qso.freedv.org (WebSocket) | — | — | Muestra el punto final fijo de FreeDV. |
| **Start / Stop (FreeDV)** | — | — | — | Conecta o desconecta el WebSocket de FreeDV. |
