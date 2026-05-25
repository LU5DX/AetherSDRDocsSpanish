# Olvidar un certificado SmartLink anclado tras una actualización de firmware o un reemplazo de hardware

Cuando actualiza el firmware de su radio o reemplaza el hardware de la misma, la huella digital del certificado TLS de SmartLink cambia. El anclaje de confianza en el primer uso de AetherSDR rechazará la conexión porque la huella digital almacenada ya no coincide. Use la pestaña SmartLink en Configuración de Radio para olvidar el certificado antiguo, de modo que la próxima conexión ancle el nuevo certificado de forma silenciosa.

## Antes de comenzar

- La radio debe estar conectada a AetherSDR.
- Necesita el nombre de host de la radio cuyo certificado anclado desea eliminar. La tabla en la pestaña SmartLink muestra todos los hosts anclados.

## Pasos

1. Abra **Settings > Radio Setup...**.
2. Haga clic en la pestaña **SmartLink**.
3. En la tabla **Pinned SmartLink Certificates**, haga clic en la fila del host cuyo certificado cambió.
4. Haga clic en **Forget selected**.
5. Cierre el diálogo de Configuración de Radio y reconéctese a la radio. El nuevo certificado se ancla automáticamente.

## Relacionado

- [Borrar todos los certificados SmartLink anclados al rotar múltiples identidades TLS de radio](clear-all-pinned-smartlink-certificates-when-rotating-multiple-radio-tls-identities.md)
