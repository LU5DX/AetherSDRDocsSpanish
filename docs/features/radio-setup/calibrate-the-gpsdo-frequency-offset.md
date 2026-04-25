# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para corregir errores de frecuencia en el oscilador del FLEX-8600 estableciendo un desplazamiento en partes por mil millones (ppb) o ejecutando un barrido de calibración automático. Una calibración de frecuencia precisa mejora la exactitud de recepción y transmisión en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **RX** solo es accesible con una conexión de radio activa.
- Se necesita una señal de referencia de frecuencia conocida y precisa para calibrar (por ejemplo, una portadora WWV o una señal disciplinada por GPSDO).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Para ejecutar un barrido de calibración automático:
   1. Ingrese la frecuencia de su señal de referencia en **Cal Frequency (MHz):**.
   2. Haga clic en **Start**. El radio realiza un barrido de calibración contra esa frecuencia.
4. Para establecer un desplazamiento manual en su lugar, ingrese el valor de corrección directamente en **Freq Offset (ppb):**.

## Función de cada control

| Control | Descripción | Valor predeterminado | Rango válido |
|---|---|---|---|
| **Cal Frequency (MHz):** | La frecuencia utilizada como referencia durante el barrido de calibración automático. | — | — |
| **Start** | Inicia el barrido de calibración de frecuencia usando el valor en **Cal Frequency (MHz):**. | — | — |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual aplicado al oscilador, en partes por mil millones. | — | — |
| **10 MHz Reference Source:** | Selecciona si el radio usa su oscilador interno o una entrada externa de 10 MHz como referencia de frecuencia. | — | Internal \| External |

## Consejos

- Si tiene una referencia externa estable de 10 MHz conectada a la entrada del panel trasero del radio, cambie **10 MHz Reference Source:** a External antes de calibrar. Esto hace que el ajuste de **Freq Offset (ppb):** sea innecesario en la mayoría de los casos.

## Temas relacionados

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
