# Activar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio

El applet de Control CAT ejecuta hasta cuatro servidores TCP compatibles con rigctld (y enlaces simbólicos PTY en Linux/macOS), uno por canal de slice (A–H), para que el software externo de registro y concursos pueda controlar el radio a través de un socket de red o una ruta de estilo serie. En la versión 26.5.3, el applet utiliza una implementación nativa de Hamlib NET rigctl, eliminando la necesidad de un puente rigctld independiente. Use esta página para iniciar esos servidores y apuntar su software de registro al puerto correcto.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT requiere una conexión activa con el radio.
- Decida qué puerto base usar. El valor predeterminado es `4532`. Los canales A, B, C y D se enlazan al puerto base, base+1, base+2 y base+3 respectivamente.
- Asegúrese de que ninguna otra aplicación (incluida una instancia independiente de rigctld) esté escuchando ya en esos puertos.

## Pasos

1. Haga clic en el botón de la bandeja **CAT** en la barra lateral derecha para abrir el applet de Control CAT. El applet está oculto de forma predeterminada.
2. Verifique el valor en el campo **Base**. El valor predeterminado es `4532`. Cámbielo si es necesario (rango válido: 1024–65535). Presione Enter o haga clic fuera para confirmar; los valores fuera de rango se revierten a `4532`.
3. Haga clic en **Enable TCP**. El botón se resalta en verde cuando está activo.
4. Verifique las filas de los canales. Cada fila etiquetada A, B, C o D debería actualizarse de `(stopped)` a `:<puerto> (0 clients)` una vez que los servidores estén escuchando.
5. En su software de registro o concursos (N1MM, Log4OM, WSJT-X o similar), configure la conexión CAT como **rigctld (net)** e ingrese `localhost` (o la dirección IP de la máquina con AetherSDR) y el puerto del canal que desea controlar — por ejemplo, `4532` para el canal A o `4533` para el canal B.
6. Cuando el software externo se conecte, la fila del canal se actualiza a `:<puerto> (1 client)`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TCP** | Off | On / Off | — | Inicia o detiene los cuatro servidores TCP rigctld. También escribe el puerto base actual en `CatTcpPort`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. El canal A usa este puerto; B, C y D usan base+1, base+2, base+3. Si los servidores ya están en ejecución, se reinician inmediatamente en los nuevos puertos. |
| **Enable TTY** | Off | On / Off | — | Inicia o detiene los enlaces simbólicos PTY para acceso tipo serie. La ruta del enlace simbólico se muestra por canal. En Linux, las rutas están bajo `$XDG_RUNTIME_DIR/aethersdr/cat-A` hasta `cat-D`. En macOS, las rutas están bajo `~/Library/Caches/AetherSDR/cat-A` hasta `cat-D`. No es necesario para software basado en TCP. |
| Filas de canales (A–D) | `(stopped)` | — | — | Muestra el estado TCP de cada canal y el número de clientes conectados. El color de la insignia coincide con el color del slice. La ruta PTY se muestra cuando está habilitada. |

## Actualización de seguridad en v26.5.3

En la versión 26.5.3, la ubicación del enlace simbólico PTY se movió de `/tmp` a directorios de ejecución por usuario (`$XDG_RUNTIME_DIR/aethersdr/` en Linux, `~/Library/Caches/AetherSDR/` en macOS). Este cambio corrige una vulnerabilidad de enlace simbólico entre usuarios (GHSA-qxhr-cwrc-pvrm). El reemplazo atómico de enlaces simbólicos (creando un enlace simbólico temporal y luego renombrándolo) cierra la ventana de ejecución TOCTOU.

## Consejos

- Si solo usa un programa de registro a la vez, el canal A en el puerto `4532` es suficiente. Los canales B–D existen para ejecutar múltiples programas simultáneamente contra diferentes slices.
- Para que los servidores TCP se inicien automáticamente cada vez que AetherSDR se lance, use `Settings > Autostart rigctld with AetherSDR`.
- Cambiar el valor de **Base** mientras **Enable TCP** está activo reinicia todos los servidores en ejecución inmediatamente en los nuevos puertos. Actualice la configuración del puerto en su software de registro para que coincida antes de reconectar.
- Para acceso PTY, el software externo abre la ruta mostrada en la fila del canal, que es la misma ubicación donde se crea el enlace simbólico real.

## Solución de problemas

- **La fila del canal permanece `(stopped)` después de hacer clic en Enable TCP** — Es probable que otro proceso ya esté escuchando en ese puerto. Elija un puerto base diferente o detenga la aplicación en conflicto.
- **El software de registro muestra "connection refused"** — Confirme que **Enable TCP** esté activado (el botón está verde) y que esté usando el número de puerto correcto para el canal. Si AetherSDR está en una máquina remota, use la dirección IP de esa máquina en lugar de `localhost`.
- **El contador de clientes no aumenta** — El software se conectó pero se desconectó inmediatamente. Verifique que su software de registro esté configurado en modo **rigctld** (red), no en un modo serie directo o Hamlib que espere un protocolo diferente.

## Relacionado

- [Resumen del Control CAT](overview.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Inicio automático de servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Activar CAT PTY para que aplicaciones Linux/macOS puedan abrir un puerto CAT tipo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
