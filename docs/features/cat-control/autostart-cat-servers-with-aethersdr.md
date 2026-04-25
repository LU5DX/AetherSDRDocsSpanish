# Inicio automático de servidores CAT con AetherSDR

Configure AetherSDR para iniciar sus servidores TCP CAT o enlaces seriales PTY automáticamente cada vez que se inicia la aplicación, de modo que su software de registro o de concursos se conecte sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 para que los servidores CAT puedan operar. El inicio automático pondrá en cola los servidores para iniciarse en el siguiente arranque cuando se establezca una conexión con la radio.
- Decida si necesita servidores TCP (para software de registro conectado en red, como N1MM, Log4OM o WSJT-X), enlaces seriales PTY (para aplicaciones en Linux/macOS que esperan un puerto serial), o ambos.
- El applet de control CAT está oculto de forma predeterminada. Haga clic en el botón **CAT** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

### Inicio automático de servidores TCP

1. Abra el applet **CAT** haciendo clic en el botón **CAT** de la bandeja en la barra lateral derecha.
2. Haga clic en `Settings > Autostart rigctld with AetherSDR` para marcar ese elemento del menú.
3. El botón **Enable TCP** del applet se marcará automáticamente en el siguiente inicio.

### Inicio automático de enlaces seriales PTY (solo Linux/macOS)

1. Abra el applet **CAT** haciendo clic en el botón **CAT** de la bandeja en la barra lateral derecha.
2. Haga clic en `Settings > Autostart CAT with AetherSDR` para marcar ese elemento del menú.
3. El botón **Enable TTY** del applet se marcará automáticamente en el siguiente inicio.

### Verificar que el inicio automático está activo

1. Reinicie AetherSDR y vuelva a conectarse a la radio.
2. Abra el applet **CAT**.
3. Confirme que **Enable TCP** y/o **Enable TTY** aparecen marcados (resaltados en verde).
4. Compruebe que cada fila de canal (A, B, C, D) muestre un estado de puerto como `:4532 (0 clients)` en lugar de `(stopped)`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| `Settings > Autostart rigctld with AetherSDR` | Casilla de menú | sin marcar | — | `AutoStartRigctld` | Cuando está marcado, habilita los cuatro servidores TCP rigctld al iniciar. |
| `Settings > Autostart CAT with AetherSDR` | Casilla de menú | sin marcar | — | `AutoStartCAT` | Cuando está marcado, crea los enlaces simbólicos PTY `/tmp/AetherSDR-CAT-A` hasta `-D` al iniciar. Solo Linux/macOS. |
| **Enable TCP** | Botón de alternancia | desactivado | — | — | Inicia o detiene los cuatro servidores TCP rigctld de inmediato. También persiste el puerto base actual en `CatTcpPort`. |
| **Enable TTY** | Botón de alternancia | desactivado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY de inmediato. |
| **Base** | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Puerto TCP base. Los canales A–D se enlazan al puerto, puerto+1, puerto+2 y puerto+3. Los valores fuera de rango vuelven a `4532`. Si los servidores TCP están en ejecución, se reinician de inmediato en el nuevo puerto. |

## Consejos

- Habilitar el inicio automático mediante el menú `Settings` establece la preferencia de forma persistida. Alternar **Enable TCP** o **Enable TTY** en el panel del applet cambia el estado de la sesión actual y también actualiza el mismo valor persistido, por lo que cualquiera de los dos métodos sobrevive a un reinicio.
- Si cambia el puerto **Base** mientras **Enable TCP** está marcado, los cuatro servidores se reinician en los nuevos puertos de inmediato, sin necesidad de reiniciar AetherSDR.

## Solución de problemas

- **Las filas de canal siguen mostrando `(stopped)` después del inicio automático** — La radio no estaba conectada cuando se inició AetherSDR. Conecte la radio y, a continuación, haga clic manualmente en **Enable TCP** o **Enable TTY** para iniciar los servidores en la sesión actual. Se iniciarán automáticamente de forma correcta en los arranques posteriores una vez que la radio esté conectada.
- **Enable TTY no aparece o no tiene efecto en Windows** — Los enlaces seriales PTY son una función de Linux/macOS. Use TCP (mediante **Enable TCP**) en Windows.
- **Conflictos de puertos: el servidor no puede iniciarse en un canal** — Otra aplicación ya está usando uno de los cuatro puertos del rango Base a Base+3. Cambie **Base** a un valor diferente, como `4536`, y vuelva a habilitar TCP.

## Relacionado

- [Descripción general del control CAT](overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM y WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones en Linux/macOS puedan abrir un puerto CAT de tipo serial](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Comprobar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
