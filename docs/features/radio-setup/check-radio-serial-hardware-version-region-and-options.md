# Verificar el número de serie, versión de hardware, región y opciones del radio

La pestaña **Radio** en Radio Setup muestra campos de identidad de hardware de solo lectura, reportados directamente por el radio: número de serie del chasis, versión de hardware, región regulatoria y opciones licenciadas. Consulte esta página cuando necesite confirmar qué hardware tiene conectado o verificar qué opciones están activas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Estos campos son completados por el radio en el momento de la conexión y son de solo lectura.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio** si no está ya seleccionada.
3. En el grupo **Radio Information**, lea los siguientes campos:
   - **Radio SN** — número de serie del chasis.
   - **HW Version** — cadena de versión de hardware reportada por el radio.
   - **Region** — región regulatoria (por defecto `USA` si el radio no reporta ninguna).
   - **Options** — opciones licenciadas activas en este radio.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador | Número de serie del chasis. Solo lectura; asignado por el radio. |
| HW Version | Indicador | Cadena de versión de hardware. Solo lectura; asignada por el radio. |
| Region | Indicador | Región regulatoria. Por defecto `USA` si el radio reporta un valor vacío. |
| Options | Indicador | Opciones licenciadas activas en este radio (por ejemplo, GPS, PGXL). Solo lectura; asignadas por el radio. |

## Solución de problemas

- **Todos los campos aparecen en blanco o con guiones** — el radio aún no ha reportado su identidad. Confirme que el radio esté completamente conectado y en línea, luego cierre y vuelva a abrir `Settings > Radio Setup...`.
- **Region muestra `USA` pero el radio está configurado para una región diferente** — el firmware del radio reportó una cadena de región vacía; AetherSDR sustituye `USA` como valor de visualización predeterminado. Verifique el firmware del radio y la configuración de región en SmartSDR si el valor mostrado no es el esperado.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar el apodo, indicativo y nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
