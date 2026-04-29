# Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld, uno por canal de slice (A–D), para que el software externo de registro y concursos pueda controlar la radio a través de un socket de red. Use esta página para iniciar esos servidores y apuntar su software de registro al puerto correcto.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT requiere una conexión de radio activa.
- Decida qué puerto base utilizar. El valor predeterminado es `4532`. Los canales A, B, C y D se vinculan al puerto base, base+1, base+2 y base+3 respectivamente.
- Asegúrese de que ninguna otra aplicación (incluida una instancia independiente de rigctld) esté ya escuchando en esos puertos.

## Pasos

1. Haga clic en el botón de bandeja **CAT** en la barra lateral derecha para abrir el applet CAT Control. El applet está oculto de forma predeterminada.
2. Verifique el valor en el campo **Base**. El valor predeterminado es `4532`. Cámbielo si es necesario (rango válido: 1024–65535). Presione Enter o haga clic fuera para confirmar; los valores fuera de rango vuelven automáticamente a `4532`.
3. Haga clic en **Enable TCP**. El botón se resalta en verde cuando está activo.
4. Verifique las filas de canales. Cada fila etiquetada A, B, C o D debería actualizarse de `(stopped)` a `:<puerto> (0 clients)` una vez que los servidores estén escuchando.
5. En su software de registro o de concursos (N1MM, Log4OM, WSJT-X o similar), configure la conexión CAT como **rigctld (net)** e ingrese `localhost` (o la dirección IP del equipo con AetherSDR) y el puerto del canal que desea controlar — por ejemplo, `4532` para el canal A o `4533` para el canal B.
6. Cuando el software externo se conecte, la fila del canal se actualizará a `:<puerto> (1 client)`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TCP** | Apagado | Encendido / Apagado | — | Inicia o detiene los cuatro servidores TCP rigctld. También escribe el puerto base actual en `CatTcpPort`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. El canal A usa este puerto; B, C y D usan base+1, base+2, base+3. Si los servidores ya están en ejecución, se reinician en los nuevos puertos de inmediato. |
| **Enable TTY** | Apagado | Encendido / Apagado | — | Inicia o detiene los enlaces simbólicos PTY (`/tmp/AetherSDR-CAT-A` hasta `D`) para acceso estilo serie. No es necesario para software basado en TCP. |
| Filas de canales (A–D) | `(stopped)` | — | — | Muestra el estado TCP de cada canal y el número de clientes conectados. El color del indicador coincide con el color del slice. |

## Consejos

- Si solo usa un programa de registro a la vez, el canal A en el puerto `4532` es suficiente. Los canales B–D existen para ejecutar varios programas simultáneamente contra diferentes slices.
- Para que los servidores TCP se inicien automáticamente cada vez que AetherSDR arranque, use `Settings > Autostart rigctld with AetherSDR`.
- Cambiar el valor de **Base** mientras **Enable TCP** está activo reinicia todos los servidores en ejecución en los nuevos puertos de inmediato. Actualice la configuración de puerto en su software de registro antes de volver a conectarse.

## Solución de problemas

- **La fila del canal permanece en `(stopped)` después de hacer clic en Enable TCP** — Es probable que otro proceso ya esté escuchando en ese puerto. Elija un puerto base diferente o detenga la aplicación en conflicto.
- **El software de registro muestra "connection refused"** — Confirme que **Enable TCP** esté activado (el botón está en verde) y que esté usando el número de puerto correcto para el canal. Si AetherSDR está en un equipo remoto, use la dirección IP de ese equipo en lugar de `localhost`.
- **El contador de clientes no aumenta** — El software se conectó pero se desconectó de inmediato. Verifique que su software de registro esté configurado en modo **rigctld** (red) y no en modo serial directo o Hamlib que espere un protocolo diferente.

## Relacionado

- [Descripción general de CAT Control](overview.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
