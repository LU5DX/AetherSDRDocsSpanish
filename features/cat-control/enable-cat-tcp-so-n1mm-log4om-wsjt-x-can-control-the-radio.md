# Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld, uno por canal de slice (A–D). Habilite TCP para que el software externo de registro y de concurso pueda conectarse a AetherSDR y controlar la radio a través de la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT Control requiere una conexión de radio activa.
- Decida qué puerto base utilizar. El valor predeterminado es `4532`. Los canales A–D se enlazan a Base, Base+1, Base+2 y Base+3 respectivamente.
- Asegúrese de que ninguna otra aplicación (incluida una instancia independiente de rigctld) esté escuchando en esos puertos.

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha. Aparece el applet CAT Control.
2. Verifique el campo **Base**. El valor predeterminado es `4532`. Si necesita un puerto diferente, haga clic en el campo, escriba un nuevo valor (1024–65535) y presione Enter. Los valores fuera de ese rango vuelven automáticamente a `4532`.
3. Haga clic en **Enable TCP**. El botón se resalta en verde y los cuatro servidores TCP rigctld se inician.
4. Confirme que las filas de canales se actualizan. Cada fila que tiene un servidor en ejecución muestra un puerto y el número de clientes conectados, por ejemplo `:4532 (0 clients)`. Las filas sin ningún cliente conectado muestran el puerto atenuado; las filas con un cliente activo muestran el puerto en el color del slice del canal.
5. En su software de registro o de concurso (N1MM, Log4OM, WSJT-X, etc.), configure la interfaz CAT como **rigctld**, con el host `localhost` (o la dirección IP del equipo con AetherSDR) y el puerto correspondiente al canal que desea controlar:

   | Canal | Puerto predeterminado |
   |-------|-----------------------|
   | A     | 4532                  |
   | B     | 4533                  |
   | C     | 4534                  |
   | D     | 4535                  |

6. Conéctese desde el software externo. El contador de clientes en la fila del canal se incrementa para confirmar la conexión, por ejemplo `:4532 (1 client)`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| **Enable TCP** | Botón de alternancia | Desactivado | Activado / Desactivado | — | Inicia o detiene los cuatro servidores TCP rigctld en los puertos Base a Base+3. Al activarse, también guarda el puerto base actual en `CatTcpPort`. |
| **Enable TTY** | Botón de alternancia | Desactivado | Activado / Desactivado | — | Inicia o detiene los enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. No es necesario para software que solo use TCP. |
| **Base** | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. El canal A se enlaza a este puerto; B, C y D se enlazan a Base+1, Base+2 y Base+3. Si TCP ya está en ejecución cuando se cambia este valor, todos los servidores se reinician automáticamente en los nuevos puertos. |
| **Filas A / B / C / D** | Indicador | `(stopped)` | — | — | Cada fila muestra la etiqueta del canal, el estado TCP actual, el número de clientes conectados y la ruta PTY. |

## Consejos

- Cada canal corresponde a un slice de radio. Si solo utiliza un slice, conecte su software al canal A (puerto `4532` de forma predeterminada) e ignore los demás canales.
- Si cambia el puerto base mientras **Enable TCP** está activo, los servidores se reinician automáticamente en los nuevos puertos. No es necesario desactivar y volver a activar TCP.
- Para iniciar los servidores TCP automáticamente cada vez que se inicia AetherSDR, use `Settings > Autostart CAT with AetherSDR`.

## Solución de problemas

- **La fila del canal permanece en `(stopped)` después de hacer clic en Enable TCP** — Es posible que otro proceso ya esté escuchando en ese puerto. Detenga el proceso en conflicto, o cambie **Base** a un rango de puertos libre y haga clic en **Enable TCP** nuevamente.
- **El software externo se conecta pero informa una frecuencia o modo incorrecto** — Verifique que el software esté apuntando al puerto de canal correcto para el slice que desea controlar. Cada canal controla únicamente su slice asignado.
- **Enable TCP no tiene efecto y el botón no permanece resaltado** — AetherSDR debe estar conectado a la radio antes de que los servidores CAT puedan iniciarse. Conéctese a la radio primero y luego haga clic en **Enable TCP**.

## Relacionados

- [Descripción general de CAT Control](overview.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
