# Verificar cuántos clientes externos están conectados a cada canal

El applet CAT Control muestra un conteo de clientes en tiempo real para cada uno de los cuatro canales TCP de rigctld (A–D). Use esto para confirmar que su software de registro o de concurso se ha conectado correctamente al canal indicado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT requiere una conexión activa con el radio.
- Los servidores TCP deben estar en funcionamiento. Haga clic en "Enable TCP" en el applet CAT si aún no lo ha hecho. Consulte [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md).

## Pasos

1. Haga clic en el botón de bandeja "CAT" en la barra lateral derecha para abrir el applet CAT Control.
2. Lea la etiqueta de estado TCP en la fila de cada canal (A, B, C, D).

Eso es todo. El estado se actualiza automáticamente cada vez que un cliente se conecta o desconecta.

## Qué hace cada control

| Control | Qué muestra | Estados |
|---|---|---|
| Filas de canal A / B / C / D | Estado del servidor por canal y conteo de clientes conectados | `(stopped)` cuando el servidor no está en ejecución; `:<port> (1 client)` o `:<port> (N clients)` cuando el servidor está en ejecución |
| "Enable TCP" | Inicia o detiene los cuatro servidores TCP de rigctld | Desactivado por defecto; los canales se enlazan a `Base`, `Base+1`, `Base+2`, `Base+3` |
| Campo "Base" | Puerto TCP base para los cuatro servidores | Valor predeterminado: `4532`; rango válido: 1024–65535; se persiste como `CatTcpPort`; los valores fuera de rango vuelven automáticamente a `4532` |

Cuando un canal no tiene clientes conectados, su etiqueta de estado muestra el número de puerto en un color atenuado. Cuando hay uno o más clientes conectados, la etiqueta cambia al color del slice (canal receptor) correspondiente y muestra `:<port> (N client)` o `:<port> (N clients)`.

## Consejos

- Cada canal corresponde a un slice (A = slice 0, B = slice 1, C = slice 2, D = slice 3). Si su software se conecta al puerto incorrecto, controlará el slice incorrecto.
- El conteo de clientes refleja conexiones TCP, no sesiones autenticadas. Un conteo de 1 normalmente indica que hay una aplicación externa conectada.

## Solución de problemas

- **Todas las filas muestran `(stopped)` aunque "Enable TCP" está activado** — Es posible que el servidor no haya podido enlazarse al puerto. Puede que otra aplicación ya esté usando el puerto base. Cambie el valor en el campo "Base" a un número de puerto diferente y presione Enter. AetherSDR reiniciará los servidores en los nuevos puertos.
- **El conteo de clientes permanece en 0 después de iniciar su software de registro** — Confirme que el software esté configurado para conectarse a `localhost` (o al host correcto) en el puerto esperado (`CatTcpPort` + desplazamiento del canal). Verifique que "Enable TCP" esté activo (el botón aparece resaltado cuando está activado).

## Relacionado

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Cambiar el puerto TCP base](../../features/cat-control/change-the-base-tcp-port.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Descripción general de CAT Control](../../features/cat-control/overview.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
