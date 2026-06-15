# Verifique el Voltaje de Alimentación de CC en Vivo de la Radio

El applet Medidores muestra el voltaje de alimentación reportado en vivo por la radio. Úselo para confirmar que su fuente de alimentación de CC se encuentra dentro de un rango saludable durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Medidores requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón **MTR** de la bandeja en la barra lateral derecha para abrir el applet Medidores.
2. Lea el indicador **+13.8V**. La etiqueta en el centro de la barra se actualiza en vivo para mostrar el voltaje actual, por ejemplo, `+13.82V`.

## Qué hace cada control

| Indicador | Rango válido | Rojo por encima de | Comportamiento | Accesibilidad |
|-----------|--------------|---------------------|----------------|---------------|
| +13.8V | 10.0–16.0 V | 15 V | Muestra el voltaje de alimentación reportado por la radio. La etiqueta del indicador se actualiza dinámicamente para reflejar el valor en vivo (ej. `+13.82V`). | Nombre accesible: "Supply voltage" |
| PA Temp | 0–120 °C | 70 °C | Muestra la lectura del medidor PATEMP de la radio. | Nombre accesible: "PA temperature" |
| Main Fan | 0–3000 rpm | 2500 rpm | Muestra el valor del medidor MAINFAN de la radio. | Nombre accesible: "Main fan speed" |

No existe una clave de configuración persistente para estos indicadores. No tienen valores predeterminados configurables.

## Notas de accesibilidad

Cada indicador tiene un nombre accesible configurado para compatibilidad con lectores de pantalla:
- Indicador PA Temp: "PA temperature"
- Indicador de voltaje de alimentación: "Supply voltage"
- Indicador Main Fan: "Main fan speed"

Estos nombres se anuncian cuando el indicador recibe el foco o se navega hasta él con tecnología de asistencia.

## Consejos

- La etiqueta del indicador cambia en cada actualización de telemetría de la radio, por lo que el valor mostrado en el centro de la barra siempre está actualizado; no es un marcador de posición estático.
- La barra se llena de color cian en el rango normal y se vuelve roja por encima de 15 V. Una barra roja indica un voltaje de alimentación que supera el rango operativo esperado.
- El indicador de temperatura del PA se vuelve rojo por encima de 70 °C. Si esto ocurre, reduzca la potencia de transmisión o el ciclo de trabajo.
- El indicador Main Fan se vuelve rojo por encima de 2500 rpm. Esto es normal durante la operación de alta potencia e indica que el ventilador de refrigeración funciona según lo esperado.

## Solución de problemas

- **El indicador no muestra movimiento o tiene una etiqueta fija** — La radio no está conectada o el flujo de telemetría no ha comenzado. Confirme el estado de la conexión y vuelva a conectar mediante `Settings > Connect to Radio...`.

## Relacionados

- [Resumen de medidores](overview.md)
- [Vigile la temperatura del PA durante sobretiempos largos](watch-pa-temperature-during-long-overs.md)
- [Supervise la velocidad del ventilador de refrigeración principal](monitor-the-main-cooling-fan-speed.md)
