# Monitorear la velocidad del ventilador principal de refrigeración

El applet Meters incluye un indicador "Main Fan" que muestra en tiempo real la velocidad del ventilador principal de refrigeración del FLEX-8600. Úselo para confirmar que el ventilador está en funcionamiento y para detectar velocidades anormalmente altas que puedan indicar estrés térmico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si no lo está, habilítelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón de bandeja **MTR** en la barra lateral derecha para abrir el applet Meters.
2. Observe el indicador **Main Fan** bajo el encabezado de sección "Radio Hardware".
3. Lea la velocidad actual del ventilador en la barra horizontal. El rango del indicador es de 0–3000 rpm. La barra se vuelve roja por encima de 2500 rpm.

## Qué hace cada control

| Control | Descripción | Rango válido | Línea roja |
|---|---|---|---|
| Main Fan | Muestra la velocidad del ventilador principal de refrigeración de la radio. | 0–3000 rpm | > 2500 rpm (la barra se vuelve roja) |
| PA Temp | Muestra la temperatura del PA. | 0–120 °C | > 70 °C |
| +13.8V | Muestra el voltaje de alimentación de CC. | 10.0–16.0 V | > 15 V |

## Consejos

- El indicador Main Fan se actualiza con cierta demora: la primera lectura puede aparecer un momento después de abrir el applet, una vez que la radio reporta el valor del medidor.
- La barra se llena en cian, pasa por una zona amarilla y se vuelve roja a partir de 2500 rpm. Lecturas sostenidas en rojo durante transmisiones prolongadas pueden indicar ventilación insuficiente alrededor de la radio.

## Solución de problemas

- **El indicador Main Fan no muestra movimiento** — El índice del medidor se resuelve después de establecer la conexión con la radio. Si el indicador permanece en blanco, desconéctese y vuelva a conectarse a la radio, luego reabra el applet Meters.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Vigilar la temperatura del PA durante transmisiones prolongadas](watch-pa-temperature-during-long-overs.md)
- [Verificar el voltaje de alimentación de CC de la radio](check-the-radio-s-dc-supply-voltage.md)
