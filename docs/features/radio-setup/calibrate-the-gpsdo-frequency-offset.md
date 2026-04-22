# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para corregir cualquier error de frecuencia en el oscilador interno del FLEX-8600 aplicando un desplazamiento medido en partes por mil millones (ppb), o ejecutando un barrido de calibración automático contra una frecuencia de referencia conocida.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de la pestaña RX solo están activos con una conexión de radio activa.
- Tenga disponible una referencia de frecuencia conocida y precisa si desea usar el barrido de calibración — por ejemplo, una portadora de WWV, una baliza disciplinada por GPS, o un generador de señales calibrado.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Para ejecutar un barrido automático: ingrese la frecuencia de referencia en MHz en el spinbox **Cal Frequency (MHz):** y luego haga clic en **Start**. El radio realiza un barrido alrededor de esa frecuencia y calcula el desplazamiento.
4. Para establecer el desplazamiento manualmente: ingrese la corrección deseada directamente en el spinbox **Freq Offset (ppb):**. Los valores positivos desplazan la frecuencia indicada hacia arriba; los valores negativos la desplazan hacia abajo.
5. Cierre el diálogo. El desplazamiento se aplica de inmediato al radio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Rango |
|---|---|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | Frecuencia utilizada como referencia para el barrido de calibración automático. | — | — |
| **Start** | Botón | Inicia el barrido de calibración de frecuencia usando el valor en **Cal Frequency (MHz):**. | — | — |
| **Freq Offset (ppb):** | Spinbox | Corrección de frecuencia manual aplicada al oscilador, en partes por mil millones. | — | — |
| **10 MHz Reference Source:** | Lista desplegable | Selecciona si el radio se sincroniza con su oscilador interno o con una entrada de referencia externa de 10 MHz. | — | Internal \| External |

## Consejos

- Si tiene una fuente de 10 MHz disciplinada por GPS conectada a la entrada de referencia del panel trasero, cambie **10 MHz Reference Source:** a External en lugar de aplicar un desplazamiento manual. Consulte [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md).
- Ejecute el barrido de calibración en una frecuencia donde los efectos de propagación sean despreciables — una referencia local es más confiable que un estándar de onda corta distante.

## Solución de problemas

- **El botón Start no tiene efecto** — Confirme que AetherSDR está conectado al radio. Los controles de la pestaña RX requieren una conexión de radio activa.
- **El valor de Freq Offset (ppb): se restablece después de reconectar** — El desplazamiento se almacena en el radio, no en la configuración local de AetherSDR. Si el radio pierde alimentación antes de guardar su estado, el valor puede revertir a la última configuración de radio guardada.

## Relacionados

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
