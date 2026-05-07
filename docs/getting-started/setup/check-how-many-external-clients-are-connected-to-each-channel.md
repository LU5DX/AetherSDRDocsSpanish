# Compruebe cuántos clientes externos están conectados a cada canal

El miniaplicativo CAT Control muestra un recuento en vivo de clientes para cada uno de los cuatro canales TCP de rigctld (A–D). Úselo para confirmar que su programa de registro o concurso se ha conectado correctamente al canal adecuado.

## Antes de comenzar

- El radio debe estar conectado. El miniaplicativo CAT Control requiere una conexión activa al radio.
- La opción Enable TCP debe estar activa. Si los servidores no están en ejecución, todos los canales mostrarán `(stopped)` y ningún cliente podrá conectarse. Consulte [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md).

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha para abrir el miniaplicativo CAT Control.
2. Lea la etiqueta de estado TCP en cada fila de canal (A, B, C, D).

Cada fila muestra uno de los siguientes estados:

| Visualización | Significado |
|---|---|
| `(stopped)` | El servidor TCP de ese canal no está en ejecución. |
| `:<puerto> (0 clients)` | El servidor está en ejecución; no hay ningún cliente externo conectado. |
| `:<puerto> (1 client)` | Hay un cliente externo conectado en ese puerto. |
| `:<puerto> (N clients)` | Hay N clientes externos conectados en ese puerto. |

El puerto mostrado es el puerto base para el canal A, base+1 para B, base+2 para C y base+3 para D. El puerto base predeterminado es `4532` (persistido como `CatTcpPort`).

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TCP** | Off | On / Off | — | Inicia o detiene los cuatro servidores TCP de rigctld. También guarda el puerto base actual en `CatTcpPort`. |
| **Enable TTY** | Off | On / Off | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales se vinculan a base, base+1, base+2, base+3. Los valores fuera del rango válido retroceden a `4532`. Si los servidores se están ejecutando, se reinician inmediatamente en los nuevos puertos. |
| Filas de canal A/B/C/D | `(stopped)` | — | — | Cada fila muestra la insignia de color del slice, el estado TCP con el recuento de clientes y la ruta PTY. Se actualiza en vivo a medida que los clientes se conectan o desconectan. |

## Consejos

- La etiqueta de estado TCP cambia de color cuando un cliente está conectado: adopta el color del slice para ese canal, lo que facilita identificar de un vistazo qué canales están en uso.
- Si cambia el valor en **Base** mientras los servidores están en ejecución, los cuatro servidores se reinician automáticamente en los nuevos puertos. Los clientes conectados se desconectarán y deberán reconectarse.

## Solución de problemas

- **Todas las filas muestran `(stopped)` aunque Enable TCP esté activado** — Es posible que se haya perdido la conexión con el radio. Verifique que AetherSDR esté conectado al FLEX-8600 y luego desactive y vuelva a activar **Enable TCP**.
- **El recuento de clientes se mantiene en 0 después de iniciar su programa de registro** — Confirme que el programa apunta al puerto correcto. El canal A usa el puerto base (`4532` por defecto), B usa base+1, y así sucesivamente. Verifique el valor en el campo **Base** y compárelo con el puerto configurado en su programa.
- **El servidor no puede iniciarse en el puerto seleccionado** — Es posible que otra aplicación ya esté escuchando en ese puerto. Cambie el valor de **Base** a un rango de puertos libre y haga clic en **Enable TCP** nuevamente.

## Relacionados

- [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Change the base TCP port](../../features/cat-control/change-the-base-tcp-port.md)
- [Autostart CAT servers with AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Enable CAT PTY so Linux/macOS apps can open a serial-style CAT port](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [See how many TCI clients are connected](see-how-many-tci-clients-are-connected.md)
