# Verificar cuántos clientes externos están conectados a cada canal

El applet CAT Control muestra un recuento de clientes en tiempo real para cada uno de los cuatro canales TCP de rigctld. Use esto para confirmar que el software de registro o de concurso se ha conectado correctamente al canal adecuado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT requiere una conexión de radio activa.
- Los servidores TCP deben estar en ejecución. Haga clic en "Enable TCP" en el applet CAT si aún no lo ha hecho. Consulte [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md).

## Pasos

1. Haga clic en el botón CAT del panel lateral derecho para abrir el applet CAT Control.
2. Observe las cuatro filas de canales etiquetadas **A**, **B**, **C** y **D**.
3. Lea el campo de estado TCP junto a cada identificador de canal:
   - `(stopped)` — el servidor TCP de ese canal no está en ejecución.
   - `:<port> (0 clients)` — el servidor está escuchando pero ningún software externo está conectado.
   - `:<port> (1 client)` — un cliente externo está conectado.
   - `:<port> (N clients)` — N clientes están conectados.

El estado se actualiza automáticamente cada vez que un cliente se conecta o desconecta. No se necesita actualización manual.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| Filas de canales (A / B / C / D) | Indicador | `(stopped)` | Cada fila muestra un identificador de canal con código de color, el estado TCP y el recuento de clientes, y la ruta PTY. El color del campo de estado cambia para coincidir con el color del slice cuando uno o más clientes están conectados. |
| Enable TCP | Botón de alternancia | Desactivado | Inicia o detiene los cuatro servidores TCP de rigctld. Los puertos se asignan en Base, Base+1, Base+2, Base+3. |
| Base | Campo de texto | `4532` | Puerto TCP base. Rango válido: 1024–65535. Los valores fuera de este rango vuelven automáticamente a `4532`. Se almacena como `CatTcpPort`. |

## Consejos

- El color de la etiqueta de estado TCP cambia al color del slice cuando al menos un cliente está activo, lo que facilita identificar los canales activos de un vistazo.
- Los canales A a D corresponden a los slices 0 al 3. Asegúrese de que su software externo apunte al puerto correcto para el slice que debe controlar.

## Solución de problemas

- **Todas las filas muestran `(stopped)` aunque Enable TCP esté activado** — Es posible que el puerto base esté en uso por otra aplicación. Cambie el valor en el campo Base a un puerto libre en el rango 1024–65535 y presione Enter. Los servidores se reiniciarán automáticamente.
- **El recuento de clientes no aumenta después de conectar software externo** — Confirme que el software apunta al número de puerto correcto para el canal deseado (Base para A, Base+1 para B, Base+2 para C, Base+3 para D). Verifique que Enable TCP esté activo (el botón aparece resaltado en verde cuando está activado).

## Relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Cambiar el puerto TCP base](../../features/cat-control/change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
