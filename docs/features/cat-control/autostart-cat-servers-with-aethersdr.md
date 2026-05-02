# Inicio automático de servidores CAT con AetherSDR

Configure AetherSDR para iniciar los servidores TCP de rigctld y/o los puertos serie virtuales PTY automáticamente cada vez que la aplicación se inicie, de modo que el software externo de registro y concursos esté listo sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que los servidores CAT puedan funcionar. La configuración de inicio automático se guarda de todas formas, pero los servidores solo se activan una vez que se establece la conexión con la radio.
- Decida si necesita TCP, PTY (solo Linux/macOS), o ambos. TCP funciona en todas las plataformas; PTY es para aplicaciones que esperan una ruta de dispositivo serie como `/tmp/AetherSDR-CAT-A`.

## Pasos

### Habilitar el inicio automático para los servidores TCP

1. Abra `Settings > Autostart rigctld with AetherSDR`.
2. Haga clic en el elemento para colocar una marca de verificación junto a él.

AetherSDR iniciará ahora los cuatro servidores TCP de rigctld automáticamente en el próximo lanzamiento. Se utiliza el puerto base almacenado en `CatTcpPort` (predeterminado `4532`); los canales se enlazan al puerto, puerto+1, puerto+2 y puerto+3.

### Habilitar el inicio automático para los puertos serie virtuales PTY

1. Abra `Settings > Autostart CAT with AetherSDR`.
2. Haga clic en el elemento para colocar una marca de verificación junto a él.

AetherSDR creará ahora los enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D` automáticamente en el próximo lanzamiento.

### Verificar la sesión actual sin reiniciar

Si desea que los servidores se ejecuten de inmediato en la sesión actual:

1. Haga clic en el botón `CAT` de la barra lateral derecha para abrir el applet CAT Control.
2. Haga clic en `Enable TCP` para iniciar los servidores TCP ahora.
3. Haga clic en `Enable TTY` para iniciar los enlaces simbólicos PTY ahora (solo Linux/macOS).

Las filas de canales (A, B, C, D) se actualizarán de `(stopped)` a `:<port> (0 clients)` a medida que cada servidor se inicie.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave almacenada | Comportamiento |
|---|---|---|---|---|---|
| `Enable TCP` | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP de rigctld en Base hasta Base+3. También guarda el puerto base actual en `CatTcpPort`. |
| `Enable TTY` | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. |
| `Base` | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera de rango vuelven automáticamente a `4532`. Si los servidores TCP ya están en ejecución, se reinician en el nuevo puerto de inmediato. |
| Filas de canales A/B/C/D | Indicador | `(stopped)` | — | — | Muestra la insignia del canal, el estado TCP (puerto y número de clientes) y la ruta PTY para cada uno de los cuatro canales. Las insignias de canal tienen código de colores según el color del slice asignado a ese canal. |

## Consejos

- El botón de alternancia `Enable TCP` en el applet refleja la configuración `AutoStartRigctld`. El botón de alternancia `Enable TTY` refleja la configuración `AutoStartCAT`. Al activar o desactivar cualquiera de los botones en el applet se actualiza también la preferencia de inicio automático, por lo que puede usar los botones del applet en lugar del menú Settings si lo prefiere.
- Si cambia el puerto `Base` después de habilitar el inicio automático, el nuevo puerto se guarda en `CatTcpPort` y los servidores en ejecución se reinician inmediatamente en la nueva base. El valor guardado también se utiliza en el siguiente inicio automático.

## Solución de problemas

- **Los servidores no se inician después del lanzamiento aunque el inicio automático esté habilitado** — La radio debe estar conectada antes de que los servidores se activen. Confirme el estado de la conexión en la barra de título y vuelva a intentarlo una vez conectado.
- **Los enlaces simbólicos PTY no aparecen** — El inicio automático `Enable TTY` solo funciona en Linux y macOS. En Windows, `Enable TTY` no tiene efecto.
- **Puerto en uso** — Si otra aplicación ocupa un puerto en el rango Base–Base+3, el servidor correspondiente fallará silenciosamente. Cambie el valor de `Base` en el applet CAT Control a un rango de puertos disponible y vuelva a habilitar TCP.
- **Los colores de las insignias de canal son incorrectos** — Los colores del slice se gestionan de forma dinámica. Si las insignias muestran colores inesperados, desconéctese y vuelva a conectarse a la radio para que las asignaciones de color del slice se actualicen.

## Relacionado

- [Descripción general de CAT Control](overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT de tipo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
