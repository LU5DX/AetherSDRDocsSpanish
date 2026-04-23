# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para ajustar la frecuencia del oscilador interno del radio Flex ingresando una frecuencia de calibración conocida y aplicando un desplazamiento en partes por mil millones (ppb). Una calibración de frecuencia precisa mejora la exactitud en recepción y la precisión de frecuencia en el aire.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña RX no es accesible sin una conexión activa al radio.
- Tenga disponible una señal de referencia de precisión conocida en una frecuencia específica, o conozca el desplazamiento que desea aplicar directamente.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. En **Cal Frequency (MHz):**, ingrese la frecuencia de su señal de referencia en MHz.
4. Haga clic en **Start** para iniciar el barrido de calibración.
5. Si prefiere establecer el desplazamiento manualmente sin ejecutar un barrido, ingrese el valor deseado directamente en **Freq Offset (ppb):**.

## Función de cada control

| Control | Descripción | Valor predeterminado | Rango válido |
|---|---|---|---|
| **Cal Frequency (MHz):** | La frecuencia utilizada como referencia durante el barrido de calibración. | — | — |
| **Start** | Inicia el barrido de calibración de frecuencia usando el valor indicado en **Cal Frequency (MHz):**. | — | — |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual aplicado al oscilador del receptor, en partes por mil millones. | — | — |
| **10 MHz Reference Source:** | Selecciona si el radio utiliza su oscilador interno o una señal de referencia externa de 10 MHz. | — | Internal \| External |

## Consejos

- Si dispone de una referencia externa estable de 10 MHz, cambiar **10 MHz Reference Source:** a External y conectar la señal a la entrada del panel trasero del radio puede proporcionar mejor estabilidad a largo plazo que la calibración por desplazamiento por sí sola.

## Temas relacionados

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
