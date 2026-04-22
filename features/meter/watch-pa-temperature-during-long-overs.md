# Supervisar la temperatura del PA durante transmisiones prolongadas

El applet Meters muestra un indicador en vivo de PA Temp alimentado directamente desde la radio. Úselo durante períodos de transmisión extendidos para detectar la acumulación de calor antes de que active los circuitos de protección de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, use `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón MTR de la barra lateral derecha. El applet Meters se abre y muestra la sección **Radio Hardware** con tres indicadores horizontales.
2. Localice el indicador **PA Temp** en la parte superior del applet.
3. Inicie su transmisión. Observe la barra **PA Temp** a medida que avanza la transmisión.
4. Si la barra entra en la zona amarilla (por encima de 55 °C), considere acortar sus transmisiones. Si alcanza la zona roja (por encima de 70 °C), finalice la transmisión y permita que la radio se enfríe.

## Qué hace cada control

| Control | Qué muestra | Rango | Umbral de zona roja |
|---|---|---|---|
| PA Temp | Temperatura del amplificador de potencia según el medidor PATEMP de la radio | 0–120 °C | por encima de 70 °C |
| +13.8V | Tensión de alimentación de corriente continua | 10.0–16.0 V | por encima de 15 V |
| Main Fan | Velocidad del ventilador de refrigeración | 0–3000 rpm | por encima de 2500 rpm |

La barra se llena de cian a amarillo (por encima de 55 °C) y luego a rojo (por encima de 70 °C). El indicador se actualiza de forma continua mientras la radio está conectada; no se necesita actualización manual.

## Consejos

- Durante una transmisión prolongada, observe **Main Fan** junto con **PA Temp**. Una lectura del ventilador muy por debajo de la zona roja (2500 rpm) mientras la temperatura sube puede indicar que el flujo de aire alrededor de la radio está restringido.
- El indicador utiliza una respuesta suavizada, por lo que la barra se anima gradualmente hacia la lectura actual en lugar de saltar. Los picos térmicos breves pueden aparecer ligeramente atenuados.

## Solución de problemas

- **El indicador PA Temp no muestra movimiento tras transmitir** — Confirme que la conexión con la radio está activa. El applet Meters requiere una conexión en vivo para recibir telemetría; si la radio está desconectada, todos los indicadores permanecerán estáticos.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Supervisar la velocidad del ventilador principal de refrigeración](monitor-the-main-cooling-fan-speed.md)
- [Verificar la tensión de alimentación de corriente continua de la radio](check-the-radio-s-dc-supply-voltage.md)
