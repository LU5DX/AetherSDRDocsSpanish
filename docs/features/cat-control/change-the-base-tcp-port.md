# Cambiar el puerto TCP base

Cambie el número de puerto que el applet CAT Control utiliza como punto de partida para sus cuatro servidores TCP rigctld. Debe hacer esto cuando el puerto 4532 entra en conflicto con otra aplicación en su sistema.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT Control requiere una conexión de radio activa.
- Abra el applet CAT Control haciendo clic en el botón de bandeja **CAT** en la barra lateral derecha si no está visible todavía.

## Pasos

1. Localice el campo **Base:** en la zona superior derecha del applet CAT Control.
2. Haga clic en el campo **Base:** e ingrese el nuevo número de puerto. El rango válido es 1024–65535. El valor predeterminado es `4532`.
3. Presione Enter o haga clic fuera del campo para confirmar.
   - Si ingresa un valor fuera del rango 1024–65535, el campo regresa automáticamente a `4532`.
   - El nuevo valor se guarda en `CatTcpPort` de inmediato.
   - Si **Enable TCP** está activo en ese momento, los cuatro servidores se detienen y se reinician en los nuevos puertos automáticamente. No se requiere reinicio manual.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---------|----------------|--------------|------------------|----------------|
| **Base:** | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales A, B, C y D se enlazan a Base, Base+1, Base+2 y Base+3 respectivamente. Los valores fuera de rango regresan a `4532`. Si **Enable TCP** está activo, los servidores se reinician inmediatamente con los nuevos puertos. |

## Consejos

- Elija un puerto base que deje libres los tres puertos siguientes. Por ejemplo, si establece **Base:** en `4532`, los cuatro servidores ocupan los puertos 4532, 4533, 4534 y 4535.
- Después de cambiar el puerto, actualice el número de puerto en cualquier software externo de registro o concurso (N1MM, Log4OM, WSJT-X) para que coincida.
- Las filas de estado de canal (A/B/C/D) se actualizan para mostrar los nuevos números de puerto en cuanto se reinician los servidores.

## Solución de problemas

- **El campo regresa a 4532 después de ingresar un nuevo valor** — El valor ingresado estaba fuera del rango válido de 1024–65535. Ingrese un número dentro de ese rango.
- **Los servidores no se reinician en el nuevo puerto tras cambiar Base:** — Verifique que **Enable TCP** esté activo. Si TCP está deshabilitado, el nuevo puerto se guarda pero los servidores no se inician hasta que haga clic en **Enable TCP**.
- **El servidor no logra iniciarse en el nuevo puerto** — Es posible que otra aplicación ya esté escuchando en ese puerto o en uno de los tres puertos superiores. Elija un puerto base diferente e inténtelo de nuevo.

## Relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
