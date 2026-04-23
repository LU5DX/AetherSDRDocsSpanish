# Consultar el número de serie, versión de hardware, región y opciones del radio

Consulte los detalles de hardware de solo lectura reportados por su radio Flex conectado: número de serie del chasis, cadena de versión de hardware, región regulatoria y opciones con licencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Estos campos se completan a partir de la conexión activa con el radio y permanecen en blanco en caso contrario.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio** (se abre de forma predeterminada).
3. Localice el grupo **Radio Information** cerca de la parte superior de la pestaña.
4. Lea los valores que se muestran para **Radio SN**, **HW Version**, **Region** y **Options**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador (solo lectura) | Número de serie del chasis reportado por el radio. |
| **HW Version** | Indicador (solo lectura) | Cadena de versión de hardware reportada por el radio. |
| **Region** | Indicador (solo lectura) | Región regulatoria programada en el radio. Muestra `USA` si el radio no reporta ninguna región. |
| **Options** | Indicador (solo lectura) | Opciones con licencia activas en este radio (por ejemplo, `GPS`, `GPS, PGXL`). |

## Consejos

- Los cuatro campos son de solo lectura. No hay controles para modificarlos desde AetherSDR; reflejan lo que reporta el firmware del radio.
- Si **Radio SN** aparece en blanco, es posible que la conexión con el radio aún no se haya establecido completamente. Cierre y vuelva a abrir el diálogo una vez que la conexión se estabilice.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Establecer el apodo del radio, indicativo y nombre de la estación](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr en el radio](upload-a-new-firmware-ssdr-to-the-radio.md)
