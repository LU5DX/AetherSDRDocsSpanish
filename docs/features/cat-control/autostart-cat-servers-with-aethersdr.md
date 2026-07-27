# Inicio automático de servidores CAT con AetherSDR

Configure AetherSDR para iniciar automáticamente los servidores TCP rigctld y/o puertos serie virtuales PTY cada vez que se inicie la aplicación, de modo que el software externo de registro y concurso esté listo sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que los servidores CAT puedan funcionar. La configuración de inicio automático se guarda independientemente, pero los servidores solo se activan una vez que se establece una conexión con la radio.
- Decida si necesita TCP, PTY (solo Linux/macOS) o ambos. TCP funciona en todas las plataformas; PTY es para aplicaciones que esperan una ruta de dispositivo serie.
- Las rutas de los enlaces simbólicos PTY se encuentran en directorios de ejecución por usuario por seguridad:
  - Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` hasta `cat-D`
  - macOS: `~/Library/Caches/AetherSDR/cat-A` hasta `cat-D`

## Pasos

### Habilitar inicio automático para servidores TCP

1. Abra `Settings > Autostart rigctld with AetherSDR`.
2. Haga clic en el elemento para marcar la casilla.

AetherSDR iniciará automáticamente los cuatro servidores TCP rigctld en el próximo inicio. Se utiliza el puerto base almacenado en `CatTcpPort` (predeterminado `4532`); los canales se enlazan al puerto, puerto+1, puerto+2 y puerto+3.

### Habilitar inicio automático para puertos serie virtuales PTY

1. Abra `Settings > Autostart CAT with AetherSDR`.
2. Haga clic en el elemento para marcar la casilla.

AetherSDR creará automáticamente los enlaces simbólicos PTY en las rutas de ejecución por usuario en el próximo inicio:
- Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` hasta `cat-D`
- macOS: `~/Library/Caches/AetherSDR/cat-A` hasta `cat-D`

### Verificar la sesión actual sin reiniciar

Si desea que los servidores se ejecuten inmediatamente también en la sesión actual:

1. Haga clic en el botón de la bandeja `CAT` en la barra lateral derecha para abrir el applet CAT Control.
2. Haga clic en el botón maestro `Enable` (etiquetado como `Disabled` de forma predeterminada) para iniciar todos los servidores CAT ahora. El texto del botón cambia a `Enabled` y las filas de los canales se vuelven editables.
3. En cada fila de canal que desee usar, haga clic en la casilla junto a la insignia del canal para habilitar el servidor TCP y/o el enlace simbólico PTY de ese canal.

Las filas de los canales (A, B, C, D) se actualizarán de `(stopped)` a `:<puerto> (0 clients)` a medida que cada servidor se active. Cada fila de canal también muestra la ruta PTY actual.

## Casillas de habilitación por canal

En la v26.7.4, cada fila de canal (A, B, C, D) obtuvo una casilla de habilitación individual. Estas casillas tienen un estilo de alto contraste que utiliza un color de acento relleno cuando están marcadas, lo que hace que el estado activado/desactivado sea legible de un vistazo sobre el fondo oscuro del applet.

- Cuando el botón maestro `Enable` está desactivado, todas las casillas por canal están deshabilitadas y los servidores se detienen.
- Cuando el botón maestro `Enable` está activado, puede habilitar o deshabilitar cada canal de forma independiente haciendo clic en su casilla.
- Cada casilla controla tanto el servidor TCP como el enlace simbólico PTY para ese canal simultáneamente.

## Descripción general del applet CAT Control

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld (y enlaces simbólicos PTY en Linux/macOS) para que el software externo de registro y concurso pueda controlar un slice por canal. Los slices A–H exponen cada uno un TTY (ruta de ejecución por usuario) y un puerto TCP (4532–4539).

## Función de cada control

