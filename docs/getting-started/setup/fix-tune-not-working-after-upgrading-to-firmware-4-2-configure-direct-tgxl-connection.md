# Solución para TUNE que no funciona tras actualizar al firmware 4.2 (configurar conexión directa con TGXL)

El firmware 4.2 interrumpió la ruta interna del transceptor para enviar el comando de autosintonía al Tuner Genius XL. Desde AetherSDR v0.9.2.1, el botón TUNE puede omitir completamente el firmware del transceptor conectándose al TGXL directamente por el puerto 9010. Esta página explica cómo configurar esa conexión directa.

## Antes de comenzar

- AetherSDR v0.9.2.1 o posterior está instalado.
- Su TGXL está encendido y es accesible desde el equipo que ejecuta AetherSDR (no solo desde el transceptor).
- Conoce la dirección IP del TGXL.
- Está conectado al transceptor. El botón de bandeja TUN es visible en la barra lateral derecha (el applet del sintonizador aparece únicamente cuando se detecta un Tuner Genius XL).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Seleccione la pestaña **Tuner**.
3. Ingrese la dirección IP de su TGXL y confirme que el puerto esté configurado en **9010**.
4. Haga clic en **Apply** u **OK** para guardar.
5. En la barra lateral derecha, haga clic en el botón de bandeja **TUN** para abrir el applet del sintonizador.
6. Haga clic en **TUNE**.

El botón se vuelve rojo y muestra **TUNING...** mientras se ejecuta el barrido de autosintonía. Al finalizar, parpadea **SWR x.xx** durante aproximadamente 2.5 segundos y luego regresa a **TUNE**.

## Consejos

- Cuando hay una conexión directa activa, AetherSDR envía el comando nativo `autotune` directamente al TGXL por el puerto 9010, omitiendo la ruta `tgxl autotune handle=<H>` a través del firmware del transceptor que se interrumpió en la versión 4.2.
- Si no hay ninguna conexión directa configurada, el botón TUNE recurre a la ruta del firmware del transceptor. En el firmware 4.2 esa ruta puede no funcionar; configurar la conexión directa es la solución confiable.
- Con una conexión directa activa, las barras de relés C1, L y C2 también permiten el ajuste con la rueda del ratón, y la fila del selector de antena ANT 1 / ANT 2 / ANT 3 se vuelve visible si su TGXL tiene un conmutador 3x1.

## Solución de problemas

- **El botón TUNE muestra TUNING... pero nunca devuelve un resultado de SWR** — Es posible que el TGXL no sea accesible por el puerto 9010 desde su equipo. Verifique la dirección IP en `Settings > Radio Setup...` bajo la pestaña Tuner, y confirme que ningún firewall esté bloqueando el puerto 9010 entre su equipo y el TGXL.
- **El botón de bandeja TUN no es visible** — El applet del sintonizador permanece oculto hasta que AetherSDR detecta un Tuner Genius XL. Confirme que el TGXL esté encendido y que el transceptor lo reconozca antes de abrir el applet.
- **El resultado de SWR muestra un valor muy alto tras la sintonía** — La ventana de captura de SWR posterior a la sintonía es de 400 ms. Si el TGXL reporta el SWR estabilizado fuera de esa ventana, el valor mostrado puede no reflejar el ajuste final. Intente la sintonía nuevamente; el valor mostrado es el SWR más bajo detectado en la ventana de captura.

## Relacionados

- [Conectar TGXL, PGXL o Antenna Genius por IP](connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Ejecutar una autosintonía en el TGXL externo](../../features/tuner/run-an-autotune-on-the-external-tgxl.md)
- [Leer el SWR inmediatamente después de una sintonía](../../features/tuner/read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](../../features/tuner/put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](../../features/tuner/fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Cambiar entre tres antenas en un TGXL 3x1](../../features/tuner/switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Descripción general del sintonizador](../../features/tuner/overview.md)
