# Descripción general de los medidores

El applet de medidores muestra telemetría de hardware en tiempo real de su radio Flex: temperatura del amplificador de potencia (PA), tensión de alimentación de CC y velocidad del ventilador principal. Úselo para supervisar el estado del equipo durante la operación sin salir de la ventana principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet de medidores requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si no lo está, actívelo con `View > Applet Panel`.

## Cómo funciona

El applet de medidores está oculto de forma predeterminada. Haga clic en el botón MTR de la barra lateral derecha para mostrarlo u ocultarlo.

Una vez abierto, el applet muestra un encabezado de sección "Radio Hardware" sobre tres barras indicadoras horizontales. Cada barra se actualiza continuamente desde el flujo de medidores del equipo. La barra se llena de izquierda a derecha; las zonas de color indican condiciones normales (verde), de precaución (amarillo) y fuera de rango (rojo). La etiqueta del medidor aparece centrada en la barra y las marcas de escala se muestran a lo largo del borde superior.

Las lecturas de temperatura del PA y tensión de alimentación provienen directamente del flujo de telemetría de hardware del equipo. La velocidad del ventilador principal se resuelve a partir de la lista de medidores del equipo en la primera actualización; puede haber un breve retraso antes de que el medidor del ventilador muestre una lectura tras la conexión.

La corriente del PA no se muestra. El hardware de la serie FLEX-8000 limita ese medidor a 10 A, lo que provoca que la lectura se sature bajo plena potencia del PA, haciéndola poco confiable.

## Qué hace cada control

| Medidor | Qué mide | Rango | Rojo por encima de |
|---|---|---|---|
| PA Temp | Temperatura del amplificador de potencia | 0–120 °C | 70 °C |
| +13.8V | Tensión de alimentación de CC | 10.0–16.0 V | 15 V |
| Main Fan | Velocidad del ventilador principal | 0–3000 rpm | 2500 rpm |

Ninguno de estos controles tiene ajustes persistentes. Son pantallas de solo lectura; no se puede ajustar ningún valor desde este applet.

## Consejos

- Los medidores utilizan una respuesta suavizada, por lo que las fluctuaciones rápidas se promedian visualmente. Un transitorio breve puede no alcanzar la zona roja aunque la lectura instantánea sí lo haga.
- Si el medidor Main Fan marca cero inmediatamente después de conectar, espere un momento. El índice del medidor del ventilador se resuelve de forma diferida en la primera actualización del equipo.

## Relacionados

- [Supervisar la temperatura del PA durante transmisiones prolongadas](watch-pa-temperature-during-long-overs.md)
- [Verificar la tensión de alimentación de CC del equipo](check-the-radio-s-dc-supply-voltage.md)
- [Monitorear la velocidad del ventilador principal](monitor-the-main-cooling-fan-speed.md)
