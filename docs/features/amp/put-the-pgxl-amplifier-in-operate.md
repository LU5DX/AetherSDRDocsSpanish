# Poner el amplificador PGXL en OPERATE

Esta página explica cómo cambiar un amplificador Power Genius XL conectado de STANDBY a OPERATE usando el applet Amplificador de AetherSDR.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet Amplificador está oculto hasta que la radio detecte un Power Genius XL.
- El PGXL debe estar encendido y comunicándose con la radio Flex para que haya llegado la telemetría de estado. El botón OPERATE está oculto hasta que se reciba la primera actualización de estado.

## Pasos

1. Localice el botón AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet Amplificador.
3. Confirme que el botón en el applet muestra "STANDBY". Esto significa que el PGXL está actualmente en espera.
4. Haga clic en STANDBY. La etiqueta del botón cambia a "OPERATE" y se vuelve verde, indicando que el amplificador está ahora en OPERATE.

## Qué hace cada control

| Control | Comportamiento                                                                                                                          | Notas                                                                                                                                                                                                                                                                                                      |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OPERATE | Alterna el amplificador entre OPERATE y STANDBY; emite operateToggled.                                                                  | Oculto hasta que llega setState. Muestra 'OPERATE' (verde) para estados IDLE/OPERATE/TRANSMIT_*, 'STANDBY' en caso contrario. En v0.9.8, setState se llama desde RadioModel::ampStateChanged (autoritativo), evitando que el botón se quede atascado en la etiqueta anterior (#2437).                       |
| STANDBY | Cuando el botón muestra "STANDBY" (estilo predeterminado), el PGXL está en STANDBY, POWERUP o FAULT. Haga clic para enviar el amplificador a OPERATE. | Mismo botón; la etiqueta y el color cambian según el estado.                                                                                                                                                                                                                                               |
| Fwd Pwr | Indicador de barra horizontal que muestra la potencia directa de salida. Rango: 0–2000 W. La barra se vuelve roja por encima de 1500 W. |                                                                                                                                                                                                                                                                                                            |
| SWR     | Indicador de barra horizontal que muestra la ROE. Rango: 1.0–3.0. La barra se vuelve roja por encima de 2.5.                           |                                                                                                                                                                                                                                                                                                            |
| Temp    | Indicador de barra horizontal que muestra la temperatura del disipador. Rango: 0–100 °C. La barra se vuelve roja por encima de 80 °C.   |                                                                                                                                                                                                                                                                                                            |

## Consejos

- Si el panel de applets no es visible, vaya a `View > Applet Panel` para mostrarlo.
- El botón OPERATE refleja el estado reportado por el PGXL, no una alternancia local. Si el amplificador entra en FAULT o POWERUP, el botón vuelve automáticamente a "STANDBY".

## Solución de problemas

- **El botón AMP no aparece** — La radio no ha detectado ningún Power Genius XL. Verifique que el PGXL esté encendido y correctamente conectado a la radio Flex.
- **El botón OPERATE no es visible dentro del applet** — El applet se ha abierto pero aún no ha llegado telemetría de estado del PGXL. Espere un momento; el botón aparece después de la primera actualización de estado.
- **El botón muestra "STANDBY" inmediatamente después de hacer clic** — El PGXL puede estar en FAULT o POWERUP y no puede entrar en OPERATE. Revise el panel frontal del amplificador en busca de indicadores de falla.

## Relacionados

- [Amplifier overview](overview.md)
- [Put the PGXL amplifier in STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Monitor forward power and SWR at the amplifier output](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Watch PGXL temperature, drain current, and mains voltage](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
