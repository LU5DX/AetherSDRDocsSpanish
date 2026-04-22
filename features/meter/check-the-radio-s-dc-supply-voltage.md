# Verificar el voltaje de alimentación CC del radio

El applet Meters incluye un medidor de voltaje de alimentación en tiempo real que muestra el voltaje que recibe el radio desde su fuente de alimentación CC. Úselo para confirmar que su fuente de alimentación entrega un voltaje adecuado antes y durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Meters requiere una conexión activa con el radio.
- El panel de applets debe estar visible. Si está oculto, use `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el botón de bandeja `MTR` en la barra lateral derecha del panel de applets.
2. Haga clic en `MTR` para abrir el applet Meters.
3. Lea el medidor `+13.8V` bajo el encabezado de sección **Radio Hardware**.

La barra se llena de izquierda a derecha. El color de relleno es verde en el rango de operación normal, cambia a amarillo a medida que el voltaje sube hacia la zona de advertencia, y se torna rojo por encima de 15.0 V.

## Qué hace cada control

| Control | Descripción | Rango válido | Umbral rojo |
|---|---|---|---|
| `+13.8V` | Voltaje de alimentación CC en tiempo real desde la entrada de energía del radio | 10.0–16.0 V | > 15.0 V |

Ninguna clave de configuración está asociada a este medidor. El valor se lee directamente del radio y no se almacena.

## Consejos

- Una lectura consistentemente inferior a 13.0 V bajo carga de transmisión sugiere que la fuente de alimentación o el cableado no pueden sostener el consumo de corriente del radio. Verifique la corriente nominal de su fuente y el calibre del cable.
- El medidor utiliza balística suavizada, por lo que las caídas de voltaje breves y repentinas pueden aparecer levemente atenuadas en la pantalla.

## Solución de problemas

- **El medidor `+13.8V` no muestra movimiento o indica 0 V** — Es posible que el radio aún no haya enviado telemetría. Verifique que la conexión con el radio esté activa. El medidor se actualiza únicamente cuando el radio envía datos de telemetría de hardware.
- **El panel de applets no aparece** — Haga clic en `View > Applet Panel` para restaurarlo y luego haga clic en el botón de bandeja `MTR`.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Monitorear la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Monitorear la velocidad del ventilador principal](monitor-the-main-cooling-fan-speed.md)
