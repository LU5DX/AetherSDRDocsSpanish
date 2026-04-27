# Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT de tipo serial

CAT PTY crea cuatro enlaces simbólicos de puerto serie virtual que los programas de registro y concurso pueden abrir como si fueran dispositivos seriales físicos. Use esta función en Linux o macOS cuando su aplicación externa espere una ruta de puerto serie en lugar de una conexión TCP.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT Control requiere una conexión activa con el radio.
- La función PTY está disponible únicamente en Linux y macOS.
- Abra el applet CAT Control haciendo clic en el botón **CAT** de la barra lateral derecha. El applet está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha para abrir el applet CAT Control.
2. Haga clic en **Enable TTY**.

   El botón se vuelve verde cuando está activo. AetherSDR crea cuatro enlaces simbólicos:

   ```
   /tmp/AetherSDR-CAT-A
   /tmp/AetherSDR-CAT-B
   /tmp/AetherSDR-CAT-C
   /tmp/AetherSDR-CAT-D
   ```

3. En su aplicación externa, establezca la ruta del puerto serie al enlace simbólico del canal que desea controlar — por ejemplo, `/tmp/AetherSDR-CAT-A` para el canal A.
4. Cada fila de canal en el applet se actualiza para mostrar la ruta PTY activa una vez que el enlace simbólico está en funcionamiento.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TTY** | Apagado | Encendido / Apagado | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. |
| **Enable TCP** | Apagado | Encendido / Apagado | — | Inicia o detiene los cuatro servidores TCP rigctld. Al cambiar el estado también se guarda el puerto base en `CatTcpPort`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Puerto TCP base para los servidores TCP. Los valores fuera del rango válido vuelven automáticamente a `4532`. No afecta las rutas PTY. |
| Filas de canales A/B/C/D | `(detenido)` | — | — | Cada fila muestra una insignia de canal con código de color, el estado del servidor TCP y la ruta del enlace simbólico PTY para ese canal. |

## Consejos

- Cada canal (A, B, C, D) corresponde a un slice de radio. Apunte su programa de registro al enlace simbólico que corresponde al slice que desea controlar.
- Para que AetherSDR inicie los enlaces simbólicos PTY automáticamente al arrancar, habilite `Settings > Autostart CAT with AetherSDR`.
- Puede ejecutar **Enable TTY** y **Enable TCP** de forma independiente. Habilitar uno no requiere habilitar el otro.

## Solución de problemas

- **Enable TTY no tiene efecto o los enlaces simbólicos no aparecen** — La compatibilidad con PTY requiere Linux o macOS. La función no está disponible en Windows.
- **La aplicación externa no puede abrir el puerto** — Confirme que la aplicación esté usando la ruta completa, por ejemplo `/tmp/AetherSDR-CAT-A`. Verifique que **Enable TTY** siga activo (el botón debe estar verde) y que AetherSDR permanezca conectado al radio.
- **La ruta del enlace simbólico mostrada en la fila no coincide con `/tmp/AetherSDR-CAT-A`** — La ruta mostrada se actualiza a la ruta real del dispositivo PTY una vez que el enlace simbólico está en funcionamiento. Use la ruta que se muestre en la fila del canal, no el marcador de posición.

## Relacionado

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Descripción general de CAT Control](overview.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
