# Habilitar CAT PTY para que aplicaciones en Linux/macOS puedan abrir un puerto CAT de tipo serie

CAT PTY crea cuatro enlaces simbólicos de puertos serie virtuales que los programas de registro y concurso pueden abrir como si fueran dispositivos serie físicos. Use esta función en Linux o macOS cuando su aplicación externa espera una ruta de puerto serie en lugar de una conexión TCP.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Control CAT requiere una conexión de radio activa.
- La función PTY solo está disponible en Linux y macOS.
- Abra el applet de Control CAT haciendo clic en el botón de bandeja **CAT** de la barra lateral derecha. El applet está oculto por defecto.

## Pasos

1. Haga clic en el botón de bandeja **CAT** de la barra lateral derecha para abrir el applet de Control CAT.
2. Haga clic en **Enable TTY**.

   El botón se vuelve verde cuando está activo. AetherSDR crea cuatro enlaces simbólicos:

   ```
   /tmp/AetherSDR-CAT-A
   /tmp/AetherSDR-CAT-B
   /tmp/AetherSDR-CAT-C
   /tmp/AetherSDR-CAT-D
   ```

3. En su aplicación externa, configure la ruta del puerto serie al enlace simbólico del canal que desea controlar — por ejemplo, `/tmp/AetherSDR-CAT-A` para el canal A.
4. Cada fila de canal en el applet se actualiza para mostrar la ruta PTY activa una vez que el enlace simbólico está en ejecución.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TTY** | Off | On / Off | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D`. |
| **Enable TCP** | Off | On / Off | — | Inicia o detiene los cuatro servidores TCP rigctld. Al alternar también se persiste el puerto base en `CatTcpPort`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Puerto TCP base para los servidores TCP. Los valores fuera del rango válido se revierten a `4532`. No afecta las rutas PTY. |
| Filas de canal A/B/C/D | `(stopped)` | — | — | Cada fila muestra una insignia de canal con código de color, el estado del servidor TCP y la ruta del enlace simbólico PTY para ese canal. |

## Consejos

- Cada canal (A, B, C, D) se asigna a una slice de radio. Apunte su programa de registro al enlace simbólico que corresponda a la slice que desea que controle.
- Para que AetherSDR inicie los enlaces simbólicos PTY automáticamente al arrancar, habilite `Settings > Autostart CAT with AetherSDR`.
- Puede ejecutar **Enable TTY** y **Enable TCP** de forma independiente. Habilitar uno no requiere habilitar el otro.

## Solución de problemas

- **Enable TTY no tiene efecto o los enlaces simbólicos no aparecen** — La compatibilidad con PTY requiere Linux o macOS. Esta función no está disponible en Windows.
- **La aplicación externa no puede abrir el puerto** — Confirme que la aplicación está usando la ruta completa, por ejemplo `/tmp/AetherSDR-CAT-A`. Verifique que **Enable TTY** siga activo (el botón debe estar verde) y que AetherSDR permanezca conectado a la radio.
- **La ruta del enlace simbólico mostrada en la fila no coincide con `/tmp/AetherSDR-CAT-A`** — La ruta mostrada se actualiza a la ruta real del dispositivo PTY una vez que el enlace simbólico está en ejecución. Use la ruta que se muestre en la fila del canal, no el texto de ejemplo.

## Relacionados

- [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Autostart CAT servers with AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [CAT Control overview](overview.md)
- [Check how many external clients are connected to each channel](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
