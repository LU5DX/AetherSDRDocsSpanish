# Descripción general del control CAT

El control CAT permite que software externo de registro y concursos — como N1MM+, Log4OM y WSJT-X — controle el FLEX-8600 presentando hasta cuatro interfaces independientes compatibles con rigctld, una por cada slice de radio. Cada interfaz está disponible como servidor TCP, enlace simbólico PTY serie (solo en Linux y macOS), o ambos simultáneamente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El control CAT requiere una conexión de radio activa.
- Abra el applet de control CAT haciendo clic en el botón CAT de la bandeja en la barra lateral derecha. El applet está oculto de forma predeterminada.

## Cómo funciona

AetherSDR ejecuta hasta cuatro servidores compatibles con rigctld en paralelo, etiquetados como canales A, B, C y D. Cada canal se asigna a un slice de radio (slice 0–3). El software externo se conecta a un canal y emite comandos rigctld estándar para leer o establecer la frecuencia, el modo y otros parámetros de ese slice.

**Los servidores TCP** se enlazan a puertos consecutivos comenzando desde el puerto base. Con el puerto base predeterminado de 4532, el canal A se enlaza al puerto 4532, B al 4533, C al 4534 y D al 4535. Cualquier software que pueda apuntar a un socket TCP de rigctld puede conectarse al puerto correspondiente.

**Los enlaces simbólicos PTY** (solo en Linux y macOS) aparecen como dispositivos serie virtuales en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. El software que espera una ruta de puerto serie puede abrir estos enlaces simbólicos directamente.

Los modos TCP y PTY son independientes. Puede ejecutar uno, ambos o ninguno en cualquier sesión. Ambos modos se pueden configurar para iniciarse automáticamente cuando AetherSDR se inicia, mediante `Settings > Autostart rigctld with AetherSDR` y `Settings > Autostart CAT with AetherSDR`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| Enable TCP | Botón de activación | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP rigctld en Base hasta Base+3. También persiste el puerto base actual en `CatTcpPort`. |
| Enable TTY | Botón de activación | Desactivado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Solo en Linux y macOS. |
| Base | Campo de texto | 4532 | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales se enlazan a Base, Base+1, Base+2, Base+3. Los valores fuera del rango válido vuelven automáticamente a 4532. Si los servidores TCP ya están en ejecución, se reinician inmediatamente en los nuevos puertos. |
| Filas de canales A / B / C / D | Indicador | (detenido) | — | — | Cada fila muestra una insignia de canal codificada por color, el estado TCP de ese canal y la ruta PTY. El estado TCP muestra `(stopped)` cuando el servidor no está en ejecución, o `:<port> (N client(s))` cuando está escuchando. |

## Consejos

- Si cambia el puerto base mientras Enable TCP está activo, los servidores se reinician automáticamente en los nuevos puertos; no es necesario desactivar y volver a activar Enable TCP.
- Los colores de las insignias de canal coinciden con los colores de los slices utilizados en otras partes de AetherSDR, lo que facilita identificar qué canal corresponde a qué slice.
- Para verificar cuántos clientes externos están conectados actualmente a cada canal, lea la etiqueta de estado TCP en cada fila de canal. Se actualiza en tiempo real a medida que los clientes se conectan y desconectan.

## Solución de problemas

- **Enable TCP permanece desactivado después de hacer clic en él** — Confirme que AetherSDR está conectado a la radio. El control CAT requiere una conexión de radio activa.
- **El enlace al puerto falla silenciosamente** — Es posible que otro proceso del sistema ya esté usando ese puerto. Cambie Base a un puerto sin uso en el rango 1024–65535 y haga clic en Enable TCP nuevamente.
- **Enable TTY no tiene efecto** — Los enlaces simbólicos PTY solo están disponibles en Linux y macOS. El control no tiene función en Windows.
- **El software externo no puede conectarse** — Verifique que el software esté apuntando al puerto correcto (Base + desplazamiento de canal 0–3) y que un cortafuegos local no esté bloqueando la conexión.

## Relacionados

- [Activar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Activar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
