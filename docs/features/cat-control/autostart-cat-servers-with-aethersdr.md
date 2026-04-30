# Iniciar automáticamente servidores CAT con AetherSDR

Configure AetherSDR para que inicie automáticamente los servidores TCP de rigctld y/o puertos seriales virtuales PTY cada vez que la aplicación se abre, de modo que el software de logging y competencia externo esté listo sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que los servidores CAT puedan funcionar. La configuración de autostart se guarda de todas formas, pero los servidores solo se activan una vez que se establece la conexión con la radio.
- Decida si necesita TCP, PTY (solo Linux/macOS), o ambos. TCP funciona en todas las plataformas; PTY es para aplicaciones que esperan una ruta de dispositivo serial como `/tmp/AetherSDR-CAT-A`.

## Pasos

### Habilitar autostart para servidores TCP

1. Abra `Settings > Autostart rigctld with AetherSDR`.
2. Haga clic en el elemento para colocar una marca de verificación junto a él.

AetherSDR ahora iniciará automáticamente los cuatro servidores TCP de rigctld en el próximo lanzamiento. Se utiliza el puerto base persistente en `CatTcpPort` (predeterminado `4532`); los canales se vinculan a puerto, puerto+1, puerto+2 y puerto+3.

### Habilitar autostart para puertos seriales virtuales PTY

1. Abra `Settings > Autostart CAT with AetherSDR`.
2. Haga clic en el elemento para colocar una marca de verificación junto a él.

AetherSDR ahora creará automáticamente los enlaces simbólicos PTY bajo `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D` en el próximo lanzamiento.

### Verificar la sesión actual sin reiniciar

Si desea que los servidores se ejecuten inmediatamente en la sesión actual también:

1. Haga clic en el botón `CAT` de la bandeja en la barra lateral derecha para abrir el applet CAT Control.
2. Haga clic en `Enable TCP` para iniciar ahora los servidores TCP.
3. Haga clic en `Enable TTY` para iniciar ahora los enlaces simbólicos PTY (solo Linux/macOS).

Las filas de canales (A, B, C, D) se actualizarán de `(stopped)` a `:<puerto> (0 clientes)` a medida que cada servidor se levante.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|---|
| `Enable TCP` | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP de rigctld en Base a Base+3. También persiste el puerto base actual a `CatTcpPort`. |
| `Enable TTY` | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY bajo `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D`. |
| `Base` | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los valores fuera de rango se ajustan a `4532`. Si los servidores TCP ya se están ejecutando, se reinician en el nuevo puerto inmediatamente. |
| Filas de canal A/B/C/D | Indicador | `(stopped)` | — | — | Muestra la insignia del canal, estado TCP (puerto y número de clientes) y ruta PTY para cada uno de los cuatro canales. Las insignias de canal están codificadas por color usando el color de slice asignado a ese canal. |

## Consejos

- El botón de alternancia `Enable TCP` en el applet refleja la configuración `AutoStartRigctld`. El botón de alternancia `Enable TTY` refleja la configuración `AutoStartCAT`. Alternar cualquiera de los botones en el applet actualiza la preferencia de autostart al mismo tiempo, por lo que puede usar los botones del applet en lugar del menú Settings si lo prefiere.
- Si cambia el puerto `Base` después de habilitar autostart, el nuevo puerto se guarda en `CatTcpPort` y los servidores en ejecución se reinician en la nueva base inmediatamente. El valor guardado también se utiliza en el próximo autostart.

## Solución de problemas

- **Los servidores no se inician después del lanzamiento aunque autostart esté habilitado** — La radio debe estar conectada antes de que los servidores se activen. Confirme el estado de la conexión en la barra de título e intente nuevamente una vez conectado.
- **Los enlaces simbólicos PTY no aparecen** — El autostart `Enable TTY` solo funciona en Linux y macOS. En Windows, `Enable TTY` no tiene efecto.
- **Puerto ya en uso** — Si otra aplicación ocupa un puerto en el rango Base–Base+3, el servidor correspondiente fallará silenciosamente. Cambie el valor `Base` en el applet CAT Control a un rango de puertos no utilizado y vuelva a habilitar TCP.
- **Los colores de insignia de canal aparecen incorrectos** — Los colores de slice se gestionan dinámicamente. Si las insignias muestran colores inesperados, desconecte y reconnecte a la radio para que se actualicen las asignaciones de color de slice.

## Relacionado

- [Descripción general de CAT Control](overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serial](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
