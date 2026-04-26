# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para ajustar la calibración de la referencia de frecuencia en su FLEX-8600. Corregir el desplazamiento mejora la precisión de frecuencia en recepción y transmisión en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña RX no es accesible mientras está desconectado.
- Identifique una señal de referencia de precisión conocida para calibrar (por ejemplo, una portadora de WWV o un estándar disciplinado por GPS).

## Pasos

1. Vaya a `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. En **Cal Frequency (MHz):**, ingrese la frecuencia de su señal de referencia.
4. Haga clic en **Start** para iniciar el barrido de calibración.
5. Cuando el barrido finalice, revise el resultado. Si necesita aplicar una corrección manual, ingrese el valor deseado directamente en **Freq Offset (ppb):**.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido |
|---|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para el barrido de calibración. Establézcala en la frecuencia de su señal de referencia. | — | — |
| **Start** | Inicia el barrido de calibración de frecuencia contra la frecuencia de calibración ingresada. | — | — |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual aplicado al oscilador de referencia, en partes por mil millones. Ajuste este valor si la calibración automática no está disponible. | — | — |
| **10 MHz Reference Source:** | Selecciona si el radio utiliza su oscilador interno o una entrada externa de 10 MHz como referencia de frecuencia. | — | Internal \| External |

## Consejos

- Si tiene una referencia externa de 10 MHz conectada a la entrada del panel trasero del radio, cambie **10 MHz Reference Source:** a External antes de calibrar. Esto puede hacer innecesaria la corrección manual del desplazamiento.

## Relacionados

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
