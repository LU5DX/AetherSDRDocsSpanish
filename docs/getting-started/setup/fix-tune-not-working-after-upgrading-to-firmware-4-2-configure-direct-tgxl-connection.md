# Solucionar que TUNE no funcione tras actualizar al firmware 4.2 (configurar conexión directa TGXL)

El firmware 4.2 interrumpió la ruta interna de la radio para enviar el comando de sintonización automática al Tuner Genius XL. Desde AetherSDR v0.9.2.1, el botón TUNE puede omitir por completo el firmware de la radio conectándose directamente al TGXL en el puerto 9010. Esta página explica cómo configurar esa conexión directa.

## Antes de comenzar

- AetherSDR v0.9.2.1 o posterior está instalado.
- Su TGXL está encendido y accesible desde el ordenador que ejecuta AetherSDR (no solo desde la radio).
- Conoce la dirección IP del TGXL.
- Está conectado a la radio. El botón de bandeja TUN es visible en la barra lateral derecha (el applet del sintonizador aparece solo cuando se detecta un Tuner Genius XL).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Seleccione la pestaña **Tuner**.
3. Ingrese la dirección IP de su TGXL y confirme que el puerto esté configurado en **9010**.
4. Haga clic en **Apply** o **OK** para guardar.
5. En la barra lateral derecha, haga clic en el botón de bandeja **TUN** para abrir el applet del sintonizador.
6. Haga clic en **TUNE**.

El botón se vuelve rojo y muestra **TUNING...** mientras se ejecuta el barrido de sintonización automática. Al finalizar, parpadea **SWR x.xx** durante aproximadamente 2,5 segundos y luego vuelve a **TUNE**.

## Consejos

- Cuando hay una conexión directa activa, AetherSDR envía el comando nativo `autotune` directamente al TGXL a través del puerto 9010, omitiendo la ruta `tgxl autotune handle=<H>` a través del firmware de la radio que se interrumpió en la versión 4.2.
- Si no hay una conexión directa configurada, el botón TUNE recurre a la ruta del firmware de la radio. En el firmware 4.2, esa ruta puede no funcionar; configurar la conexión directa es la solución confiable.
- Con una conexión directa activa, las barras de relés C1, L y C2 también permiten ajuste con la rueda del ratón, y la fila del conmutador de antena ANT 1 / ANT 2 / ANT 3 se vuelve visible si su TGXL tiene un conmutador 3x1.

## Solución de problemas

- **El botón TUNE muestra TUNING... pero nunca devuelve un resultado de SWR** — Es posible que el TGXL no sea accesible en el puerto 9010 desde su ordenador. Verifique la dirección IP en `Settings > Radio Setup...` en la pestaña Tuner, y confirme que no haya un firewall bloqueando el puerto 9010 entre su ordenador y el TGXL.
- **El botón de bandeja TUN no es visible** — El applet del sintonizador permanece oculto hasta que AetherSDR detecta un Tuner Genius XL. Confirme que el TGXL esté encendido y que la radio lo reconozca antes de abrir el applet.
- **El resultado de SWR parpadea con un valor muy alto después de la sintonización** — La ventana de captura de SWR posterior a la sintonización es de 400 ms. Si el TGXL reporta la SWR estabilizada fuera de esa ventana, el valor mostrado puede no reflejar la adaptación final. Intente sintonizar nuevamente; el valor mostrado es la SWR más baja observada en la ventana de captura.

## Relacionado

- [Conectar TGXL, PGXL o Antenna Genius por IP](connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Ejecutar una sintonización automática en el TGXL externo](../../features/tuner/run-an-autotune-on-the-external-tgxl.md)
- [Leer SWR inmediatamente después de una sintonización](../../features/tuner/read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](../../features/tuner/put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](../../features/tuner/fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Cambiar entre tres antenas en un TGXL 3x1](../../features/tuner/switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Visión general del sintonizador](../../features/tuner/overview.md)
