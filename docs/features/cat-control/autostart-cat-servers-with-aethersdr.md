# Inicio automático de servidores CAT con AetherSDR

Configure AetherSDR para que inicie los servidores TCP rigctld y/o los puertos serie virtuales PTY automáticamente cada vez que se inicie la aplicación, de modo que el software externo de registro y concurso esté listo sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que los servidores CAT puedan funcionar. La configuración de inicio automático se guarda independientemente, pero los servidores solo se activan una vez que se establece una conexión con la radio.
- Decida si necesita TCP, PTY (solo Linux/macOS), o ambos. TCP funciona en todas las plataformas; PTY es para aplicaciones que esperan una ruta de dispositivo serie.
- Las rutas de los enlaces simbólicos PTY se encuentran en directorios de ejecución por usuario por seguridad:
  - Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D`
  - macOS: `~/Library/Caches/AetherSDR/cat-A` a `cat-D`

## Pasos

### Habilitar el inicio automático para servidores TCP

1. Abra `Settings > Autostart rigctld with AetherSDR`.
2. Haga clic en el elemento para marcar la casilla junto a él.

AetherSDR iniciará ahora los cuatro servidores TCP rigctld automáticamente en el próximo inicio. Se utiliza el puerto base persistido en `CatTcpPort` (predeterminado `4532`); los canales se vinculan al puerto, puerto+1, puerto+2 y puerto+3.

### Habilitar el inicio automático para puertos serie virtuales PTY

1. Abra `Settings > Autostart CAT with AetherSDR`.
2. Haga clic en el elemento para marcar la casilla junto a él.

AetherSDR creará ahora los enlaces simbólicos PTY en las rutas de ejecución por usuario automáticamente en el próximo inicio:
- Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D`
- macOS: `~/Library/Caches/AetherSDR/cat-A` a `cat-D`

### Verificar la sesión actual sin reiniciar

Si desea que los servidores se ejecuten inmediatamente también en la sesión actual:

1. Haga clic en el botón de la bandeja `CAT` en la barra lateral derecha para abrir el applet de Control CAT.
2. Haga clic en `Enable TCP` para iniciar los servidores TCP ahora.
3. Haga clic en `Enable TTY` para iniciar los enlaces simbólicos PTY ahora (solo Linux/macOS).

Las filas de canales (A, B, C, D) se actualizarán de `(stopped)` a `:<puerto> (0 clients)` a medida que cada servidor se active. Cada fila de canal también muestra la ruta PTY actual.

## Qué hace cada control

| Control              | Tipo          | Predeterminado |
|----------------------|---------------|----------------|
| `Enable TCP`         | Botón de alternancia | Desactivado    |
| `Enable TTY`         | Botón de alternancia | Desactivado    |
| `Base`               | Campo de texto | `4532`        |
| Filas de canal A/B/C/D | Indicador     | `(stopped)`   |

El indicador de ruta PTY por canal muestra:
- `stopped` cuando no hay ningún PTY activo
- La ruta completa del enlace simbólico (p. ej., `/run/user/1000/aethersdr/cat-A` en Linux o `~/Library/Caches/AetherSDR/cat-A` en macOS) cuando el PTY está en ejecución

## Consejos

- La alternancia `Enable TCP` en el applet refleja la configuración `AutoStartRigctld`. La alternancia `Enable TTY` refleja la configuración `AutoStartCAT`. Alternar cualquiera de los botones en el applet actualiza la preferencia de inicio automático al mismo tiempo, por lo que puede usar los botones del applet en lugar del menú de Configuración si lo prefiere.
- Si cambia el puerto `Base` después de habilitar el inicio automático, el nuevo puerto se guarda en `CatTcpPort` y los servidores en ejecución se reinician en la nueva base inmediatamente. El valor guardado también se utiliza en el próximo inicio automático.
- En v26.5.3, AetherSDR incluye una implementación nativa de controlador Hamlib NET rigctl, eliminando la necesidad de un puente rigctld independiente. Los slices A–H exponen cada uno un TTY (ruta de ejecución por usuario) y un puerto TCP (4532–4539).
- La creación de enlaces simbólicos PTY utiliza reemplazo atómico (enlace simbólico + renombrar) para prevenir condiciones de carrera TOCTOU (GHSA-qxhr-cwrc-pvrm).

## Solución de problemas

- **Los servidores no se inician después del inicio aunque el inicio automático esté habilitado** — La radio debe estar conectada antes de que los servidores se activen. Confirme el estado de la conexión en la barra de título y vuelva a intentarlo una vez conectado.
- **Los enlaces simbólicos PTY no aparecen** — El inicio automático de `Enable TTY` solo funciona en Linux y macOS. En Windows, `Enable TTY` no tiene efecto. En Linux, verifique que `$XDG_RUNTIME_DIR` esté configurado (normalmente `/run/user/<uid>`).
- **Puerto ya en uso** — Si otra aplicación ocupa un puerto en el rango Base–Base+3, el servidor correspondiente fallará silenciosamente. Cambie el valor de `Base` en el applet de Control CAT a un rango de puertos no utilizado y vuelva a habilitar TCP.
- **Los colores de las insignias de canal parecen incorrectos** — Los colores de los slices se gestionan dinámicamente. Si las insignias muestran colores inesperados, desconéctese y vuelva a conectarse a la radio para que se actualicen las asignaciones de color de los slices.

## Relacionado

- [Descripción general del Control CAT](overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que las aplicaciones Linux/macOS puedan abrir un puerto CAT de tipo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
