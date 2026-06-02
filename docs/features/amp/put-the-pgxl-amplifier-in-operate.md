# Poner el amplificador PGXL en OPERATE

Esta página explica cómo cambiar un amplificador Power Genius XL conectado de STANDBY a OPERATE usando el applet Amplificador de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Amplificador está oculto hasta que la radio detecte un Power Genius XL.
- El PGXL debe estar encendido y comunicándose con la radio Flex para que llegue la telemetría de estado. El botón OPERATE está oculto hasta que se reciba la primera actualización de estado.

## Pasos

1. Localice el botón AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet Amplificador.
3. Confirme que el botón en el applet muestra "STANDBY". Esto significa que el PGXL está actualmente en espera.
4. Haga clic en STANDBY. La etiqueta del botón cambia a "OPERATE" y se vuelve verde, indicando que el amplificador está ahora en OPERATE.

## Qué hace cada control

| Control | Comportamiento                                                                                                                                                                                                                                                                | Notas                                                                                                                                                                                                                                                                                                                              |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OPERATE | Alterna el amplificador entre OPERATE y STANDBY; emite operateToggled.                                                                                                                                                                                                       | Oculto hasta que llega setState. Muestra 'OPERATE' (verde) para los estados IDLE/OPERATE/TRANSMIT_*, 'STANDBY' en caso contrario. En v0.9.8, setState se llama desde RadioModel::ampStateChanged (autoritativo), evitando que el botón se quede atascado con la etiqueta antigua (#2437).                                           |
| STANDBY | Cuando el botón muestra "STANDBY" (estilo predeterminado), el PGXL está en STANDBY, POWERUP o FAULT. Haga clic para enviar el amplificador a OPERATE.                                                                                                                         | Es el mismo botón; la etiqueta y el color cambian según el estado.                                                                                                                                                                                                                                                                 |
| PWR     | Etiqueta del lado izquierdo que muestra el valor actual de potencia directa (ej., "PWR 1148"), seguida de un medidor de barra horizontal que muestra la potencia de salida directa. Rango: 0–2000 W. La barra se vuelve roja por encima de 1500 W. El medidor usa suavizado balístico: sube rápido, disminuye en ~800 ms. | La etiqueta del medidor se eliminó del interior del medidor; el valor en vivo aparece en la etiqueta PWR a la izquierda. Introducido en v26.6.1.                                                                                                                                                                                   |
| SWR     | Etiqueta del lado izquierdo que muestra el valor actual de ROE (ej., "SWR 1.2"), seguida de un medidor de barra horizontal que muestra la ROE. Rango: 1.0–3.0. La barra se vuelve roja por encima de 2.5.                                                                  | La etiqueta del medidor se eliminó del interior del medidor; el valor en vivo aparece en la etiqueta SWR a la izquierda. Introducido en v26.6.1.                                                                                                                                                                                   |
| Id      | Etiqueta del lado izquierdo que muestra el valor actual de corriente de drenaje (ej., "Id 12.5"), seguida de un medidor de barra horizontal que muestra la corriente de drenaje del PGXL. Rango: 0–70 A. La barra se vuelve roja por encima de 60 A.                         | Reemplaza el antiguo medidor Temp. La lectura de temperatura ahora aparece en la pila de información debajo. Introducido en v26.6.1.                                                                                                                                                                                               |
| Temp    | Etiqueta de texto que muestra la temperatura del disipador en grados Celsius (ej., "— C" antes de que lleguen los datos). Aparece en la pila de información junto con Vdd y Vac.                                                                                            | Anteriormente era un medidor horizontal; ahora es una etiqueta de texto en el área de información inferior.                                                                                                                                                                                                                        |
| Vdd     | Etiqueta de texto que muestra el voltaje de drenaje del PGXL (ej., "Vdd  50 V"). Aparece en la pila de información.                                                                                                                                                        | Reemplaza el antiguo indicador "Volts / Amps". Introducido en v26.6.1.                                                                                                                                                                                                                                                             |
| Vac     | Etiqueta de texto que muestra el voltaje de red del PGXL (ej., "Vac  240 V"). Aparece en la pila de información.                                                                                                                                                            | Nuevo en v26.6.1.                                                                                                                                                                                                                                                                                                                  |
| R       | Etiqueta de texto que muestra la fuente de datos (ej., "● RADIO" en gris). Aparece en la pila de información debajo de Vac.                                                                                                                                                 | Nuevo en v26.6.1. Indica que la telemetría proviene de la radio/proxy.                                                                                                                                                                                                                                                             |

## Consejos

- Si el panel de applets no está visible, vaya a `View > Applet Panel` para mostrarlo.
- El botón OPERATE refleja el estado informado del PGXL, no una alternancia registrada localmente. Si el amplificador entra en FAULT o POWERUP, el botón vuelve a "STANDBY" automáticamente.
- El medidor PWR usa suavizado balístico: sube rápido cuando hay RF presente, pero disminuye en ~800 ms para que las transmisiones breves sigan siendo visibles. Esto coincide con la sensación de retención de pico del S-meter.
- La pila de información (Temp, Vdd, Vac, indicador de fuente) solo aparece después de que llegan los primeros datos de telemetría del PGXL.

## Solución de problemas

- **El botón AMP en la bandeja no aparece** — La radio no ha detectado ningún Power Genius XL. Confirme que el PGXL esté encendido y correctamente conectado a la radio Flex.
- **El botón OPERATE no es visible dentro del applet** — El applet se ha abierto pero aún no ha llegado telemetría de estado del PGXL. Espere un momento; el botón aparece después de la primera actualización de estado.
- **El botón muestra "STANDBY" inmediatamente después de hacer clic** — El PGXL puede estar en FAULT o POWERUP y no puede entrar en OPERATE. Verifique el panel frontal del amplificador en busca de indicadores de falla.
- **El medidor PWR o SWR no muestra ningún valor** — Aún no se ha recibido telemetría. Confirme que el PGXL se está comunicando con la radio Flex.

## Relacionados

- [Descripción general del amplificador](overview.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Ver la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
