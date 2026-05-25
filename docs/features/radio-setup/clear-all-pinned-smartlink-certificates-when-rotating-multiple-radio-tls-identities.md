# Borrar todos los certificados SmartLink anclados al rotar múltiples identidades TLS de radios

Elimina todos los certificados TLS de SmartLink de confianza que AetherSDR ha anclado en la primera conexión, permitiéndole volver a anclar certificados de forma segura después de rotar identidades de radios o reemplazar hardware de radio.

## Antes de empezar

- La radio debe estar conectada a AetherSDR.
- Desea reemplazar o rotar certificados TLS en múltiples radios y necesita borrar todos los anclajes de confianza en el primer uso almacenados.

## Pasos

1. Abra **Settings > Radio Setup...**
2. Haga clic en la pestaña **SmartLink**.
3. Haga clic en **Forget all**.
4. En el cuadro de diálogo de confirmación, haga clic en **Yes** para borrar todos los certificados anclados.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Sección **Pinned SmartLink Certificates** | Lista cada host que este cliente ha anclado en la primera conexión. Muestra el Host, la huella digital SHA-256 y la fecha de anclaje. | (no se persiste – administrado por `WanCertCache`) |
| **Forget selected** | Elimina el certificado anclado del host seleccionado. La siguiente conexión a ese host vuelve a anclarlo silenciosamente. | (ninguna) |
| **Forget all** | Borra todos los certificados anclados después de un mensaje de confirmación. La siguiente conexión a cada radio vuelve a anclarlos silenciosamente. | (ninguna) |

## Consejos

- Después de borrar todos los anclajes, la siguiente conexión SmartLink a cada radio confiará silenciosamente en el nuevo certificado y lo volverá a anclar.
- Use **Forget selected** para eliminar el anclaje de un solo host si solo está actualizando una radio.

## Relacionado

- [Olvidar un certificado SmartLink anclado después de una actualización de firmware de radio o reemplazo de hardware](forget-a-pinned-smartlink-certificate-after-a-radio-firmware-update-or-hardware-replacement.md)
