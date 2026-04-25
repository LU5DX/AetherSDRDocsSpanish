# Verificar el número de serie, versión de hardware, región y opciones del radio

Consulte los campos de identificación de solo lectura que reporta su FLEX-8600: número de serie del chasis, cadena de versión de hardware, región regulatoria y opciones licenciadas. Use esta página para confirmar la identidad del radio antes de enviar una solicitud de soporte o verificar una actualización de hardware.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Estos campos se completan a partir de una conexión activa con el radio.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**. Es la primera pestaña y se abre de forma predeterminada.
3. En el grupo **Radio Information**, lea los siguientes indicadores:
   - **Radio SN** — número de serie del chasis.
   - **HW Version** — cadena de versión de hardware.
   - **Region** — región regulatoria (predeterminado: `USA`).
   - **Options** — opciones licenciadas activas en este radio.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento | Predeterminado |
|---|---|---|---|
| Radio SN | Indicador | Número de serie del chasis. Solo lectura. | — |
| HW Version | Indicador | Cadena de versión de hardware. Solo lectura. | — |
| Region | Indicador | Región regulatoria del radio. Solo lectura. | USA |
| Options | Indicador | Opciones licenciadas activas en esta unidad. Solo lectura. | — |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. Solo lectura. | — |
| multiFLEX | Indicador | Estado de habilitación de multiFLEX. Solo lectura. | — |

## Consejos

- Los cuatro campos son de solo lectura. Nada en esta página modifica el hardware del radio ni el estado de la licencia.
- Si **Radio SN** aparece en blanco, el firmware del radio aún no ha reportado el número de serie del chasis. Desconecte y vuelva a conectar para activar una respuesta de estado actualizada.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Establecer el apodo, indicativo y nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr en el radio](upload-a-new-firmware-ssdr-to-the-radio.md)
