# Iniciar una portadora de ajuste para verificar la ROS

Transmita una portadora continua a potencia reducida para leer la ROS en el medidor antes de establecer un contacto o ejecutar el ATU.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls requiere una conexión activa con el radio.
- La antena y la línea de alimentación deben estar conectadas al radio.
- Ajuste "Tune Pwr" a un nivel seguro para su sistema de antena antes de activar la portadora. El valor predeterminado es 10.

## Pasos

1. Haga clic en el botón de bandeja **TX** en la barra lateral derecha para abrir el applet TX Controls.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10. Ajústelo si necesita un nivel de salida diferente (rango válido: 0–100).
3. Haga clic en **TUNE**.
   La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo. El radio transmite una portadora continua.
4. Lea el medidor **SWR**. La escala va de 1.0 a 3.0; el indicador se vuelve rojo por encima de 2.5.
5. Haga clic en **TUNING...** para detener la portadora.
   El botón regresa a la etiqueta **TUNE**.

## Función de cada control

| Control | Tipo | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|---|
| **Tune Pwr** | Control deslizante | 10 | 0–100 | Establece el nivel de potencia de salida utilizado durante la portadora de ajuste. |
| **TUNE** | Botón | — | — | El primer clic inicia la portadora (la etiqueta cambia a **TUNING...**). Haga clic de nuevo para detenerla. |
| **SWR** | Medidor | — | 1.0–3.0 (rojo por encima de 2.5) | Muestra la relación de onda estacionaria en la salida del excitador mientras la portadora está activa. |
| **RF Pwr** | Medidor | — | 0–120 W sin amplificador; 0–600 W Aurora 500W (rojo por encima de 100 W / 500 W) | Muestra la potencia directa en la salida del excitador. |

## Consejos

- Mantenga **Tune Pwr** bajo (10–20) para una verificación inicial. Auméntelo solo si su medidor de ROS necesita más señal para obtener una lectura estable.
- El medidor **SWR** está activo siempre que el radio esté transmitiendo, no únicamente durante **TUNE**. También puede leerlo mientras usa **MOX**.
- Para inhibir salidas de TX específicas durante el ajuste, use `Settings > Inhibit during TUNE` y seleccione las salidas que desea suprimir.

## Solución de problemas

- **El botón TUNE aparece desactivado** — El radio no está conectado. Verifique el estado de la conexión y consulte `Settings > Connect to Radio...`.
- **El medidor SWR indica 1.0 y RF Pwr indica 0 durante TUNE** — La portadora se inició, pero ninguna potencia llega al medidor. Verifique la selección del puerto de antena en `Settings > Radio Setup...` y confirme que la línea de alimentación está conectada.
- **La portadora no se detiene al hacer clic en TUNING...** — Haga clic en el botón una vez con firmeza. Si el problema persiste, haga clic en **MOX** para forzar al radio a salir del modo de transmisión y, a continuación, verifique que el firmware del radio sea la versión 4.1.5.

## Temas relacionados

- [Ajustar la potencia de la portadora de ajuste](set-tune-carrier-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Usar MOX para activar el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Descripción general de TX Controls](overview.md)
