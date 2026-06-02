# Solucionar el problema de TUNE que no funciona tras actualizar al firmware 4.2 (configurar la conexión directa al TGXL)

El firmware 4.2 rompió la ruta interna del equipo para enviar el comando de sintonización automática al Tuner Genius XL. Desde AetherSDR v0.9.2.1, el botón TUNE puede omitir el firmware del equipo por completo conectándose directamente al TGXL a través del puerto 9010. Esta página explica cómo configurar esa conexión directa.

## Antes de comenzar

- Tiene instalado AetherSDR v0.9.2.1 o posterior.
- El TGXL está encendido y accesible desde el equipo que ejecuta AetherSDR (no solo desde el equipo de radio).
- Conoce la dirección IP del TGXL.
- Está conectado al equipo de radio. El botón de bandeja TUN es visible en la barra lateral derecha (el applet del sintonizador aparece solo cuando se detecta un Tuner Genius XL).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Seleccione la pestaña **Tuner**.
3. Ingrese la dirección IP de su TGXL y confirme que el puerto esté configurado en **9010**.
4. Haga clic en **Apply** o **OK** para guardar.
5. En la barra lateral derecha, haga clic en el botón de bandeja **TUN** para abrir el applet del sintonizador.
6. Haga clic en **TUNE**.

El botón se vuelve rojo y muestra **TUNING...** mientras se ejecuta el barrido de sintonización automática. Cuando finaliza, parpadea **SWR x.xx** durante aproximadamente 2.5 segundos y luego vuelve a **TUNE**.

## Consejos

- Cuando una conexión directa está activa, AetherSDR envía el comando nativo `autotune` directamente al TGXL a través del puerto 9010, omitiendo la ruta `tgxl autotune handle=<H>` a través del firmware del equipo que se rompió en la versión 4.2.
- Si no hay una conexión directa configurada, el botón TUNE recurre a la ruta del firmware del equipo. En el firmware 4.2, esa ruta puede no funcionar; configurar la conexión directa es la solución confiable.
- Con una conexión directa activa, las barras de relés C1, L y C2 también permiten el ajuste con la rueda del ratón, y la fila del conmutador de antena ANT 1 / ANT 2 / ANT 3 se vuelve visible si su TGXL tiene un conmutador 3x1.
- La escala del medidor de potencia se ajusta automáticamente según la configuración de su amplificador:
  - **Sin amplificador (0–200 W)**: Umbral amarillo a 80 W, umbral rojo a 125 W.
  - **Amplificador Aurora (0–600 W)**: Umbral amarillo a 400 W, umbral rojo a 500 W.
  - **Amplificador PGXL (0–2000 W)**: Umbral amarillo a 1000 W, umbral rojo a 1500 W.
- Las etiquetas PWR y SWR muestran valores en vivo actualizados desde el TGXL. Si no se recibe una lectura de potencia válida durante 800 ms, las etiquetas vuelven a sus nombres estáticos para evitar parpadeos por intervalos de paquetes.
- Aparece una marca de pico blanca en el indicador Fwd Pwr en la potencia más alta medida. La marca se borra automáticamente después de 2.5 segundos sin un nuevo pico.

## Solución de problemas

- **El botón TUNE muestra TUNING... pero nunca devuelve un resultado de SWR** — Es posible que el TGXL no sea accesible en el puerto 9010 desde su equipo. Verifique la dirección IP en `Settings > Radio Setup...` en la pestaña Tuner y confirme que no haya un cortafuegos bloqueando el puerto 9010 entre su equipo y el TGXL.
- **El botón de bandeja TUN no es visible** — El applet del sintonizador está oculto hasta que AetherSDR detecta un Tuner Genius XL. Confirme que el TGXL esté encendido y que el equipo de radio lo reconozca antes de abrir el applet.
- **El resultado de SWR parpadea con un valor muy alto después de la sintonización** — La ventana de captura de SWR posterior a la sintonización es de 400 ms. Si el TGXL informa la SWR estabilizada fuera de esa ventana, el valor mostrado puede no reflejar la concordancia final. Intente sintonizar nuevamente; el valor mostrado es la SWR más baja observada en la ventana de captura.
- **El indicador PWR muestra una disminución lenta o las etiquetas no se actualizan** — La balística de liberación lenta disminuye la barra durante ~800 ms para suavizar las ráfagas de RF. Las etiquetas se borran después de 800 ms sin datos para evitar parpadeos. Si las etiquetas permanecen en blanco, verifique la conexión del TGXL.

## Relacionado

- [Connect TGXL, PGXL or Antenna Genius by IP](connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Run an autotune on the external TGXL](../../features/tuner/run-an-autotune-on-the-external-tgxl.md)
- [Read SWR immediately after a tune](../../features/tuner/read-swr-immediately-after-a-tune.md)
- [Put the tuner in OPERATE, BYPASS, or STANDBY](../../features/tuner/put-the-tuner-in-operate-bypass-or-standby.md)
- [Fine-tune the C1/L/C2 relays with the mousewheel](../../features/tuner/fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Switch between three antennas on a TGXL 3x1](../../features/tuner/switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Tuner overview](../../features/tuner/overview.md)
