# Cambio a una referencia externa de 10 MHz

Esta página explica cómo seleccionar un reloj de referencia externo de 10 MHz en su FLEX-8600. Utilice una referencia externa cuando necesite sincronizar el equipo con un oscilador disciplinado por GPS, un patrón de rubidio u otra fuente de frecuencia de precisión.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El diálogo Radio Setup no está disponible sin una conexión activa al equipo.
- Una señal estable de 10 MHz debe estar físicamente conectada a la entrada de referencia de 10 MHz del panel trasero del FLEX-8600 antes de cambiar la fuente.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Localice el cuadro combinado **10 MHz Reference Source:**.
4. Seleccione **External**.

El equipo cambia inmediatamente su entrada de oscilador de referencia. No se requiere ningún paso adicional de confirmación.

Para volver al oscilador interno, regrese a la pestaña **RX** y seleccione **Internal** en **10 MHz Reference Source:**.

## Qué hace cada control

| Control | Tipo | Valores válidos | Comportamiento |
|---|---|---|---|
| **10 MHz Reference Source:** | Cuadro combinado | Internal \| External | Selecciona si el equipo se sincroniza con su oscilador interno o con una señal presente en la entrada de 10 MHz del panel trasero. |

## Consejos

- Si también necesita corregir un error de frecuencia residual después de sincronizar con una referencia externa, utilice el control giratorio **Freq Offset (ppb):** en la misma pestaña **RX**.

## Solución de problemas

- **La frecuencia del equipo es inestable o se desvía tras seleccionar External** — Es posible que la señal externa de 10 MHz esté ausente, sea demasiado débil o esté fuera de especificación. Verifique que la señal esté presente y dentro de los requisitos de nivel de entrada del FLEX-8600; luego vuelva a **Internal** y reintente.
- **El cuadro combinado 10 MHz Reference Source: aparece atenuado o no está visible** — AetherSDR requiere una conexión activa al equipo para mostrar los controles de la pestaña **RX**. Confirme que el equipo esté conectado antes de abrir Radio Setup.

## Relacionado

- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
