# Cambiar el puerto TCP base

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld en puertos consecutivos a partir de un puerto base configurable. Cambie el puerto base cuando el valor predeterminado entre en conflicto con otra aplicación en su sistema.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT requiere una conexión de radio activa.
- Abra el applet CAT Control haciendo clic en el botón CAT de la bandeja en la barra lateral derecha, si no está visible todavía.

## Pasos

1. En el applet CAT Control, localice la etiqueta `Base:` y su campo de texto en la parte inferior del applet.
2. Haga clic en el campo `Base:` y escriba el nuevo número de puerto. Rango válido: 1024–65535. Valor predeterminado: `4532`.
3. Presione Enter o Tab para confirmar. Si el valor está fuera del rango válido, vuelve automáticamente a `4532`.
4. El nuevo puerto base se guarda inmediatamente en `CatTcpPort`.
5. Si `Enable TCP` está activo en ese momento, los cuatro servidores se reinician automáticamente en los nuevos puertos (base, base+1, base+2, base+3). No se requiere ninguna acción adicional.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| `Base:` | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales A, B, C, D se vinculan a base, base+1, base+2, base+3. Los valores fuera de rango vuelven a `4532`. Si `Enable TCP` está activo, los servidores se reinician con el nuevo puerto de inmediato. |
| `Enable TCP` | Botón de alternancia | Off | — | — | Inicia o detiene los cuatro servidores TCP rigctld. También persiste el puerto base actual en `CatTcpPort` al ser activado. |
| `Enable TTY` | Botón de alternancia | Off | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Solo en Linux y macOS. |
| Filas A/B/C/D | Indicador | `(stopped)` | — | — | Muestra el estado TCP por canal como `:<port> (N clients)` cuando el servidor está en ejecución, o `(stopped)` cuando no lo está. También muestra la ruta del enlace simbólico PTY para cada canal cuando TTY está habilitado. Las insignias de canal están codificadas por color según el slice. |

## Consejos

- Elija un puerto base que deje libres los tres puertos consecutivos siguientes. Por ejemplo, un puerto base de `4532` utiliza `4532`, `4533`, `4534` y `4535`.
- Si cambia el puerto mientras `Enable TCP` está desactivado, los servidores se iniciarán en el nuevo puerto la próxima vez que haga clic en `Enable TCP`.
- En Linux y macOS, haga clic en `Enable TTY` para exponer cada canal como un puerto serie virtual. Apunte su software de registro al enlace simbólico correspondiente `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D` en lugar de un socket TCP.

## Solución de problemas

- **Los servidores no se reinician después de cambiar el puerto** — Confirme que presionó Enter o Tab para finalizar la edición del campo `Base:`. Hacer clic fuera sin confirmar la edición puede no aplicar el cambio.
- **El campo del puerto vuelve a 4532** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro de ese rango.
- **El servidor no logra iniciarse en el nuevo puerto** — Es posible que otra aplicación ya esté utilizando ese puerto o uno de los tres puertos consecutivos. Elija un puerto base diferente.
- **Los enlaces simbólicos PTY no aparecen** — `Enable TTY` está disponible solo en Linux y macOS. Confirme que hizo clic en `Enable TTY` y que AetherSDR tiene acceso de escritura a `/tmp`.

## Relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
