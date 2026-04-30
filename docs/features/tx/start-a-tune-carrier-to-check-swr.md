# Iniciar un portadora de sintonía para verificar ROS

Envíe una portadora continua a potencia reducida para leer el ROS en su sistema de antena. Utilice esto antes de un QSO o después de cambiar antenas para confirmar una buena adaptación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX Controls solo está activo con una conexión de radio activa.
- Asegúrese de que está autorizado a transmitir en la frecuencia (la banda debe estar abierta a su estación legalmente).
- Establezca la potencia de sintonía a un nivel apropiado para su sistema de antena. El valor predeterminado es 10; consulte [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón de bandeja TX en la barra lateral derecha para abrir el applet TX Controls si no está ya visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10 (de 100). Ajuste si es necesario antes de transmitir.
3. Haga clic en **TUNE**.
   - La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo mientras la portadora está activa.
   - El medidor **SWR** se actualiza en tiempo real. La escala va de 1,0 a 3,0; las lecturas superiores a 2,5 se muestran en rojo.
   - El medidor **RF Pwr** muestra la potencia directa en la salida del excitador.
4. Lea el valor de ROS del medidor **SWR**.
5. Haga clic en **TUNE** nuevamente para detener la portadora.
   - La etiqueta del botón vuelve a **TUNE** y el fondo rojo se borra.

## Qué hace cada control

| Control      | Tipo        | Predeterminado |
|--------------|-------------|---------|
| **TUNE**     | Botón de pulso | —       |
| **Tune Pwr** | Control deslizante      | 10      |
| **RF Pwr**   | Medidor       | —       |
| **SWR**      | Medidor       | —       |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) al probar un sistema de antena desconocido. Auméntelo solo después de confirmar un ROS razonable.
- El medidor **SWR** se vuelve rojo por encima de 2,5. Si se detiene en 3,0, detenga la portadora y verifique su línea de alimentación y las conexiones de la antena antes de continuar.
- Para ejecutar el ATU interno en lugar de verificar el ROS manualmente, haga clic en **ATU** después de que la portadora de sintonía confirme que la antena es utilizable. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- Si desea inhibir salidas TX específicas (ACC TX, TX1, TX2, TX3) durante la sintonía, configúrelas en `Settings > Inhibit during TUNE`.

## Solución de problemas

- **El botón TUNE no hace nada** — El applet requiere una conexión de radio activa. Verifique que AetherSDR muestre la radio como conectada antes de intentar transmitir.
- **El medidor SWR no se mueve durante TUNE** — La potencia directa puede estar en o cerca de cero. Verifique que el control deslizante **Tune Pwr** esté por encima de 0 y que el puerto de antena correcto esté seleccionado para la banda actual.
- **La portadora no se detiene** — Haga clic en **TUNE** una vez más. Si el botón permanece en el estado **TUNING...**, verifique la conexión de la radio; una conexión perdida puede dejar el estado de transmisión sin confirmar.

## Relacionado

- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria de ATU](recall-an-atu-memory.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Alternar MOX para modular manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
