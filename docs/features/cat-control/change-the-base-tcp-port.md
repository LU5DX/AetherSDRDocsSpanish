# Cambiar el puerto TCP base

Cambie el número de puerto que usa el applet CAT Control como punto de partida para sus cuatro servidores TCP rigctld. Cada canal se enlaza a puertos consecutivos a partir del base: Base, Base+1, Base+2, Base+3.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT Control requiere una conexión de radio activa.
- Abra el applet CAT Control haciendo clic en el botón `CAT` de la barra lateral derecha si no está visible todavía.

## Pasos

1. Localice el campo `Base:` en la fila inferior del applet CAT Control.
2. Haga clic en el campo `Base:` y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `4532`.
3. Presione Enter o Tab para confirmar. Si el valor está fuera del rango válido, se restablece automáticamente a `4532`.
4. AetherSDR guarda el nuevo valor en `CatTcpPort` de inmediato.
5. Si `Enable TCP` está activo en ese momento, los cuatro servidores se detienen y se reinician en los nuevos puertos automáticamente. No se requiere ninguna acción adicional.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| `Base:` | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales A, B, C, D se enlazan a Base, Base+1, Base+2, Base+3. Los valores fuera de rango vuelven a `4532`. Si `Enable TCP` está activado, los servidores se reinician con el nuevo puerto de inmediato. |
| `Enable TCP` | Off | On/Off | — | Inicia o detiene los cuatro servidores TCP rigctld. También persiste el puerto base actual en `CatTcpPort` al conmutarlo. |
| Filas A/B/C/D | `(stopped)` | — | — | Cada fila muestra la letra del canal, el estado TCP (p. ej., `:4532 (1 client)`) y la ruta PTY. |

## Consejos

- Si cambia el puerto mientras `Enable TCP` está desactivado, el nuevo puerto entrará en vigor la próxima vez que haga clic en `Enable TCP`.
- El software externo (N1MM, Log4OM, WSJT-X) debe reconfigurarse para usar los nuevos números de puerto después de cualquier cambio.
- El canal A usa exactamente el puerto base; el canal D usa Base+3. Tenga esto en cuenta si otras aplicaciones ocupan puertos cercanos.

## Solución de problemas

- **El servidor no inicia después de cambiar el puerto** — Es posible que otra aplicación ya esté escuchando en ese puerto o en un puerto adyacente (Base a Base+3). Elija un puerto base diferente e inténtelo de nuevo.
- **El campo se restablece a 4532** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro del rango válido.

## Relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X controlen la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
