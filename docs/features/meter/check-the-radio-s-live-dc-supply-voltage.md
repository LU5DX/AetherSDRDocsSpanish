# Verificar la Tensión de Alimentación en Vivo de la Radio

El applet Medidores muestra la tensión de alimentación reportada en vivo por la radio. Úselo para confirmar que su fuente de alimentación de CC se encuentra dentro de un rango saludable durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Medidores requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón **MTR** de la bandeja en la barra lateral derecha para abrir el applet Medidores.
2. Lea el indicador **+13.8V**. La etiqueta en el centro de la barra se actualiza en vivo para mostrar la tensión actual — por ejemplo, `+13.82V`.

## Descripción de cada control

| Indicador | Rango válido | Rojo por encima de | Comportamiento |
|-----------|--------------|--------------------|----------------|
| +13.8V    | 10.0–16.0 V  | 15 V               | Muestra la tensión de alimentación reportada por la radio. La etiqueta del indicador se actualiza dinámicamente para reflejar el valor en vivo (p.ej. `+13.82V`). |
| PA Temp   | 0–120 °C     | 70 °C              | Muestra la lectura del medidor PATEMP de la radio. |
| Main Fan  | 0–3000 rpm   | 2500 rpm           | Muestra el valor del medidor MAINFAN de la radio. |

No existe una clave de configuración persistente para estos indicadores. No tienen valores predeterminados configurables.

## Consejos

- La etiqueta del indicador cambia con cada actualización de telemetría de la radio, por lo que el valor mostrado en el centro de la barra siempre es actual — no es un marcador estático.
- La barra se llena de color cian en el rango normal y se vuelve roja por encima de 15 V. Una barra roja indica una tensión de alimentación por encima del rango de operación esperado.
- El indicador de temperatura del PA se vuelve rojo por encima de 70 °C. Si esto ocurre, reduzca la potencia de transmisión o el ciclo de trabajo.
- El indicador del ventilador principal se vuelve rojo por encima de 2500 rpm. Esto es normal durante la operación de alta potencia e indica que el ventilador de refrigeración está funcionando según lo esperado.

## Solución de problemas

- **El indicador no se mueve o muestra una etiqueta fija** — La radio no está conectada o el flujo de telemetría no se ha iniciado. Confirme el estado de la conexión y reconéctese mediante `Settings > Connect to Radio...`.

## Relacionados

- [Resumen de Medidores](overview.md)
- [Observar la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Monitorear la velocidad del ventilador principal de refrigeración](monitor-the-main-cooling-fan-speed.md)