| Control                     | Tipo           | Predeterminado | Clave de configuración | Notas |
|-----------------------------|----------------|----------------|------------------------|-------|
| Botón maestro `Enable`      | Botón de alternancia | `Disabled` | `CatEnabled` | Inicia/detiene todos los servidores CAT. El texto del botón cambia a `Enabled` cuando está activo. |
| Casillas por canal          | Casilla        | Sin marcar     | Ninguna               | Estilo de alto contraste; visible solo cuando el botón maestro `Enable` está activado. |
| `Base`                      | Campo de texto | `4532`         | `CatTcpPort`           | Puerto TCP base; los canales se enlazan al puerto, puerto+1, puerto+2, puerto+3. Los valores fuera de rango se restablecen a 4532. |
| Filas de canal A/B/C/D      | Indicador      | `(stopped)`    | Ninguna               | Cada fila muestra la insignia del canal, el estado TCP y la ruta PTY. |

### Indicador de estado TCP por canal

| Estado                      | Significado |
|-----------------------------|-------------|
| `(stopped)`                 | Servidor no en ejecución |
| `:<puerto> (1 client)`      | Servidor activo con 1 cliente conectado |
| `:<puerto> (N clients)`     | Servidor activo con N clientes conectados |

### Indicador de ruta PTY por canal

| Estado                      | Significado |
|-----------------------------|-------------|
| `stopped`                   | Sin PTY activo |
| `<ruta>`                    | Ruta del enlace simbólico cuando PTY está en ejecución (ej., `/run/user/1000/aethersdr/cat-A` en Linux o `~/Library/Caches/AetherSDR/cat-A` en macOS) |

## Persistencia de la selección de VFO

Los combos VFO en cada fila de canal están limitados por la cantidad de slices de la radio. Si se reconecta a una radio más pequeña, un slice previamente seleccionado que ya no existe se conserva en la configuración y reaparece cuando los slices regresan. Solo se conserva una selección genuina y representable (incluyendo un `—` deliberado).

## Consejos

- El botón maestro `Enable` en el applet está vinculado a las configuraciones `Autostart rigctld with AetherSDR` y `Autostart CAT with AetherSDR`. Al alternar el botón, se actualizan ambas preferencias de inicio automático al mismo tiempo, por lo que puede usar el botón del applet en lugar del menú Configuración si lo prefiere.
- Si cambia el puerto `Base` después de habilitar los servidores CAT, el nuevo puerto se guarda en `CatTcpPort` y los servidores en ejecución se reinician inmediatamente en la nueva base. El valor guardado también se usa en el próximo inicio automático.
- En la v26.5.3, AetherSDR incluye una implementación nativa de Hamlib NET rigctl, reemplazando la necesidad de un puente rigctld independiente. Los slices A–H exponen cada uno un TTY (ruta de ejecución por usuario) y un puerto TCP (4532–4539).
- La creación de enlaces simbólicos PTY utiliza reemplazo atómico (symlink + rename) para evitar condiciones de carrera TOCTOU (GHSA-qxhr-cwrc-pvrm).

## Solución de problemas

- **Los servidores no se inician después del inicio aunque el inicio automático esté habilitado** — La radio debe estar conectada antes de que los servidores se activen. Confirme el estado de la conexión en la barra de título y vuelva a intentarlo una vez conectado.
- **Las casillas por canal están atenuadas** — Haga clic primero en el botón maestro `Enable` para habilitar los servidores CAT antes de configurar los canales individuales.
- **Los enlaces simbólicos PTY no aparecen** — La función PTY solo funciona en Linux y macOS. En Windows, PTY no tiene efecto. En Linux, verifique que `$XDG_RUNTIME_DIR` esté configurado (típicamente `/run/user/<uid>`).
- **Puerto ya en uso** — Si otra aplicación ocupa un puerto en el rango Base–Base+3, el servidor correspondiente fallará silenciosamente. Cambie el valor de `Base` en el applet CAT Control a un rango de puertos no utilizado y vuelva a habilitar.
- **Los colores de las insignias de canal parecen incorrectos** — Los colores de los slices se gestionan dinámicamente. Si las insignias muestran colores inesperados, desconéctese y reconéctese a la radio para que se actualicen las asignaciones de color de los slices.

## Relacionados

- [Descripción general de CAT Control](overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones Linux/macOS puedan abrir un puerto CAT de tipo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
