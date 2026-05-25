# Control CAT

El applet **CAT Control** ejecuta hasta cuatro servidores TCP compatibles con `rigctld` (y enlaces simbólicos PTY en Linux/macOS), de modo que el software externo de registro y concurso pueda controlar un slice por canal. AetherSDR implementa un protocolo nativo Hamlib NET `rigctl`, eliminando la necesidad de un puente `rigctld` independiente.

## Abrir Control CAT

Haga clic en el botón **CAT Control** de la barra de herramientas, o presione `Ctrl+Shift+C`.

## Disposición del Control CAT

La ventana Control CAT contiene controles para habilitar los servidores TCP y TTY, configurar el puerto base y supervisar el estado por canal.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------------|-------|------------------------|----------------|
| **Enable TCP** | desactivado | activado/desactivado | `CatTcpPort` | Inicia/detiene los cuatro servidores TCP `rigctld` en `Base..Base+3`. También persiste el puerto base actual. |
| **Enable TTY** | desactivado | activado/desactivado | — | Inicia/detiene los cuatro enlaces simbólicos PTY en `$XDG_RUNTIME_DIR/aethersdr/cat-A..D` (Linux) o `~/Library/Caches/AetherSDR/cat-A..D` (macOS). |
| **Base** | 4532 | 1024–65535 | `CatTcpPort` | Puerto TCP base; los canales se vinculan a puerto, puerto+1, puerto+2, puerto+3. Los valores fuera de rango se revierten a 4532; los servidores se reinician con el nuevo puerto si están habilitados. |

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
- `:<puerto> (N clientes)` cuando hay múltiples clientes conectados

La **Ruta PTY** muestra la ruta del enlace simbólico que el software de registro puede abrir como dispositivo serie:
- Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D`
- macOS: `~/Library/Caches/AetherSDR/cat-A` a `cat-D`
- Muestra "detenido" cuando el servidor TTY no está en ejecución

## Notas de seguridad

En la versión v26.5.3, la ubicación del enlace simbólico PTY se movió de `/tmp` a directorios de ejecución por usuario para corregir una vulnerabilidad de enlaces simbólicos entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico de enlaces simbólicos mediante `symlink(.tmp) + rename(.tmp, final)` cierra la ventana TOCTOU.
