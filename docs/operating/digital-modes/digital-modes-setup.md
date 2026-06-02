# Audio DAX

El applet **DAX Audio** muestra medidores de recepción por canal y controles deslizantes de ganancia para DAX 1-4, además de un medidor de transmisión único, con un interruptor maestro de habilitación que se guarda como `AutoStartDAX`. En la versión 0.9.7 (Linux), la latencia de RX de DAX se reduce de aproximadamente 400 ms a aproximadamente 200 ms mediante una ruta de origen nativa `pw_stream` de PipeWire, reemplazando el cliente PulseAudio anterior.

## Cómo abrir DAX Audio

Haga clic en el botón **DAX Audio** en la barra de herramientas.

## Disposición de DAX Audio

La ventana de DAX Audio contiene controles para habilitar el puente de audio DAX, ajustar la ganancia de RX por canal, la ganancia de TX y ver las asignaciones de slices.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **DAX Enable** | desactivado | activado/desactivado | `AutoStartDAX` | Inicia el puente de audio DAX; emite `daxToggled`. La etiqueta del botón es "Enable"; interruptor maestro para todos los flujos de RX y TX de DAX. |
| **DAX 1 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain1` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 1. Emite `daxRxGainChanged(1, g)` y se guarda. |
| **DAX 2 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain2` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 2. |
| **DAX 3 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain3` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 3. |
| **DAX 4 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain4` | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 4. |
| **TX gain+meter** | 0.5 | 0.0–1.0 | `DaxTxGain` | Medidor/control deslizante combinado para el flujo de TX de DAX. |

### Indicadores de asignación de slices

Cada canal DAX muestra qué slice (si hay alguno) está enrutado actualmente a él.

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| **DAX 1 assignment** | —, Slice A..H | El slice (si hay alguno) asignado actualmente a este canal DAX. |
| **DAX 2 assignment** | —, Slice A..H | El slice (si hay alguno) asignado actualmente a este canal DAX. |
| **DAX 3 assignment** | —, Slice A..H | El slice (si hay alguno) asignado actualmente a este canal DAX. |
| **DAX 4 assignment** | —, Slice A..H | El slice (si hay alguno) asignado actualmente a este canal DAX. |
| **TX assignment** | —, Slice A..H | El slice que posee actualmente los privilegios de TX (controla DAX TX). |

# Control CAT

El applet **CAT Control** ejecuta hasta cuatro servidores TCP compatibles con `rigctld` (y enlaces simbólicos PTY en Linux/macOS) para que el software externo de registro y concursos pueda controlar un slice por canal. AetherSDR implementa un protocolo nativo `rigctl` de Hamlib NET, eliminando la necesidad de un puente `rigctld` independiente.

## Cómo abrir CAT Control

Haga clic en el botón **CAT Control** en la barra de herramientas, o presione `Ctrl+Shift+C`.

## Disposición de CAT Control

La ventana de CAT Control contiene controles para habilitar los servidores TCP y TTY, configurar el puerto base y monitorear el estado por canal.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **Enable TCP** | desactivado | activado/desactivado | `CatTcpPort` | Inicia/detiene los cuatro servidores TCP `rigctld` en el puerto `Base..Base+3`. También guarda el puerto base actual. |
| **Enable TTY** | desactivado | activado/desactivado | — | Inicia/detiene los cuatro enlaces simbólicos PTY en `$XDG_RUNTIME_DIR/aethersdr/cat-A..D` (Linux) o `~/Library/Caches/AetherSDR/cat-A..D` (macOS). |
| **Base** | 4532 | 1024–65535 | `CatTcpPort` | Puerto base TCP; los canales se vinculan al puerto, puerto+1, puerto+2, puerto+3. Los valores fuera de rango vuelven a 4532; los servidores se reinician con el nuevo puerto si están habilitados actualmente. |

### Estado por canal

Cada canal (A/B/C/D) muestra su estado en una fila:

| Canal | Estado TCP | Ruta PTY |
|-------|------------|----------|
| **A** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **B** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **C** | (detenido) | Ruta al enlace simbólico o "detenido" |
| **D** | (detenido) | Ruta al enlace simbólico o "detenido" |

El **Estado TCP** muestra:
- `(detenido)` cuando el servidor no está en ejecución
- `:<puerto> (1 cliente)` cuando hay un cliente conectado
- `:<puerto> (N clientes)` cuando hay varios clientes conectados

La **Ruta PTY** muestra la ruta del enlace simbólico que el software de registro puede abrir como un dispositivo serie:
- Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D`
- macOS: `~/Library/Caches/AetherSDR/cat-A` a `cat-D`
- Muestra "detenido" cuando el servidor TTY no está en ejecución

## Notas de seguridad

En la versión 26.5.3, la ubicación del enlace simbólico PTY se trasladó de `/tmp` a directorios de ejecución por usuario para corregir una vulnerabilidad de enlace simbólico entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico de enlaces simbólicos mediante `symlink(.tmp) + rename(.tmp, final)` cierra la ventana TOCTOU.
