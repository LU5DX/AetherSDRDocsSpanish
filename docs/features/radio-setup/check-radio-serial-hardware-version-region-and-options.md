# Verificar el número de serie, versión de hardware, región y opciones del radio

Abra la pestaña **Radio** en Radio Setup para ver el número de serie del chasis de su FLEX-8600, la cadena de versión de hardware, la región regulatoria y las opciones con licencia. Estos son valores de solo lectura informados por el firmware del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los campos de la pestaña **Radio** aparecen en blanco hasta que se establezca una conexión.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — número de serie del chasis.
   - **HW Version** — cadena de versión de hardware informada por el radio.
   - **Region** — región regulatoria (se establece como `USA` de manera predeterminada si el radio no informa ninguna).
   - **Options** — opciones con licencia activas en este radio.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis según lo informado por el radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware. Se muestra con una `v` inicial. |
| Region | Indicador (solo lectura) | Región regulatoria. Valor predeterminado: `USA`. |
| Options | Indicador (solo lectura) | Cadena de opciones con licencia proveniente del firmware del radio. |
| FlexControl | Indicador (solo lectura) | Estado detectado del hardware FlexControl conectado. |
| multiFLEX | Indicador (solo lectura) | Estado de habilitación de multiFLEX. |

## Consejos

- Los cuatro valores se leen del radio en el momento de la conexión y no pueden modificarse desde este cuadro de diálogo.
- Los detalles de la licencia (nivel de suscripción, fecha de vencimiento, ID de radio y versión de firmware con licencia) se muestran en el grupo **License Info** de la misma pestaña.

## Relacionados

- [Establecer el apodo, indicativo y nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Descripción general de Radio Setup](overview.md)
