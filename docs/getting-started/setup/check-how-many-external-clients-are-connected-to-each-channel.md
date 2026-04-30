# Verifique cuántos clientes externos están conectados a cada canal

El applet CAT Control muestra un recuento de clientes activos para cada uno de los cuatro canales TCP rigctld (A–D). Úselo para confirmar que su software de registro o concurso se ha conectado exitosamente al canal correcto.

## Antes de comenzar

- La radio debe estar conectada. El applet CAT Control requiere una conexión de radio activa.
- Enable TCP debe estar activo. Si los servidores no se están ejecutando, todos los canales muestran `(stopped)` y ningún cliente puede conectarse. Consulte [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md).

## Pasos

1. Haga clic en el botón **CAT** de la bandeja en la barra lateral derecha para abrir el applet CAT Control.
2. Lea la etiqueta de estado TCP en cada fila de canal (A, B, C, D).

Cada fila muestra uno de los siguientes estados:

| Pantalla | Significado |
|---|---|
| `(stopped)` | El servidor TCP para ese canal no se está ejecutando. |
| `:<port> (0 clients)` | El servidor se está ejecutando; no hay cliente externo conectado. |
| `:<port> (1 client)` | Un cliente externo está conectado en ese puerto. |
| `:<port> (N clients)` | N clientes externos están conectados en ese puerto. |

El puerto mostrado es el puerto base para el canal A, base+1 para B, base+2 para C y base+3 para D. El puerto base predeterminado es `4532` (persistente como `CatTcpPort`).

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| **Enable TCP** | Off | On / Off | — | Inicia o detiene los cuatro servidores TCP rigctld. También guarda el puerto base actual en `CatTcpPort`. |
| **Enable TTY** | Off | On / Off | — | Inicia o detiene los cuatro enlaces PTY en `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales se vinculan a base, base+1, base+2, base+3. Los valores fuera del rango válido vuelven a `4532`. Si los servidores se están ejecutando, se reinician en los nuevos puertos inmediatamente. |
| Filas de canal A/B/C/D | `(stopped)` | — | — | Cada fila muestra la insignia de color del slice, el estado TCP con recuento de clientes y la ruta PTY. Se actualiza en vivo cuando los clientes se conectan o desconectan. |

## Consejos

- La etiqueta de estado TCP cambia de color cuando un cliente está conectado: adopta el color del slice para ese canal, facilitando identificar de un vistazo qué canales están en uso.
- Si cambia el valor en **Base** mientras los servidores se están ejecutando, los cuatro servidores se reinician automáticamente en los nuevos puertos. Cualquier cliente conectado se desconectará y deberá reconectarse.

## Solución de problemas

- **Todas las filas muestran `(stopped)` aunque Enable TCP esté activo** — Es posible que la conexión de radio se haya perdido. Verifique que AetherSDR esté conectado al FLEX-8600 y luego desactive y active nuevamente **Enable TCP**.
- **El recuento de clientes se mantiene en 0 después de iniciar su software de registro** — Confirme que el software apunta al puerto correcto. El canal A usa el puerto base (`4532` de forma predeterminada), B usa base+1, y así sucesivamente. Verifique el valor en el campo **Base** y compárelo con lo que su software está configurado para conectarse.
- **El servidor no se inicia en el puerto seleccionado** — Otra aplicación puede estar escuchando en ese puerto. Cambie el valor de **Base** a un rango de puertos libre y haga clic en **Enable TCP** nuevamente.

## Relacionado

- [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Change the base TCP port](../../features/cat-control/change-the-base-tcp-port.md)
- [Autostart CAT servers with AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Enable CAT PTY so Linux/macOS apps can open a serial-style CAT port](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [See how many TCI clients are connected](see-how-many-tci-clients-are-connected.md)
