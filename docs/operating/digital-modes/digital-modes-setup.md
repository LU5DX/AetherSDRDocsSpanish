# Audio DAX

El applet **DAX Audio** muestra medidores de RX por canal y controles deslizantes de ganancia para DAX 1-4, más un medidor de TX único, con un interruptor maestro de habilitación que se guarda como `AutoStartDAX`. En v0.9.7 (Linux), la latencia de RX de DAX se reduce de ~400 ms a ~200 ms mediante una ruta de fuente nativa de PipeWire `pw_stream`, reemplazando el cliente PulseAudio anterior.

> **Nota para usuarios de Windows:** AetherSDR no incluye un puente DAX integrado en Windows. El applet DAX Audio solo muestra un mensaje informativo. Use los controladores TCI o SmartSDR DAX de FlexRadio en su lugar. Consulte Ayuda > Configuración de modos de datos para obtener instrucciones de configuración.

## Abrir DAX Audio

Haga clic en el botón **DAX Audio** en la barra de herramientas.

## Diseño de DAX Audio

La ventana de DAX Audio contiene controles para habilitar el puente de audio DAX, ajustar la ganancia de RX por canal, la ganancia de TX y ver las asignaciones de slices.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Habilitar DAX** | desactivado | activado/desactivado | `AutoStartDAX` | Inicia el puente de audio DAX; emite `daxToggled`. La etiqueta del botón refleja el estado actual: "Enabled" cuando está activo, "Disabled" cuando está desactivado. Interruptor maestro para todas las transmisiones de RX y TX de DAX. |
| **Ganancia+medidor DAX 1** | 0.5 | 0.0–1.0 | `DaxRxGain1` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 1. Emite `daxRxGainChanged(1, g)` y se guarda. |
| **Ganancia+medidor DAX 2** | 0.5 | 0.0–1.0 | `DaxRxGain2` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 2. |
| **Ganancia+medidor DAX 3** | 0.5 | 0.0–1.0 | `DaxRxGain3` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 3. |
| **Ganancia+medidor DAX 4** | 0.5 | 0.0–1.0 | `DaxRxGain4` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 4. |
| **Ganancia+medidor TX** | 0.5 | 0.0–1.0 | `DaxTxGain` | Medidor/control deslizante combinado para la transmisión de TX de DAX. |

### Indicadores de asignación de slices

Cada canal DAX muestra qué slice (si hay alguno) está actualmente enrutado a él.

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| **Asignación DAX 1** | —, Slice A..H | El slice (si hay alguno) asignado actualmente a este canal DAX. |
| **Asignación DAX 2** | —, Slice A..H | El slice (si hay alguno) asignado actualmente a este canal DAX. |
| **Asignación DAX 3** | —, Slice A..H | El slice (si hay alguno) asignado actualmente a este canal DAX. |
| **Asignación DAX 4** | —, Slice A..H | El slice (si hay alguno) asignado actualmente a este canal DAX. |
| **Asignación TX** | —, Slice A..H | El slice que actualmente tiene privilegios de TX (impulsa DAX TX). |

### Comportamiento en plataforma Windows

En Windows, el applet DAX Audio solo muestra una nota informativa: "No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX." No se construyen controles, medidores ni indicadores. Los establecedores de estado internos del applet (`setDaxEnabled`, `setDaxRxLevel`, `setDaxTxLevel`) están protegidos y no hacen nada.

# Control CAT

El applet **CAT Control** ejecuta hasta cuatro servidores TCP compatibles con `rigctld` (y enlaces simbólicos PTY en Linux/macOS) para que el software externo de registro y concurso pueda controlar un slice por canal. AetherSDR implementa un protocolo nativo Hamlib NET `rigctl`, eliminando la necesidad de un puente `rigctld` independiente.

## Abrir Control CAT

Haga clic en el botón **CAT Control** en la barra de herramientas, o presione `Ctrl+Shift+C`.

## Diseño de Control CAT

La ventana de Control CAT contiene controles para habilitar servidores TCP y TTY, configurar el puerto base y monitorear el estado por canal.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Habilitar TCP** | desactivado | activado/desactivado | `CatTcpPort` | Inicia/detiene los cuatro servidores TCP `rigctld` en `Base..Base+3`. También guarda el puerto base actual. |
| **Habilitar TTY** | desactivado | activado/desactivado | — | Inicia/detiene los cuatro enlaces simbólicos PTY en `$XDG_RUNTIME_DIR/aethersdr/cat-A..D` (Linux) o `~/Library/Caches/AetherSDR/cat-A..D` (macOS). |
| **Base** | 4532 | 1024–65535 | `CatTcpPort` | Puerto TCP base; los canales se vinculan al puerto, puerto+1, puerto+2, puerto+3. Los valores fuera de rango vuelven a 4532; los servidores se reinician con el nuevo puerto si están habilitados actualmente. |

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
- `:<puerto> (1 cliente)` cuando hay un cliente conectado
- `:<puerto> (N clientes)` cuando hay varios clientes conectados

La **Ruta PTY** muestra la ruta del enlace simbólico que el software de registro puede abrir como dispositivo serie:
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

El diálogo SpotHub contiene una interfaz de múltiples pestañas. Cada pestaña de fuente proporciona controles de conexión, una consola de datos y un selector de color de spots. Una pestaña separada **Display** controla la visualización de spots en el panadapter, los ajustes de Signal History y el coloreado por DXCC.

### Pestaña Cluster

