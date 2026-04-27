# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para corregir la referencia de frecuencia de su FLEX-8600 mediante los controles de calibración GPSDO integrados. Una calibración de frecuencia precisa reduce el error de dial en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña RX en Radio Setup solo está disponible cuando hay una conexión de radio activa.
- El radio debe tener un GPSDO instalado y bloqueado antes de que los resultados de calibración sean significativos.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia de precisión conocida.
4. Haga clic en **Start** para iniciar el barrido de calibración.
5. Cuando el barrido se complete, revise el desplazamiento medido que se muestra en **Freq Offset (ppb):**.
6. Si prefiere establecer el desplazamiento manualmente en lugar de usar el resultado del barrido, edite **Freq Offset (ppb):** directamente.

## Qué hace cada control

| Control | Tipo | Descripción |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | La frecuencia de referencia utilizada durante el barrido de calibración. Configúrela en una señal de precisión conocida — por ejemplo, una emisora de frecuencia estándar de radiodifusión. |
| **Start** | Botón | Inicia el barrido de calibración en la frecuencia ingresada en **Cal Frequency (MHz):**. |
| **Freq Offset (ppb):** | Spinbox | El desplazamiento de frecuencia aplicado al oscilador de referencia del radio, en partes por mil millones. Puede ser establecido por el barrido o ingresado manualmente. |
| **10 MHz Reference Source:** | Combo box | Selecciona si el radio usa su referencia de 10 MHz **Internal** o una **External**. Valores válidos: `Internal` \| `External`. |

## Consejos

- Si tiene previsto usar una referencia externa de 10 MHz en lugar del GPSDO, configure **10 MHz Reference Source:** en `External` antes de calibrar, de modo que el desplazamiento se aplique a la fuente correcta.

## Relacionado

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
