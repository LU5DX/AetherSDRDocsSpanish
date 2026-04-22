# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para ajustar la referencia de frecuencia de su FLEX-8600 estableciendo una frecuencia de calibración o introduciendo un desplazamiento manual en partes por billón. Una calibración de frecuencia precisa mejora la exactitud de recepción y transmisión en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña RX solo es accesible cuando hay una conexión de radio activa.
- Su radio debe tener un GPSDO instalado, o una señal de referencia externa precisa disponible para comparación.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Para ejecutar un barrido de calibración automático, establezca la frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**, luego haga clic en **Start**.
4. Para introducir un desplazamiento manualmente, escriba el valor deseado directamente en **Freq Offset (ppb):**.
5. Cierre el diálogo. El desplazamiento se aplica al radio de inmediato.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido |
|---|---|---|---|
| **Cal Frequency (MHz):** | La frecuencia utilizada como referencia durante un barrido de calibración. Establézcala en una señal conocida y precisa (por ejemplo, un estándar de tiempo o una baliza disciplinada por GPSDO). | — | — |
| **Start** | Inicia el barrido de calibración de frecuencia usando el valor en **Cal Frequency (MHz):**. | — | — |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual aplicado al oscilador de referencia del radio, en partes por billón. | — | — |
| **10 MHz Reference Source:** | Selecciona si el radio utiliza su oscilador interno o una entrada de referencia externa de 10 MHz. | — | Internal \| External |

## Consejos

- Si dispone de una referencia externa de 10 MHz de buena calidad, cambie **10 MHz Reference Source:** a External antes de calibrar para obtener la mejor precisión de base.
- El campo **Freq Offset (ppb):** permite realizar correcciones finas sin ejecutar un barrido completo; es útil cuando ya conoce el error aproximado a partir de una calibración anterior.

## Relacionado

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Verificar el número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
