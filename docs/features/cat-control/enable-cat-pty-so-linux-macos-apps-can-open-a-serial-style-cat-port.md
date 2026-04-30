# Habilitar CAT PTY para que aplicaciones Linux/macOS abran un puerto CAT de estilo serie

CAT PTY crea cuatro enlaces simbólicos de puerto serie virtual que el software de registro y contienda puede abrir como si fueran dispositivos serie físicos. Use esta función en Linux o macOS cuando su aplicación externa espera una ruta de puerto serie en lugar de una conexión TCP.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT Control requiere una conexión activa a la radio.
- La función PTY está disponible solo en Linux y macOS.
- Abra el applet CAT Control haciendo clic en el botón **CAT** en la bandeja de la derecha. El applet está oculto por defecto.

## Pasos

1. Haga clic en el botón **CAT** en la bandeja de la derecha para abrir el applet CAT Control.
2. Haga clic en **Enable TTY**.

   El botón se vuelve verde cuando está activo. AetherSDR crea cuatro enlaces simbólicos:

   ```
   /tmp/AetherSDR-CAT-A
   /tmp/AetherSDR-CAT-B
   /tmp/AetherSDR-CAT-C
   /tmp/AetherSDR-CAT-D
   ```

3. En su aplicación externa, establezca la ruta del puerto serie en el enlace simbólico del canal que desea controlar — por ejemplo, `/tmp/AetherSDR-CAT-A` para el canal A.
4. Cada fila de canal en el applet se actualiza para mostrar la ruta PTY activa una vez que el enlace simbólico está en ejecución.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| **Enable TTY** | Off | On / Off | — | Inicia o detiene los cuatro enlaces simbólicos PTY bajo `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D`. |
| **Enable TCP** | Off | On / Off | — | Inicia o detiene los cuatro servidores TCP rigctld. Cambiar también persiste el puerto base a `CatTcpPort`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Puerto TCP base para los servidores TCP. Los valores fuera del rango válido vuelven a `4532`. No afecta las rutas PTY. |
| Filas de canal A/B/C/D | `(stopped)` | — | — | Cada fila muestra una insignia de canal codificada por color, el estado del servidor TCP y la ruta del enlace simbólico PTY para ese canal. |

## Consejos

- Cada canal (A, B, C, D) se asigna a un slice de radio. Apunte su software de registro al enlace simbólico que corresponda al slice que desea controlar.
- Para que AetherSDR inicie automáticamente los enlaces simbólicos PTY al lanzarse, habilite `Settings > Autostart CAT with AetherSDR`.
- Puede ejecutar **Enable TTY** y **Enable TCP** de forma independiente. Habilitar uno no requiere habilitar el otro.

## Solución de problemas

- **Enable TTY no tiene efecto o los enlaces simbólicos no aparecen** — El soporte PTY requiere Linux o macOS. La función no está disponible en Windows.
- **La aplicación externa no puede abrir el puerto** — Confirme que la aplicación está usando la ruta completa, por ejemplo `/tmp/AetherSDR-CAT-A`. Verifique que **Enable TTY** siga activo (el botón debe estar verde) y que AetherSDR permanezca conectado a la radio.
- **La ruta del enlace simbólico mostrada en la fila no coincide con `/tmp/AetherSDR-CAT-A`** — La ruta mostrada se actualiza a la ruta del dispositivo PTY real una vez que el enlace simbólico está en ejecución. Use cualquier ruta que se muestre en la fila del canal, no el marcador de posición.

## Relacionado

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X controlen la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Autostart CAT servers with AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [CAT Control overview](overview.md)
- [Check how many external clients are connected to each channel](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
