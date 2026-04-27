# Verificar cuántos clientes externos están conectados a cada canal

El applet CAT Control muestra el recuento de clientes en tiempo real para cada uno de los cuatro canales TCP de rigctld (A–D). Use esto para confirmar que su software de registro o de concurso se ha conectado correctamente al canal adecuado.

## Antes de comenzar

- El radio debe estar conectado. El applet CAT Control requiere una conexión de radio activa.
- Enable TCP debe estar activo. Si los servidores no están en ejecución, todos los canales muestran `(stopped)` y ningún cliente puede conectarse. Consulte [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md).

## Pasos

1. Haga clic en el botón de bandeja **CAT** en la barra lateral derecha para abrir el applet CAT Control.
2. Lea la etiqueta de estado TCP en la fila de cada canal (A, B, C, D).

Cada fila muestra uno de los siguientes estados:

| Indicación | Significado |
|---|---|
| `(stopped)` | El servidor TCP de ese canal no está en ejecución. |
| `:<port> (0 clients)` | El servidor está en ejecución; ningún cliente externo está conectado. |
| `:<port> (1 client)` | Un cliente externo está conectado en ese puerto. |
| `:<port> (N clients)` | N clientes externos están conectados en ese puerto. |

El puerto que se muestra es el puerto base para el canal A, base+1 para B, base+2 para C y base+3 para D. El puerto base predeterminado es `4532` (persistido como `CatTcpPort`).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TCP** | Desactivado | Activado / Desactivado | — | Inicia o detiene los cuatro servidores TCP de rigctld. También guarda el puerto base actual en `CatTcpPort`. |
| **Enable TTY** | Desactivado | Activado / Desactivado | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales se vinculan a base, base+1, base+2, base+3. Los valores fuera del rango válido vuelven a `4532`. Si los servidores están en ejecución, se reinician en los nuevos puertos de inmediato. |
| Filas de canales A/B/C/D | `(stopped)` | — | — | Cada fila muestra la insignia de color del slice (canal de recepción), el estado TCP con el recuento de clientes y la ruta PTY. Se actualiza en tiempo real cuando los clientes se conectan o desconectan. |

## Consejos

- La etiqueta de estado TCP cambia de color cuando hay un cliente conectado: adopta el color del slice de ese canal, lo que facilita identificar de un vistazo qué canales están en uso.
- Si cambia el valor en **Base** mientras los servidores están en ejecución, los cuatro servidores se reinician automáticamente en los nuevos puertos. Los clientes conectados serán desconectados y deberán reconectarse.

## Solución de problemas

- **Todas las filas muestran `(stopped)` aunque Enable TCP esté activo** — Es posible que se haya perdido la conexión del radio. Verifique que AetherSDR esté conectado al FLEX-8600 y luego desactive y vuelva a activar **Enable TCP**.
- **El recuento de clientes permanece en 0 después de iniciar el software de registro** — Confirme que el software apunta al puerto correcto. El canal A usa el puerto base (`4532` de forma predeterminada), B usa base+1, y así sucesivamente. Verifique el valor en el campo **Base** y compárelo con el puerto configurado en su software.
- **El servidor no logra iniciarse en el puerto seleccionado** — Es posible que otra aplicación ya esté escuchando en ese puerto. Cambie el valor de **Base** a un rango de puertos libre y haga clic en **Enable TCP** nuevamente.

## Temas relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Cambiar el puerto TCP base](../../features/cat-control/change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
