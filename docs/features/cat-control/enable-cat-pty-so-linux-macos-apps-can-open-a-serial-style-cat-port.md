# Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto serie virtual

CAT PTY crea cuatro enlaces simbólicos de puertos serie virtuales que los programas de registro y concurso pueden abrir como si fueran dispositivos serie físicos. Utilice esta función en Linux o macOS cuando su aplicación externa requiera una ruta de puerto serie en lugar de una conexión TCP.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT Control requiere una conexión activa al radio.
- La función PTY solo está disponible en Linux y macOS.
- Abra el applet CAT Control haciendo clic en el botón **CAT** en la barra lateral derecha. El applet está oculto de forma predeterminada.

## Pasos

1. Haga clic en el botón **CAT** en la barra lateral derecha para abrir el applet CAT Control.
2. Haga clic en **Enable TTY**.

   El botón se vuelve verde cuando está activo. AetherSDR crea cuatro enlaces simbólicos:

   - Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` a `cat-D`
   - macOS: `~/Library/Caches/AetherSDR/cat-A` a `cat-D`

3. En su aplicación externa, configure la ruta del puerto serie al enlace simbólico del canal que desea controlar; por ejemplo, en Linux: `$XDG_RUNTIME_DIR/aethersdr/cat-A` para el canal A.
4. Cada fila de canal en el applet se actualiza para mostrar la ruta PTY activa una vez que el enlace simbólico está en funcionamiento.

## Función de cada control

| Control              | Valor predeterminado | Rango válido |
|----------------------|----------------------|--------------|
| **Enable TTY**       | Apagado              | Encendido / Apagado |
| **Enable TCP**       | Apagado              | Encendido / Apagado |
| **Base**             | `4532`               | 1024–65535   |
| Filas de canal A/B/C/D | `(detenido)`       | —            |

## Consejos

- Cada canal (A, B, C, D) se asigna a un slice del radio. Dirija su software de registro al enlace simbólico que corresponde al slice que desea controlar.
- Para que AetherSDR inicie los enlaces simbólicos PTY automáticamente al iniciar, habilite `Settings > Autostart CAT with AetherSDR`.
- Puede ejecutar **Enable TTY** y **Enable TCP** de forma independiente. Habilitar uno no requiere habilitar el otro.
- En la versión v26.5.3, la ubicación del enlace simbólico PTY se movió de `/tmp` a directorios de tiempo de ejecución por usuario para endurecer la seguridad (GHSA-qxhr-cwrc-pvrm). Los enlaces simbólicos se crean de forma atómica para prevenir condiciones de carrera TOCTOU.

## Solución de problemas

- **Enable TTY no tiene efecto o los enlaces simbólicos no aparecen** — El soporte PTY requiere Linux o macOS. La función no está disponible en Windows.
- **La aplicación externa no puede abrir el puerto** — Confirme que la aplicación esté usando la ruta correcta. En Linux, ejecute `echo $XDG_RUNTIME_DIR/aethersdr/cat-A` para resolver la ruta completa. En macOS, use `~/Library/Caches/AetherSDR/cat-A`. Verifique que **Enable TTY** siga activo (el botón debe estar verde) y que AetherSDR permanezca conectado al radio.
- **La ruta del enlace simbólico mostrada en la fila no coincide con `/tmp/AetherSDR-CAT-A`** — A partir de v26.5.3, los enlaces simbólicos ya no se crean en `/tmp`. La ruta mostrada se actualiza a la ruta real del dispositivo PTY bajo el directorio de tiempo de ejecución por usuario. Use la ruta que se muestre en la fila del canal.
- **La ruta del enlace simbólico se muestra en lugar de una ruta en ejecución** — La ruta mostrada se actualiza al formato `RigctlPty::defaultSymlinkPath(i)` cuando el servidor está detenido, coincidiendo con el esquema de ubicación por usuario.

## Relacionados

- Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Resumen de CAT Control](overview.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