La pestaña **Cluster** proporciona una conexión telnet a un DX cluster.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Servidor:** | — | — | `ClusterHost` | Nombre de host del DX cluster al que conectarse. |
| **Puerto:** | — | 1–65535 | `ClusterPort` | Puerto telnet en el DX cluster. |
| **Callsign:** | — | — | `ClusterCallsign` | Callsign de inicio de sesión enviado al cluster. |
| **Conectar / Desconectar** | Conectar | — | — | Alterna la conexión telnet al cluster. |
| **Auto-conectar al inicio** | — | — | `ClusterAutoConnect` | Conecta automáticamente el cluster al iniciar. |
| **Consola Cluster** | — | — | — | Consola telnet de solo lectura del tráfico bruto del cluster. |
| **Enviar** | — | — | — | Envía un comando escrito al cluster. |
| **Color de spots:** | — | — | `ClusterSpotColor` | Abre un selector de color para los spots del cluster. |

### Pestaña RBN

La pestaña **RBN** proporciona una fuente telnet de Reverse Beacon Network con limitación de velocidad.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Servidor:** | — | — | `RbnHost` | Nombre de host telnet de RBN. |
| **Puerto:** | — | 1–65535 | `RbnPort` | Puerto telnet de RBN. |
| **Callsign:** | — | — | `RbnCallsign` | Callsign de inicio de sesión para RBN. |
| **Límite de velocidad:** | — | — | `RbnRateLimit` | Limita los spots de RBN por segundo. |
| **Conectar / Desconectar (RBN)** | Conectar | — | — | Alterna la conexión RBN. |
| **Auto-conectar al inicio (RBN)** | — | — | `RbnAutoConnect` | Inicia RBN automáticamente. |
| **Consola RBN** | — | — | — | Consola de solo lectura del tráfico de RBN. |
| **Enviar (RBN)** | — | — | — | Envía un comando a RBN. |
| **Color de spots: (RBN)** | — | — | `RbnSpotColor` | Selector de color para spots de RBN. |

### Pestaña WSJT-X

La pestaña **WSJT-X** proporciona un listener UDP para decodificaciones de WSJT-X con filtros y colores.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Dirección:** | — | — | `WsjtxAddress` | Dirección de vinculación UDP para mensajes de WSJT-X. |
| **Puerto:** | — | 1–65535 | `WsjtxPort` | Puerto UDP para WSJT-X. |
| **Iniciar / Detener** | — | — | — | Inicia o detiene el listener UDP. |
| **Auto-iniciar al inicio (WSJT-X)** | — | — | `WsjtxAutoStart` | Inicia automáticamente el listener al arrancar. |
| **CQ** | — | — | `WsjtxFilterCQ` | Mostrar solo llamadas CQ de WSJT-X. |
| **CQ POTA** | — | — | `WsjtxFilterPOTA` | Mostrar llamadas CQ POTA. |
| **Llamándome** | — | — | `WsjtxFilterCallingMe` | Mostrar solo decodificaciones dirigidas a su callsign. |
| **Color CQ / color POTA / color Llamándome / color predeterminado** | — | — | `WsjtxColorCQ` / `WsjtxColorPOTA` / `WsjtxColorCallingMe` / `WsjtxColorDefault` | Selectores de color para cada categoría de spot de WSJT-X. |
| **Decodificaciones WSJT-X** | — | — | — | Consola de transmisiones decodificadas. |
| **Vida del spot:** | — | — | `WsjtxSpotLife` | Segundos que los spots de WSJT-X permanecen en el panadapter. |

### Pestaña SpotCollector

La pestaña **SpotCollector** proporciona un listener UDP para las transmisiones de SpotCollector de Ham Radio Deluxe.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Puerto UDP:** | — | 1–65535 | `SpotCollectorPort` | Puerto UDP en el que SpotCollector transmite. |
| **Iniciar / Detener (SpotCollector)** | — | — | — | Inicia o detiene el listener UDP. |
| **Auto-iniciar al inicio (SpotCollector)** | — | — | `SpotCollectorAutoStart` | Inicia automáticamente el listener al arrancar. |
| **Spots SpotCollector** | — | — | — | Consola de spots recibidos de SpotCollector. |

### Pestaña POTA

La pestaña **POTA** consulta api.pota.app para obtener activaciones actuales.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Servidor:** | api.pota.app (sondeo HTTP) | — | — | Muestra el punto final POTA fijo. |
| **Intervalo de sondeo:** | — | — | `PotaPollInterval` | Segundos entre sondeos de POTA. |
| **Iniciar / Detener (POTA)** | — | — | — | Inicia o detiene el sondeo de POTA. |
| **Auto-iniciar al inicio (POTA)** | — | — | `PotaAutoStart` | Inicia automáticamente POTA al arrancar. |
| **Activaciones POTA** | — | — | — | Consola del feed de activaciones. |
| **Color de spots: (POTA)** | — | — | `PotaSpotColor` | Selector de color para spots de POTA. |

### Pestaña FreeDV

La pestaña **FreeDV** proporciona un feed WebSocket de spots del reportero QSO de FreeDV. Esta pestaña solo está disponible cuando AetherSDR se compila con soporte WebSocket.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------|-------|-------------|----------|
| **Servidor:** | qso.freedv.org (WebSocket) | — | — | Muestra el punto final FreeDV fijo. |
| **Iniciar / Detener (FreeDV)** | — | — | — | Conecta o desconecta el WebSocket de FreeDV. |
