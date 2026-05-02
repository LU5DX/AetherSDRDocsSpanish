# Habilitar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de tipo serial

CAT PTY crea cuatro enlaces simbólicos de puertos seriales virtuales que el software de registro y de concursos puede abrir como si fueran dispositivos seriales físicos. Use esta función en Linux o macOS cuando su aplicación externa espere una ruta de puerto serial en lugar de una conexión TCP.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT Control requiere una conexión de radio activa.
- La función PTY está disponible únicamente en Linux y macOS.
- Abra el applet CAT Control haciendo clic en el botón **CAT** de la barra lateral derecha. El applet está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha para abrir el applet CAT Control.
2. Haga clic en **Enable TTY**.

   El botón se pone verde cuando está activo. AetherSDR crea cuatro enlaces simbólicos:

   ```
   /tmp/AetherSDR-CAT-A
   /tmp/AetherSDR-CAT-B
   /tmp/AetherSDR-CAT-C
   /tmp/AetherSDR-CAT-D
   ```

3. En su aplicación externa, establezca la ruta del puerto serial al enlace simbólico del canal que desea controlar — por ejemplo, `/tmp/AetherSDR-CAT-A` para el canal A.
4. Cada fila de canal en el applet se actualiza para mostrar la ruta PTY activa una vez que el enlace simbólico está en funcionamiento.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TTY** | Desactivado | Activado / Desactivado | — | Inicia o detiene los cuatro enlaces simbólicos PTY bajo `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. |
| **Enable TCP** | Desactivado | Activado / Desactivado | — | Inicia o detiene los cuatro servidores TCP rigctld. Al alternarlo también se persiste el puerto base en `CatTcpPort`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Puerto TCP base para los servidores TCP. Los valores fuera del rango válido vuelven automáticamente a `4532`. No afecta las rutas PTY. |
| Filas de canal A/B/C/D | `(stopped)` | — | — | Cada fila muestra una insignia de canal con código de color, el estado del servidor TCP y la ruta del enlace simbólico PTY para ese canal. |

## Consejos

- Cada canal (A, B, C, D) corresponde a un slice de radio. Apunte su software de registro al enlace simbólico que corresponda al slice que desea controlar.
- Para que AetherSDR inicie los enlaces simbólicos PTY automáticamente al arrancar, habilite `Settings > Autostart CAT with AetherSDR`.
- Puede ejecutar **Enable TTY** y **Enable TCP** de forma independiente. Habilitar uno no requiere habilitar el otro.

## Solución de problemas

- **Enable TTY no tiene efecto o los enlaces simbólicos no aparecen** — La compatibilidad con PTY requiere Linux o macOS. La función no está disponible en Windows.
- **La aplicación externa no puede abrir el puerto** — Confirme que la aplicación utiliza la ruta completa, por ejemplo `/tmp/AetherSDR-CAT-A`. Verifique que **Enable TTY** sigue activo (el botón debe estar verde) y que AetherSDR permanece conectado a la radio.
- **La ruta del enlace simbólico mostrada en la fila no coincide con `/tmp/AetherSDR-CAT-A`** — La ruta mostrada se actualiza a la ruta real del dispositivo PTY una vez que el enlace simbólico está en funcionamiento. Use la ruta que se muestre en la fila del canal, no el valor provisional.

## Relacionado

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Descripción general de CAT Control](overview.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
