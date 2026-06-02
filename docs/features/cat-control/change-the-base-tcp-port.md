# Cambiar el puerto TCP base

El applet de Control CAT ejecuta hasta cuatro servidores TCP compatibles con rigctld en puertos consecutivos a partir de una base configurable. Cambie el puerto base cuando el valor predeterminado entre en conflicto con otra aplicación en su sistema.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet CAT requiere una conexión de radio activa.
- Abra el applet Control CAT haciendo clic en el botón de la bandeja CAT en la barra lateral derecha, si aún no está visible.

## Pasos

1. En el applet Control CAT, localice la etiqueta `Base:` y su campo de texto en la parte inferior del applet.
2. Haga clic en el campo `Base:` y escriba el nuevo número de puerto. Rango válido: 1024–65535. Valor predeterminado: `4532`.
3. Presione Enter o Tab para confirmar. Si el valor está fuera del rango válido, vuelve automáticamente a `4532`.
4. El nuevo puerto base se guarda inmediatamente en `CatTcpPort`.
5. Si `Enable TCP` está actualmente activo, los cuatro servidores se reinician automáticamente en los nuevos puertos (base, base+1, base+2, base+3). No se requiere ninguna acción adicional.

## Función de cada control

| Control       | Tipo           | Valor predeterminado | Comportamiento |
|---------------|----------------|----------------------|----------------|
| `Base:`       | Campo de texto | `4532`               | Puerto TCP base; los canales se vinculan al puerto, puerto+1, puerto+2, puerto+3. Los valores fuera de rango vuelven a 4532; los servidores se reinician con el nuevo puerto si están habilitados. |
| `Enable TCP`  | Botón de alternancia | Desactivado      | Inicia/detiene los cuatro servidores TCP rigctld en Base..Base+3. También persiste el puerto base actual en CatTcpPort. |
| `Enable TTY`  | Botón de alternancia | Desactivado      | Inicia/detiene los cuatro enlaces simbólicos PTY en `$XDG_RUNTIME_DIR/aethersdr/cat-A..D` (Linux) o `~/Library/Caches/AetherSDR/cat-A..D` (macOS). |
| Filas de canales A/B/C/D | Indicador | `(stopped)` | Cada fila muestra la insignia del canal, el estado TCP y la ruta PTY. Insignias codificadas por color de segmento. El estado TCP por canal muestra `(stopped)` o `:<puerto> (1 cliente)` o `:<puerto> (N clientes)`. |

## Consejos

- Elija un puerto base que deje libres los tres puertos consecutivos siguientes. Por ejemplo, una base de `4532` utiliza `4532`, `4533`, `4534` y `4535`.
- Si cambia el puerto mientras `Enable TCP` está desactivado, los servidores se iniciarán en el nuevo puerto la próxima vez que haga clic en `Enable TCP`.
- En Linux y macOS, haga clic en `Enable TTY` para exponer cada canal como un puerto serie virtual. Dirija su software de registro a la ruta del enlace simbólico correspondiente que se muestra debajo de cada etiqueta de canal.
- En v26.5.3, los enlaces simbólicos PTY se crean por usuario en `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D` en Linux, o `~/Library/Caches/AetherSDR/cat-A` a `cat-D` en macOS. Este cambio con respecto a la ubicación anterior `/tmp/AetherSDR-CAT-*` corrige una vulnerabilidad de seguridad (GHSA-qxhr-cwrc-pvrm) y utiliza reemplazo atómico de enlaces simbólicos para evitar condiciones de carrera TOCTOU (tiempo de verificación/tiempo de uso).

## Solución de problemas

- **Los servidores no se reinician después de cambiar el puerto** — Confirme que presionó Enter o Tab para finalizar la edición del campo `Base:`. Hacer clic fuera sin confirmar la edición puede no aplicar el cambio.
- **El campo de puerto vuelve a 4532** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro de ese rango.
- **El servidor no se inicia en el nuevo puerto** — Otra aplicación puede estar usando ese puerto o uno de los tres puertos consecutivos. Elija un puerto base diferente.
- **Los enlaces simbólicos PTY no aparecen** — `Enable TTY` está disponible solo en Linux y macOS. Confirme que hizo clic en `Enable TTY` y que AetherSDR tiene acceso de escritura al directorio de tiempo de ejecución por usuario. En Linux, esto suele ser `$XDG_RUNTIME_DIR/aethersdr/`; en macOS `~/Library/Caches/AetherSDR/`.

## Relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
