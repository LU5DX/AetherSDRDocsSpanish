# Verificar cuántos clientes externos están conectados a cada canal

El applet CAT Control muestra un indicador de estado TCP en tiempo real para cada uno de los cuatro canales (A–D). Úselo para confirmar que el software de registro o de concurso se ha conectado correctamente al puerto rigctld correspondiente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El applet CAT Control requiere una conexión de radio activa.
- Los servidores TCP deben estar en ejecución (Enable TCP debe estar activo). Los canales muestran `(stopped)` hasta que los servidores se inicien.

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha para abrir el applet CAT Control.
2. Observe las filas de canales etiquetadas **A**, **B**, **C** y **D**.
3. Lea el indicador de estado TCP a la derecha de cada insignia de canal:
   - `(stopped)` — el servidor TCP de ese canal no está en ejecución.
   - `:<port> (0 clients)` — el servidor está escuchando, pero ningún software externo está conectado.
   - `:<port> (1 client)` — un cliente externo está conectado.
   - `:<port> (N clients)` — N clientes están conectados.

El estado se actualiza automáticamente a medida que los clientes se conectan y desconectan. No se requiere ninguna acción de actualización manual.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Enable TCP | Inicia o detiene los cuatro servidores TCP rigctld en los puertos Base a Base+3. | Off | — | — |
| Base | Puerto TCP base. El canal A se enlaza a este puerto; B, C y D se enlazan a Base+1, Base+2 y Base+3. Los valores fuera de rango vuelven automáticamente a 4532. | 4532 | 1024–65535 | `CatTcpPort` |
| Filas A/B/C/D | Indicadores por canal que muestran el estado TCP y la ruta PTY. | (stopped) | — | — |

## Consejos

- El número de puerto que aparece en el indicador de estado (por ejemplo, `:4532`) confirma en qué puerto está escuchando ese canal. Compruébelo con el puerto configurado en su software de registro.
- Los colores de las insignias de canal coinciden con los colores de slice (receptor) utilizados en el resto de AetherSDR, lo que facilita asociar una fila de canal con un slice receptor específico.

## Solución de problemas

- **Todas las filas muestran `(stopped)`** — Enable TCP no ha sido activado. Haga clic en **Enable TCP** en el applet CAT Control para iniciar los servidores.
- **El estado muestra `0 clients` pero su software de registro debería estar conectado** — Confirme que el software apunta al puerto correcto. El canal A usa el puerto base (predeterminado `4532`); B usa base+1, C usa base+2 y D usa base+3. Verifique que ningún cortafuegos esté bloqueando el puerto.
- **Enable TCP está activo pero un canal específico sigue mostrando `(stopped)`** — Es posible que el puerto de ese canal ya esté en uso por otra aplicación. Cambie el valor en **Base** a un rango de puertos libre y vuelva a activarlo.

## Relacionado

- [Activar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Cambiar el puerto TCP base](../../features/cat-control/change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Descripción general de CAT Control](../../features/cat-control/overview.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
