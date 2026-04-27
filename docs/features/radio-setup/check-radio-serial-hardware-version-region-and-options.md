# Verificar el número de serie, versión de hardware, región y opciones del radio

La pestaña **Radio** en Radio Setup muestra información de identificación reportada directamente por el radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Utilice esta página para verificar el hardware y las opciones disponibles en su radio antes de realizar diagnósticos o contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los campos de la pestaña **Radio** se llenan con datos en vivo provenientes del radio.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por el radio.
   - **Region** — la región regulatoria del radio (muestra `USA` si el radio no reporta ninguna).
   - **Options** — las opciones licenciadas activas en este radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis según lo reportado por el radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware con prefijo `v`. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si el radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones licenciadas del radio. |

Los cuatro campos son de solo lectura. No tienen claves de configuración persistente asociadas.

## Consejos

- Si **Radio SN** está en blanco, el radio aún no ha enviado su número de serie del chasis. Desconéctese y vuelva a conectarse al radio.
- **Options** refleja lo que el propio radio reporta. Si adquirió recientemente una actualización de licencia, apague y encienda el radio, luego vuelva a conectarse para que obtenga las opciones actualizadas.

## Temas relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar el apodo, indicativo y nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Subir un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
