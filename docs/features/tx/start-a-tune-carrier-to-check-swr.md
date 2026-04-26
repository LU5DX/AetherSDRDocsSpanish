# Transmitir una portadora de ajuste para verificar el ROS

Use la función TUNE para transmitir una portadora continua a potencia reducida y, a continuación, lea el medidor de ROS para verificar su sistema de antena antes de realizar un contacto.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Consulte `Settings > Connect to Radio...` si no está conectado.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón **TX** de la bandeja en la barra lateral derecha.
- Establezca un nivel de potencia de ajuste adecuado. El valor predeterminado es 10 (de 100). Consulte [Establecer la potencia de la portadora de ajuste](set-tune-carrier-power.md) si necesita cambiarlo.
- Confirme que tiene permiso para transmitir en la frecuencia actual (banda correcta, clase de licencia y cualquier configuración de inhibición requerida).

## Pasos

1. Abra el applet TX Controls haciendo clic en el botón **TX** de la bandeja en la barra lateral derecha si no está ya abierto.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10. Ajústelo si es necesario arrastrando el control.
3. Haga clic en **TUNE**.
4. La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo. El radio está transmitiendo ahora una portadora continua.
5. Lea el medidor **SWR**. La escala va de 1.0 a 3.0; la pantalla se vuelve roja por encima de 2.5.
6. Haga clic en **TUNE** nuevamente para detener la portadora. La etiqueta del botón regresa a **TUNE**.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|---|
| **Tune Pwr** | Deslizador | 10 | 0–100 | Establece el nivel de potencia de la portadora de ajuste. |
| **TUNE** | Botón | — | — | Haga clic para iniciar la portadora de ajuste; haga clic de nuevo para detenerla. La etiqueta muestra **TUNING...** con fondo rojo mientras está activo. |
| **SWR** | Medidor | — | 1.0–3.0 (rojo por encima de 2.5) | Muestra la relación de onda estacionaria en el excitador durante la transmisión. |
| **RF Pwr** | Medidor | — | 0–120 W sin amplificador; 0–600 W Aurora 500W (rojo por encima de 100 W / 500 W) | Muestra la potencia directa en la salida del excitador durante la portadora de ajuste. |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) para proteger sus transistores finales y cualquier amplificador externo mientras verifica el ROS.
- La portadora de ajuste opera al nivel de **Tune Pwr**, no al nivel de **RF Power**. Cambiar **RF Power** durante el ajuste no tiene efecto sobre la potencia de la portadora.
- Si desea suprimir una línea de salida TX específica durante el ajuste, use `Settings > Inhibit during TUNE` para seleccionar ACC TX, TX1, TX2 o TX3 antes de hacer clic en **TUNE**.

## Solución de problemas

- **El botón TUNE no tiene efecto** — Verifique que la conexión con el radio esté activa. El applet TX Controls requiere una conexión de radio en funcionamiento; el botón **TX** de la bandeja y todos los controles están deshabilitados cuando el radio está desconectado.
- **El ROS muestra un valor alto inmediatamente** — Verifique la conexión de la antena, el cable coaxial y la posición de cualquier conmutador. Una lectura igual o superior a 2.5 activa la zona roja del medidor de ROS.
- **TUNING... no se detiene** — Haga clic en **TUNE** una segunda vez para enviar el comando de detención. Si el botón no responde, verifique si hay una interrupción de red con el radio.

## Relacionados

- [Establecer la potencia de la portadora de ajuste](set-tune-carrier-power.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar el sintonizador automático interno](run-the-internal-atu.md)
- [Activar MOX para accionar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Descripción general de TX Controls](overview.md)
