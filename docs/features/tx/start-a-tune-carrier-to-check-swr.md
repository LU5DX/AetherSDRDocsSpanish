# Iniciar un portador de sintonía para verificar el ROS

Use la función TUNE para transmitir un portador estable a potencia reducida y así leer el ROS sin establecer un contacto. Esta es la forma estándar de verificar el ajuste de la antena antes de operar.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls solo funciona cuando hay una conexión de radio activa.
- Confirme que la frecuencia y el modo estén configurados según lo que desea verificar.
- Ajuste "Tune Pwr" a un nivel seguro para su antena y cualquier amplificador conectado antes de transmitir.

## Pasos

1. Haga clic en el botón TX del panel lateral derecho para abrir el applet TX Controls si no está visible.
2. Ajuste el control deslizante "Tune Pwr" al nivel de potencia deseado para el portador de sintonía. El valor predeterminado es 10; el rango válido es 0–100.
3. Haga clic en TUNE. La etiqueta del botón cambia a "TUNING..." y el fondo del botón se vuelve rojo mientras el portador está activo.
4. Lea el medidor de ROS. El indicador "SWR" muestra la relación de onda estacionaria en el excitador. La escala va de 1.0 a 3.0; los valores superiores a 2.5 se muestran en rojo.
5. Haga clic en TUNE nuevamente (ahora etiquetado como "TUNING...") para detener el portador. El botón regresa a su etiqueta normal "TUNE".

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|---|
| TUNE | Botón | — | — | Inicia o detiene el portador de sintonía. Muestra "TUNING..." con fondo rojo mientras está activo. |
| Tune Pwr | Control deslizante | 10 | 0–100 | Establece el nivel de potencia del portador de sintonía enviado al radio. |
| SWR | Medidor | — | 1.0–3.0 (rojo > 2.5) | Muestra la relación de onda estacionaria en el excitador durante la transmisión. |
| RF Pwr | Medidor | — | 0–120 W sin amplificador; 0–600 W Aurora 500W (rojo > 100 W / > 500 W) | Muestra la potencia directa en la salida del excitador. |

## Consejos

- Mantenga "Tune Pwr" en el nivel mínimo necesario para obtener una lectura confiable del ROS. Un valor de 10 es suficiente para la mayoría de los analizadores de antena y sintonizadores internos.
- Si desea usar el ATU interno, puede iniciar la sintonía del ATU directamente con el botón ATU; el ciclo del ATU utiliza el portador de sintonía automáticamente. Consulte [Usar el ATU interno](run-the-internal-atu.md).

## Solución de problemas

- **El botón TUNE no tiene efecto** — El applet TX Controls requiere una conexión de radio activa. Verifique que AetherSDR esté conectado al FLEX-8600 mediante `Settings > Connect to Radio...`.
- **El indicador SWR permanece en 1.0 durante la sintonía** — Es posible que el radio no esté detectando potencia reflejada. Verifique que el conector de antena y la línea de alimentación estén correctamente conectados al radio.
- **El portador no se detiene** — Si al hacer clic en el botón por segunda vez no se detiene la sintonía, es posible que el radio haya perdido el comando. Haga clic en MOX una vez para forzar el apagado del transmisor y luego haga clic en MOX nuevamente para volver a recepción.

## Relacionados

- [Configurar la potencia del portador de sintonía](set-tune-carrier-power.md)
- [Usar el ATU interno](run-the-internal-atu.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Usar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
