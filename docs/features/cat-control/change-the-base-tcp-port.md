# Cambiar el puerto TCP base

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld en puertos consecutivos a partir de una base configurable. Cambie el puerto base cuando el valor predeterminado entre en conflicto con otra aplicación en su sistema.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT requiere una conexión activa al radio.
- Abra el applet CAT Control haciendo clic en el botón de la bandeja CAT en la barra lateral derecha, si aún no está visible.

## Pasos

1. En el applet CAT Control, localice la etiqueta `Base:` y su campo de texto en la parte inferior del applet.
2. Haga clic en el campo `Base:` y escriba el nuevo número de puerto. Rango válido: 1024–65535. Valor predeterminado: `4532`.
3. Presione Enter o Tab para confirmar. Si el valor está fuera del rango válido, volverá automáticamente a `4532`.
4. El nuevo puerto base se guarda inmediatamente en `CatTcpPort`.
5. Si `Enable TCP` está activo en ese momento, los cuatro servidores se reinician automáticamente en los nuevos puertos (base, base+1, base+2, base+3). No se requiere ninguna acción adicional.

## Qué hace cada control

| Control                | Tipo           | Valor predeterminado |
|------------------------|----------------|----------------------|
| `Base:`                | Campo de texto | `4532`               |
| `Enable CAT`           | Botón de alternancia | Desactivado     |
| Casillas de verificación Habilitar | Casilla de verificación | Sin marcar |
| Filas de canal A/B/C/D | Indicador      | `(stopped)`          |

El botón de alternancia principal muestra `Enabled` cuando los servidores CAT están activos y `Disabled` cuando están apagados. La misma etiqueta aparece tanto en la vista acoplada como en la flotante del applet.

Cada fila de canal incluye una casilla de verificación de habilitación por canal. La casilla tiene un borde de alto contraste y se rellena con un color de acento cuando está marcada, lo que permite leer el estado activado/desactivado de un vistazo sobre el fondo oscuro del applet.

## Consejos

- Elija un puerto base que deje libres los tres puertos consecutivos siguientes. Por ejemplo, una base de `4532` utiliza `4532`, `4533`, `4534` y `4535`.
- Si cambia el puerto mientras `Enable CAT` está desactivado, los servidores se iniciarán en el nuevo puerto la próxima vez que haga clic en `Enable CAT`.
- En Linux y macOS, cada canal expone un enlace simbólico PTY cuando la casilla de verificación de habilitación correspondiente está marcada. Dirija su software de registro a la ruta del enlace simbólico que se muestra debajo de la etiqueta de cada canal.
- En v26.5.3, los enlaces simbólicos PTY se crean por usuario en `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D` en Linux, o `~/Library/Caches/AetherSDR/cat-A` a `cat-D` en macOS. Este cambio con respecto a la ubicación anterior `/tmp/AetherSDR-CAT-*` corrige una vulnerabilidad de seguridad (GHSA-qxhr-cwrc-pvrm) y utiliza reemplazo atómico de enlaces simbólicos para prevenir condiciones de carrera de verificación de tiempo/uso de tiempo (TOCTOU).

## Solución de problemas

- **Los servidores no se reinician después de cambiar el puerto** — Confirme que presionó Enter o Tab para finalizar la edición del campo `Base:`. Hacer clic fuera sin confirmar la edición puede no aplicar el cambio.
- **El campo de puerto vuelve a 4532** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro de ese rango.
- **El servidor no se inicia en el nuevo puerto** — Otra aplicación puede estar usando ese puerto o uno de los tres puertos consecutivos. Elija un puerto base diferente.
- **Los enlaces simbólicos PTY no aparecen** — La función TTY está disponible solo en Linux y macOS. Confirme que marcó la casilla de habilitación para ese canal y que AetherSDR tiene acceso de escritura al directorio de tiempo de ejecución por usuario. En Linux suele ser `$XDG_RUNTIME_DIR/aethersdr/`; en macOS `~/Library/Caches/AetherSDR/`.

## Relacionado

- [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Autostart CAT servers with AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Check how many external clients are connected to each channel](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
