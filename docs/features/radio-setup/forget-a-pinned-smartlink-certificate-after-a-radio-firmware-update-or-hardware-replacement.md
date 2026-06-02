# Olvidar un certificado SmartLink fijado tras una actualización de firmware o reemplazo de hardware

Cuando actualiza el firmware de su radio o reemplaza el hardware, la huella digital del certificado TLS de SmartLink cambia. La fijación de primera confianza de AetherSDR rechazará la conexión porque la huella almacenada ya no coincide. Use la pestaña **SmartLink** en **Radio Setup** para olvidar el certificado anterior, de modo que la próxima conexión fije silenciosamente el nuevo.

## Antes de comenzar

- La radio debe estar conectada a AetherSDR.
- Necesita el nombre de host de la radio cuyo certificado fijado desea eliminar. La tabla en la pestaña **SmartLink** muestra todos los hosts fijados.

## Pasos

1. Abra **Settings > Radio Setup...**.
2. Haga clic en la pestaña **SmartLink**.
3. En la tabla **Pinned SmartLink Certificates**, haga clic en la fila del host cuyo certificado cambió.
4. Haga clic en **Forget selected**.
5. Cierre el diálogo de configuración de la radio y reconéctese a la radio. El nuevo certificado se fija automáticamente.

## Acerca de la tabla de certificados SmartLink fijados

La tabla enumera todos los hosts que se han fijado en la primera conexión (confianza en el primer uso). Contiene tres columnas:

- **Host**: El nombre de host de la radio.
- **SHA-256 fingerprint**: La huella digital del certificado, mostrada en monoespaciado.
- **Pinned**: La fecha en que se fijó el certificado por primera vez (formato YYYY-MM-DD) o "(pre-phase 2)" si se fijó antes de que se introdujera la función.

El botón **Forget selected** elimina la huella digital del certificado fijado del host seleccionado. La próxima conexión a ese host fija silenciosamente el nuevo certificado.

El botón **Forget all** borra todos los certificados fijados tras un mensaje de confirmación. La próxima conexión a cada radio los fija silenciosamente.

## Relacionado

- [Clear all pinned SmartLink certificates when rotating multiple radio TLS identities](clear-all-pinned-smartlink-certificates-when-rotating-multiple-radio-tls-identities.md)
- [Radio Setup dialog reference](radio-setup-dialog-reference.md)
