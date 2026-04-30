# Cambiar el puerto TCP base

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld en puertos consecutivos comenzando desde una base configurable. Cambie el puerto base cuando el valor predeterminado entra en conflicto con otra aplicación en su sistema.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT requiere una conexión de radio activa.
- Abra el applet CAT Control haciendo clic en el botón CAT de la bandeja en la barra lateral derecha si no está ya visible.

## Pasos

1. En el applet CAT Control, localice la etiqueta `Base:` y su campo de texto en la parte inferior del applet.
2. Haga clic en el campo `Base:` e ingrese el nuevo número de puerto. Rango válido: 1024–65535. Predeterminado: `4532`.
3. Presione Enter o Tab para confirmar. Si el valor está fuera del rango válido, vuelve a `4532`.
4. El nuevo puerto base se guarda inmediatamente en `CatTcpPort`.
5. Si `Enable TCP` está actualmente activo, los cuatro servidores se reinician automáticamente en los nuevos puertos (base, base+1, base+2, base+3). No se requiere ninguna acción adicional.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| `Base:` | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales A, B, C, D se vinculan a base, base+1, base+2, base+3. Los valores fuera de rango se ajustan a `4532`. Si `Enable TCP` está activado, los servidores se reinician con el nuevo puerto inmediatamente. |
| `Enable TCP` | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP rigctld. También persiste el puerto base actual en `CatTcpPort` cuando se alterna. |
| `Enable TTY` | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro enlaces PTY en `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D`. Solo en Linux y macOS. |
| Filas A/B/C/D | Indicador | `(stopped)` | — | — | Muestra el estado TCP por canal como `:<puerto> (N clientes)` cuando un servidor está en ejecución, o `(stopped)` cuando no lo está. También muestra la ruta del enlace PTY para cada canal cuando TTY está habilitado. Los distintivos de canal están codificados por color según la slice. |

## Consejos

- Elija un puerto base que deje libres los tres puertos consecutivos siguientes. Por ejemplo, una base de `4532` utiliza `4532`, `4533`, `4534` y `4535`.
- Si cambia el puerto mientras `Enable TCP` está desactivado, los servidores se iniciarán en el nuevo puerto la próxima vez que haga clic en `Enable TCP`.
- En Linux y macOS, haga clic en `Enable TTY` para exponer cada canal como un puerto serie virtual. Apunte su software de registro a los enlaces simbólicos `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D` correspondientes en lugar de un socket TCP.

## Solución de problemas

- **Los servidores no se reinician después de cambiar el puerto** — Confirme que presionó Enter o Tab para terminar de editar el campo `Base:`. Hacer clic en otro lugar sin confirmar la edición puede no aplicar el cambio.
- **El campo de puerto vuelve a 4532** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro de ese rango.
- **El servidor no se inicia en el nuevo puerto** — Es posible que otra aplicación ya esté utilizando ese puerto o uno de los tres puertos consecutivos. Elija un puerto base diferente.
- **Los enlaces simbólicos PTY no aparecen** — `Enable TTY` está disponible solo en Linux y macOS. Confirme que hizo clic en `Enable TTY` y que AetherSDR tiene acceso de escritura a `/tmp`.

## Relacionado

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Autostart CAT servers with AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verifique cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
