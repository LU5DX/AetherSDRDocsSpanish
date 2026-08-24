# Solucionar el fallo de TUNE tras actualizar al firmware 4.2 (configurar la conexión directa al TGXL)

El firmware 4.2 rompió la ruta interna de la radio para enviar el comando de autosintonía al Tuner Genius XL. Desde AetherSDR v0.9.2.1, el botón TUNE puede omitir por completo el firmware de la radio al conectarse directamente al TGXL en el puerto 9010. Esta página explica cómo configurar esa conexión directa.

## Antes de comenzar

- Tiene instalado AetherSDR v0.9.2.1 o posterior.
- Su TGXL está encendido y es accesible desde el equipo que ejecuta AetherSDR (no solo desde la radio).
- Conoce la dirección IP del TGXL.
- Está conectado a la radio. El botón de bandeja TUN es visible en la barra lateral derecha (el applet Tuner solo aparece cuando se detecta un Tuner Genius XL).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Seleccione la pestaña **Tuner**.
3. Introduzca la dirección IP de su TGXL y confirme que el puerto esté configurado en **9010**.
4. Haga clic en **Apply** o **OK** para guardar.
5. En la barra lateral derecha, haga clic en el botón de bandeja **TUN** para abrir el applet Tuner.
6. Haga clic en **TUNE**.

El botón se pone rojo y muestra **TUNING...** mientras se ejecuta el barrido de autosintonía. Al finalizar, parpadea **SWR x.xx** durante aproximadamente 2,5 segundos y luego vuelve a **TUNE**.

## Consejos

- Cuando hay una conexión directa activa, AetherSDR envía el comando nativo `autotune` directamente al TGXL a través del puerto 9010, omitiendo la ruta `tgxl autotune handle=<H>` a través del firmware de la radio que se rompió en la versión 4.2.
- Si no hay una conexión directa configurada, el botón TUNE recurre a la ruta del firmware de la radio. En el firmware 4.2, esa ruta puede no funcionar; configurar la conexión directa es la solución confiable.
- Con una conexión directa activa, las barras de relés C1, L y C2 también permiten el ajuste con la rueda del mouse, y la fila de conmutación de antenas ANT 1 / ANT 2 / ANT 3 se vuelve visible si su TGXL tiene un conmutador 3x1.
- La escala del medidor de potencia se ajusta automáticamente según la configuración de su amplificador:
  - **Barefoot (0–200 W)**: umbral amarillo en 80 W, umbral rojo en 125 W.
  - **Amplificador Aurora (0–600 W)**: umbral amarillo en 400 W, umbral rojo en 500 W.
  - **Amplificador PGXL (0–2000 W)**: umbral amarillo en 1000 W, umbral rojo en 1500 W.
- Las etiquetas PWR y SWR muestran valores en vivo actualizados desde el TGXL. Si no se recibe una lectura de potencia válida durante 800 ms, las etiquetas vuelven a sus nombres estáticos para evitar el parpadeo por intervalos en los paquetes.
- Aparece una marca de pico blanca en el medidor Fwd Pwr en la potencia más alta medida. La marca se borra automáticamente después de 2,5 segundos sin un nuevo pico.
- El medidor SWR se ajusta a 1.0 (vacío) cuando la potencia directa es inferior a 5 W (el umbral del piso de ruido). Esto evita que las lecturas de ruido en reposo iluminen la barra SWR. El valor SWR bruto se conserva internamente para la lógica de captura posterior a la sintonía.
- En v26.8.4, la escala de potencia ya no se vuelve a aplicar en cada actualización de estado de la radio. La escala solo se actualiza cuando el estado del amplificador o la potencia máxima realmente cambian, lo que reduce los redibujados innecesarios y mejora la respuesta de la interfaz.

## Solución de problemas

- **El botón TUNE muestra TUNING... pero nunca devuelve un resultado SWR** — El TGXL puede no ser accesible en el puerto 9010 desde su equipo. Verifique la dirección IP en `Settings > Radio Setup...` en la pestaña Tuner, y confirme que no haya un firewall bloqueando el puerto 9010 entre su equipo y el TGXL.
- **El botón de bandeja TUN no es visible** — El applet Tuner está oculto hasta que AetherSDR detecta un Tuner Genius XL. Confirme que el TGXL esté encendido y que la radio lo reconozca antes de abrir el applet.
- **El resultado SWR parpadea con un valor muy alto después de la sintonía** — La ventana de captura SWR posterior a la sintonía es de 400 ms. Si el TGXL informa el SWR estabilizado fuera de esa ventana, el valor mostrado puede no reflejar la adaptación final. Intente sintonizar nuevamente; el valor mostrado es el SWR más bajo visto en la ventana de captura.
- **El medidor PWR muestra una caída lenta o las etiquetas no se actualizan** — La balística de liberación lenta decae la barra en ~800 ms para suavizar las ráfagas de RF. Las etiquetas se borran después de 800 ms sin datos para evitar parpadeos. Si las etiquetas permanecen en blanco, verifique la conexión al TGXL.
- **El medidor SWR muestra 1.0 en todo momento incluso con potencia directa** — Verifique que la potencia directa supere los 5 W. El medidor SWR solo muestra valores en vivo cuando la potencia directa es igual o superior a 5 W.

## Relacionado

- [Conectar TGXL, PGXL o Antenna Genius por IP](connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Ejecutar una autosintonía en el TGXL externo](../../features/tuner/run-an-autotune-on-the-external-tgxl.md)
- [Leer SWR inmediatamente después de una sintonía](../../features/tuner/read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](../../features/tuner/put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del mouse](../../features/tuner/fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Cambiar entre tres antenas en un TGXL 3x1](../../features/tuner/switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Descripción general del sintonizador](../../features/tuner/overview.md)
