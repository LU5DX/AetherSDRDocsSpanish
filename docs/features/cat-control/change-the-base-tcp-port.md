# Cambiar el puerto TCP base

El applet de Control CAT ejecuta hasta cuatro servidores TCP compatibles con rigctld en puertos consecutivos a partir de una base configurable. Cambie el puerto base cuando el valor predeterminado entre en conflicto con otra aplicación en su sistema.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT requiere una conexión activa con la radio.
- Abra el applet Control CAT haciendo clic en el botón de bandeja CAT en la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet Control CAT, localice la etiqueta `Base:` y su campo de texto en la parte inferior del applet.
2. Haga clic en el campo `Base:` y escriba el nuevo número de puerto. Rango válido: 1024–65535. Valor predeterminado: `4532`.
3. Presione Enter o Tab para confirmar. Si el valor está fuera del rango válido, se restablece a `4532`.
4. El nuevo puerto base se guarda inmediatamente en `CatTcpPort`.
5. Si `Enable TCP` está actualmente activo, los cuatro servidores se reinician automáticamente en los nuevos puertos (base, base+1, base+2, base+3). No se requiere ninguna acción adicional.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| `Base:` | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales A, B, C, D se vinculan a base, base+1, base+2, base+3. Los valores fuera de rango se restablecen a `4532`. Si `Enable TCP` está activo, los servidores se reinician inmediatamente con el nuevo puerto. |
| `Enable TCP` | Botón de alternancia | Apagado | — | — | Inicia o detiene los cuatro servidores TCP rigctld. También persiste el puerto base actual en `CatTcpPort` al alternar. |
| `Enable TTY` | Botón de alternancia | Apagado | — | — | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Solo en Linux y macOS. |
| Filas A/B/C/D | Indicador | `(stopped)` | — | — | Muestra el estado TCP por canal como `:<puerto> (N clientes)` cuando un servidor está en ejecución, o `(stopped)` cuando no lo está. También muestra la ruta del enlace simbólico PTY para cada canal cuando TTY está habilitado. Las insignias de canal tienen códigos de color por slice. |

## Consejos

- Elija un puerto base que deje libres los siguientes tres puertos consecutivos. Por ejemplo, una base de `4532` utiliza `4532`, `4533`, `4534` y `4535`.
- Si cambia el puerto mientras `Enable TCP` está desactivado, los servidores se iniciarán en el nuevo puerto la próxima vez que haga clic en `Enable TCP`.
- En Linux y macOS, haga clic en `Enable TTY` para exponer cada canal como un puerto serie virtual. Apunte su software de registro al enlace simbólico correspondiente `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D` en lugar de un socket TCP.

## Solución de problemas

- **Los servidores no se reinician después de cambiar el puerto** — Confirme que presionó Enter o Tab para finalizar la edición del campo `Base:`. Hacer clic fuera sin confirmar la edición puede no aplicar el cambio.
- **El campo de puerto se restablece a 4532** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro de ese rango.
- **El servidor no se inicia en el nuevo puerto** — Otra aplicación puede estar usando ese puerto o uno de los tres puertos consecutivos. Elija un puerto base diferente.
- **Los enlaces simbólicos PTY no aparecen** — `Enable TTY` está disponible solo en Linux y macOS. Confirme que hizo clic en `Enable TTY` y que AetherSDR tiene acceso de escritura a `/tmp`.

## Relacionados

- [Habilitar TCP CAT para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
