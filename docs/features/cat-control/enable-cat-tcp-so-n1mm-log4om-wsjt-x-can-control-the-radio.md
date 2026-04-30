# Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X controlen la radio

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld, uno por canal de slice (A–D), para que software externo de logging y concursos controle la radio a través de un socket de red. Use esta página para iniciar esos servidores y dirigir su software de logging al puerto correcto.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT requiere una conexión de radio activa.
- Decida qué puerto base usar. El predeterminado es `4532`. Los canales A, B, C y D se vinculan al puerto base, base+1, base+2 y base+3 respectivamente.
- Asegúrese de que ninguna otra aplicación (incluida una instancia independiente de rigctld) esté ya escuchando en esos puertos.

## Pasos

1. Haga clic en el botón **CAT** en la barra lateral derecha para abrir el applet CAT Control. El applet está oculto por defecto.
2. Verifique el valor en el campo **Base**. El predeterminado es `4532`. Cámbielo si es necesario (rango válido: 1024–65535). Presione Enter o haga clic en otro lugar para confirmar; los valores fuera de rango vuelven a `4532`.
3. Haga clic en **Enable TCP**. El botón se resalta en verde cuando está activo.
4. Verifique las filas de canal. Cada fila etiquetada A, B, C o D debe actualizarse de `(stopped)` a `:<puerto> (0 clients)` cuando los servidores estén escuchando.
5. En su software de logging o concursos (N1MM, Log4OM, WSJT-X, o similar), configure la conexión CAT como **rigctld (net)** e ingrese `localhost` (o la dirección IP de la máquina AetherSDR) y el puerto para el canal que desea controlar — por ejemplo, `4532` para el canal A o `4533` para el canal B.
6. Cuando el software externo se conecte, la fila de canal se actualiza a `:<puerto> (1 client)`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TCP** | Off | On / Off | — | Inicia o detiene los cuatro servidores TCP rigctld. También escribe el puerto base actual en `CatTcpPort`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. El canal A usa este puerto; B, C y D usan base+1, base+2, base+3. Si los servidores ya se están ejecutando, se reinician en los nuevos puertos inmediatamente. |
| **Enable TTY** | Off | On / Off | — | Inicia o detiene los symlinks PTY (`/tmp/AetherSDR-CAT-A` a través de `D`) para acceso de estilo serial. No es necesario para software basado en TCP. |
| Filas de canal (A–D) | `(stopped)` | — | — | Muestra el estado TCP de cada canal y el número de clientes conectados. El color del distintivo coincide con el color del slice. |

## Consejos

- Si solo usa un programa de logging a la vez, el canal A en puerto `4532` es suficiente. Los canales B–D existen para ejecutar múltiples programas simultáneamente en slices diferentes.
- Para que los servidores TCP se inicien automáticamente cada vez que se inicia AetherSDR, use `Settings > Autostart rigctld with AetherSDR`.
- Cambiar el valor de **Base** mientras **Enable TCP** está activo reinicia todos los servidores en ejecución en los nuevos puertos inmediatamente. Actualice la configuración de puerto de su software de logging para que coincida antes de reconectar.

## Solución de problemas

- **La fila de canal permanece en `(stopped)` después de hacer clic en Enable TCP** — Es probable que otro proceso ya esté escuchando en ese puerto. Elija un puerto base diferente o detenga la aplicación en conflicto.
- **El software de logging muestra "connection refused"** — Confirme que **Enable TCP** está activado (el botón es verde) y que está usando el número de puerto correcto para el canal. Si AetherSDR está en una máquina remota, use la dirección IP de esa máquina en lugar de `localhost`.
- **El contador de clientes no se incrementa** — El software se conectó pero se desconectó inmediatamente. Verifique que su software de logging esté configurado en modo **rigctld** (network), no en un modo de serial directo o Hamlib que espere un protocolo diferente.

## Relacionado

- [Descripción general de CAT Control](overview.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar automáticamente servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS abran un puerto CAT de estilo serial](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Configurar modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
