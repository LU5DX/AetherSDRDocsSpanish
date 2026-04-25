# Cambiar a una referencia externa de 10 MHz

Esta página explica cómo configurar el FLEX-8600 para bloquear su oscilador interno a una señal de referencia externa de 10 MHz en lugar de la referencia incorporada. Utilice esta opción cuando tenga un oscilador disciplinado por GPS, un patrón de rubidio u otra fuente de precisión de 10 MHz conectada al puerto REF IN del panel trasero del equipo.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El diálogo Radio Setup no está disponible sin conexión.
- La referencia externa de 10 MHz debe estar conectada al conector REF IN del panel trasero del equipo y debe estar activa antes de cambiar la fuente.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Localice el cuadro combinado **10 MHz Reference Source:**.
4. Seleccione **External**.

El equipo cambia el bloqueo de referencia de inmediato. No es necesario cerrar el diálogo ni hacer clic en Apply.

Para volver al oscilador incorporado, regrese al mismo cuadro combinado y seleccione **Internal**.

## Qué hace cada control

| Control | Tipo | Valores válidos | Comportamiento |
|---|---|---|---|
| **10 MHz Reference Source:** | Cuadro combinado | `Internal` \| `External` | Selecciona si el reloj del ADC del equipo se deriva del oscilador interno o de una señal externa de 10 MHz presente en el conector REF IN. |

## Sugerencias

- Mientras se encuentra en la pestaña **RX**, los controles **Cal Frequency (MHz):** y **Freq Offset (ppb):** también están disponibles. Si su referencia externa tiene un desplazamiento conocido, puede ingresarlo en **Freq Offset (ppb):** en lugar de ejecutar nuevamente un barrido de calibración completo.

## Solución de problemas

- **El equipo no muestra bloqueo o presenta deriva de frecuencia tras cambiar a External** — Confirme que la señal de referencia esté presente en el puerto REF IN antes de realizar el cambio. Si la fuente externa no está presente o está por debajo del nivel requerido, el equipo puede operar en modo libre o comportarse de forma errática. Vuelva a **Internal** y verifique la fuente de referencia y el cableado.

## Temas relacionados

- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Descripción general de Radio Setup](overview.md)
