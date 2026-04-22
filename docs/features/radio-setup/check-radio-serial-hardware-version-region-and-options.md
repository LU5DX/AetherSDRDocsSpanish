# Verificar el número de serie, versión de hardware, región y opciones del radio

Abra la pestaña **Radio** en Radio Setup para ver el número de serie del chasis, la versión de hardware, la región regulatoria y las opciones licenciadas de su FLEX-8600. Todos los campos de esta pestaña son indicadores de solo lectura — no es posible modificar ningún valor aquí.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Estos indicadores se completan a partir de la conexión activa con el radio.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Localice el grupo **Radio Information**.
4. Lea los valores de los siguientes indicadores:
   - **Radio SN** — número de serie del chasis.
   - **HW Version** — cadena de versión de hardware.
   - **Region** — región regulatoria (predeterminado: `USA`).
   - **Options** — opciones licenciadas activas en este radio.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador | Número de serie del chasis. Solo lectura. |
| HW Version | Indicador | Cadena de versión de hardware. Solo lectura. |
| Region | Indicador | Región regulatoria del radio. Predeterminado: `USA`. Solo lectura. |
| Options | Indicador | Lista las opciones licenciadas activas en el radio. Solo lectura. |
| Model | Indicador | Cadena del modelo del radio. Solo lectura. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl conectado. Solo lectura. |
| multiFLEX | Indicador | Estado de habilitación de multiFLEX. Solo lectura. |

## Consejos

- Si **Radio SN** aparece en blanco, es posible que el radio aún no haya reportado su número de serie del chasis. Desconéctese y vuelva a conectarse al radio, luego abra nuevamente Radio Setup.
- **Options** refleja lo que el firmware del radio reporta como licenciado. Si falta una opción esperada, verifique el estado de su licencia a través del portal de licencias de FlexRadio.

## Relacionado

- [Establecer el apodo, indicativo y nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr en el radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Descripción general de Radio Setup](overview.md)
