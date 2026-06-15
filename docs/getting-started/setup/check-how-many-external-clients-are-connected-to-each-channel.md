# Verificar cuántos clientes externos están conectados a cada canal

El applet CAT Control muestra un recuento en vivo de clientes para cada uno de los cuatro canales TCP de rigctld (A–D). Utilícelo para confirmar que su software de registro o de concurso se ha conectado correctamente al canal adecuado.

## Antes de comenzar

- La radio debe estar conectada. El applet CAT Control requiere una conexión activa con la radio.
- Enable TCP debe estar activo. Si los servidores no están en ejecución, todos los canales muestran `(stopped)` y ningún cliente puede conectarse. Consulte [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md).

## Pasos

1. Haga clic en el botón de la bandeja **CAT** en la barra lateral derecha para abrir el applet CAT Control.
2. Lea la etiqueta de estado TCP en cada fila de canal (A, B, C, D).

Cada fila muestra uno de los siguientes estados:

| Visualización | Significado |
|---|---|
| `(stopped)` | El servidor TCP para ese canal no está en ejecución. |
| `:<puerto> (0 clients)` | El servidor está en ejecución; no hay ningún cliente externo conectado. |
| `:<puerto> (1 client)` | Un cliente externo está conectado en ese puerto. |
| `:<puerto> (N clients)` | N clientes externos están conectados en ese puerto. |

El puerto mostrado es el puerto base para el canal A, base+1 para B, base+2 para C y base+3 para D. El puerto base predeterminado es `4532` (persistido como `CatTcpPort`).

## Función de cada control

| Control              | Predeterminado | Rango válido |
|----------------------|----------------|--------------|
| **Enable TCP**       | Off            | On / Off     |
| **Enable TTY**       | Off            | On / Off     |
| **Base**             | `4532`         | 1024–65535   |
| Filas de canal A/B/C/D | `(stopped)` | —            |
### Enable TCP

Inicia o detiene los cuatro servidores TCP de rigctld en el puerto base hasta base+3. También persiste el valor actual del puerto base en la configuración `CatTcpPort`.

### Enable TTY

Inicia o detiene los cuatro enlaces simbólicos PTY. En Linux, los enlaces simbólicos se crean en `$XDG_RUNTIME_DIR/aethersdr/cat-A` hasta `cat-D`. En macOS, se crean en `~/Library/Caches/AetherSDR/cat-A` hasta `cat-D`.

En v26.5.3, la ubicación de los enlaces simbólicos se trasladó de `/tmp` a directorios de tiempo de ejecución por usuario para corregir una vulnerabilidad de enlaces simbólicos entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico de enlaces simbólicos mediante `symlink(.tmp) + rename(.tmp, final)` cierra la ventana TOCTOU.

### Base

Puerto TCP base. Los canales se vinculan al puerto, puerto+1, puerto+2 y puerto+3. El valor predeterminado es `4532`. El rango válido es 1024–65535. Los valores fuera de rango se reajustan a `4532`. Los servidores se reinician con el nuevo puerto si están habilitados.

### Filas de canal A/B/C/D

Cada fila muestra:
- Una insignia de canal con el color del slice
- Estado TCP: `(stopped)`, `:<puerto> (1 client)` o `:<puerto> (N clients)`
- Ruta PTY que muestra la ubicación del enlace simbólico donde el software de registro puede abrir un dispositivo serie

## Consejos

- La etiqueta de estado TCP cambia de color cuando hay un cliente conectado: adopta el color del slice para ese canal, lo que facilita identificar de un vistazo qué canales están en uso.
- Si cambia el valor en **Base** mientras los servidores están en ejecución, los cuatro servidores se reinician automáticamente en los nuevos puertos. Los clientes conectados se desconectarán y deberán reconectarse.

## Solución de problemas

- **Todas las filas muestran `(stopped)` aunque Enable TCP esté activado** — Es posible que se haya perdido la conexión con la radio. Verifique que AetherSDR esté conectado a la FLEX-8600 y luego desactive y reactive **Enable TCP**.
- **El recuento de clientes se mantiene en 0 después de iniciar su software de registro** — Confirme que el software apunta al puerto correcto. El canal A usa el puerto base (`4532` por defecto), B usa base+1, y así sucesivamente. Verifique el valor en el campo **Base** y compárelo con el que su software tiene configurado para conectarse.
- **El servidor no puede iniciarse en el puerto seleccionado** — Otra aplicación podría ya estar escuchando en ese puerto. Cambie el valor de **Base** a un rango de puertos libre y haga clic en **Enable TCP** nuevamente.

## Relacionados

- [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Change the base TCP port](../../features/cat-control/change-the-base-tcp-port.md)
- [Autostart CAT servers with AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Enable CAT PTY so Linux/macOS apps can open a serial-style CAT port](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [See how many TCI clients are connected](see-how-many-tci-clients-are-connected.md)
