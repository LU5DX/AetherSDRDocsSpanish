# Vigilar la temperatura del PA durante transmisiones prolongadas

El applet Meters muestra un indicador en vivo de PA Temp obtenido directamente del radio. Úselo para controlar la temperatura del amplificador de potencia cuando opere en modos de alto ciclo de trabajo, como FT8, RTTY o transmisiones largas en CW.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Meters requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si está oculto, actívelo con `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja **MTR** en la barra lateral derecha del panel de applets.
2. Haga clic en **MTR** para abrir o cerrar el applet Meters.
3. Lea el indicador **PA Temp** bajo el encabezado de sección **Radio Hardware**.
4. Observe el color de la barra a medida que aumenta la temperatura: la barra es verde por debajo de 55 °C, amarilla entre 55 °C y 70 °C, y roja por encima de 70 °C.

## Qué hace cada control

| Control | Qué muestra | Rango válido | Umbral rojo |
|---|---|---|---|
| PA Temp | Temperatura del amplificador de potencia según el radio | 0–120 °C | Por encima de 70 °C |
| +13.8V | Tensión de alimentación CC | 10.0–16.0 V | Por encima de 15 V |
| Main Fan | Velocidad del ventilador principal de refrigeración | 0–3000 rpm | Por encima de 2500 rpm |

Ninguna clave de configuración está asociada a estos indicadores. Todos los valores son telemetría de solo lectura proveniente del radio.

## Consejos

- La barra del indicador se anima suavemente entre lecturas — un salto repentino al rojo es un evento real de hardware, no un fallo de visualización.
- Si PA Temp se acerca a 70 °C durante un concurso o una transmisión digital prolongada, reduzca el ciclo de trabajo o la potencia de emisión para permitir que el amplificador se enfríe.
- Revisar Main Fan junto con PA Temp puede ayudar a distinguir un problema de ventilación de uno de alta potencia.

## Solución de problemas

- **Todos los indicadores leen cero o no responden** — el applet requiere una conexión de radio activa. Confirme que el radio esté conectado mediante `Settings > Connect to Radio...` antes de usar el applet Meters.
- **El indicador PA Temp permanece en cero incluso al transmitir** — es posible que el radio aún no haya enviado una actualización de telemetría. Espere unos segundos después de activar la transmisión. Si continúa en cero, verifique su conexión de red con el radio.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Monitorear la velocidad del ventilador principal de refrigeración](monitor-the-main-cooling-fan-speed.md)
- [Verificar la tensión de alimentación CC del radio](check-the-radio-s-dc-supply-voltage.md)
