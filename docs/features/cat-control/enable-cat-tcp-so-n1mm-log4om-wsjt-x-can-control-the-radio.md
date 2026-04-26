# Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld, uno por canal de slice (A–D), para que el software externo de registro y competencias pueda controlar el radio mediante una conexión de red. Use esta página para iniciar esos servidores y apuntar su software al puerto correcto.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT Control requiere una conexión de radio activa.
- Conozca qué puerto TCP espera su software de registro. El puerto base predeterminado es `4532`.
- Si otra aplicación ya está escuchando en el puerto 4532 (por ejemplo, una instancia independiente de rigctld), elija un puerto base diferente antes de habilitar.

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha para abrir el applet CAT Control. El applet está oculto de manera predeterminada.
2. Verifique el campo **Base**. El valor predeterminado es `4532`. Si necesita un puerto diferente, haga clic en el campo, escriba un nuevo valor (1024–65535) y presione Enter. El valor se guarda en `CatTcpPort`. Si ingresa un valor fuera de rango, regresará automáticamente a `4532`.
3. Haga clic en **Enable TCP**. El botón se ilumina en verde cuando está activo. Los cuatro servidores TCP de rigctld se inician de inmediato y se enlazan a Base, Base+1, Base+2 y Base+3.
4. Confirme que las filas de canales se actualicen. Cada fila (A, B, C, D) muestra un estado como `:4532 (0 clients)` cuando el servidor está en ejecución y esperando una conexión.
5. En su software de registro o de competencias (N1MM, Log4OM, WSJT-X o similar), configure la interfaz CAT como **Hamlib NET rigctl** y establezca el host en `localhost` y el puerto en el puerto de canal que desea controlar:
   - Canal A: puerto base (predeterminado `4532`)
   - Canal B: Base+1 (predeterminado `4533`)
   - Canal C: Base+2 (predeterminado `4534`)
   - Canal D: Base+3 (predeterminado `4535`)
6. Conéctese desde el software externo. La fila del canal correspondiente se actualiza para mostrar el número de clientes, por ejemplo `:4532 (1 client)`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| **Enable TCP** | Botón de alternancia | Apagado | Encendido / Apagado | — | Inicia o detiene los cuatro servidores TCP de rigctld en Base hasta Base+3. También guarda el puerto base actual en `CatTcpPort`. |
| **Enable TTY** | Botón de alternancia | Apagado | Encendido / Apagado | — | Inicia o detiene los enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. No es necesario para software basado en TCP. |
| **Base** | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales se enlazan a Base, Base+1, Base+2 y Base+3. Si los servidores están en ejecución cuando cambia este valor, se reinician en los nuevos puertos automáticamente. |
| **Filas A / B / C / D** | Indicador | `(stopped)` | — | — | Muestra el estado del servidor y el número de clientes conectados para cada canal. Muestra `(stopped)` cuando el servidor está apagado, o `:<port> (N clients)` cuando está en ejecución. |

## Consejos

- Cada canal corresponde a un slice. Si solo usa un slice, únicamente el canal A necesita un cliente conectado.
- Si cambia el puerto **Base** mientras **Enable TCP** ya está activo, los servidores se reinician automáticamente en los nuevos puertos. No es necesario desactivar y volver a activar **Enable TCP**.
- Para iniciar los servidores TCP automáticamente cada vez que se inicie AetherSDR, use `Settings > Autostart rigctld with AetherSDR`.

## Solución de problemas

- **La fila del canal permanece en `(stopped)` después de hacer clic en Enable TCP** — Es posible que otro proceso ya esté escuchando en ese puerto. Haga clic en **Enable TCP** para detener los servidores, cambie **Base** a un puerto no utilizado y luego haga clic en **Enable TCP** nuevamente.
- **El software externo se conecta pero no puede controlar el radio** — Confirme que AetherSDR esté conectado al FLEX-8600. El applet CAT Control requiere una conexión de radio activa. Verifique el estado de la conexión y reconéctese si es necesario.
- **El campo de puerto regresa a 4532 después de escribir un valor** — El valor ingresado estaba fuera del rango válido de 1024–65535. Ingrese un valor dentro de ese rango.

## Relacionados

- [Descripción general de CAT Control](overview.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
