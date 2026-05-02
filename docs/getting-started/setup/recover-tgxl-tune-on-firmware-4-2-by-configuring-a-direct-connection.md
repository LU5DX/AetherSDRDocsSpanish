# Recuperar TGXL TUNE en firmware 4.2 configurando una conexión directa

El firmware 4.2 de FlexRadio interrumpió la ruta del comando `tgxl autotune` en el lado del radio. Configurar una conexión TCP directa desde AetherSDR al TGXL restaura el botón TUNE enviando el comando de sintonía automática directamente al TGXL, en lugar de enrutarlo a través del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- Su TGXL debe estar encendido y accesible en la red desde la máquina que ejecuta AetherSDR.
- Conozca la dirección IP del TGXL. Si el radio ya descubrió el TGXL, AetherSDR la completará automáticamente.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `Peripherals`.
3. Localice la fila del TGXL. Si el campo de dirección IP está vacío, ingrese la dirección IP del TGXL. El puerto predeterminado es `9010`; déjelo sin cambios a menos que su red requiera un puerto diferente.
4. Haga clic en `Connect` en la fila del TGXL.
5. Verifique que el botón cambie a `Disconnect`, lo que indica que la conexión TCP directa está activa.
6. Cierre el diálogo. El botón TUNE ahora envía el comando de sintonía automática directamente al TGXL.

AetherSDR guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al realizar una conexión exitosa, y se volverá a conectar automáticamente en el siguiente inicio.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Campo de dirección IP (TGXL) | Dirección IP del TGXL en su red. Se completa automáticamente con la dirección detectada por el radio, si está disponible. | — | `TGXL_ManualIp` |
| Campo de puerto (TGXL) | Puerto TCP para la conexión directa al TGXL. | `9010` | `TGXL_ManualPort` |
| `Connect` / `Disconnect` (TGXL) | Abre o cierra la conexión TCP directa al TGXL. Cuando está conectado, TUNE envía el comando de sintonía automática directamente al TGXL. | Connect | — |

## Consejos

- El TGXL controla el PTT del radio a través de su cable de interbloqueo de hardware. No se necesita ninguna configuración adicional de PTT en AetherSDR para que la sintonía funcione una vez que la conexión directa está activa.
- Si el radio ya descubrió el TGXL en la LAN, el campo de dirección IP se completa automáticamente. Solo necesita hacer clic en `Connect`.
- Los valores guardados de `TGXL_ManualIp` y `TGXL_ManualPort` persisten entre reinicios, por lo que solo necesita realizar esta configuración una vez.

## Solución de problemas

- **El botón `Connect` no cambia a `Disconnect`** — El TGXL no es accesible en la IP y el puerto ingresados. Confirme que el TGXL está encendido, verifique que el puerto `9010` no esté bloqueado por un firewall y compruebe que la dirección IP sea correcta.
- **TUNE sigue sin funcionar después de conectar** — Confirme que la etiqueta `Disconnect` se muestra en la fila del TGXL, lo que confirma que la conexión directa está activa. Si el botón volvió a `Connect`, la conexión se interrumpió; verifique la estabilidad de la red y vuelva a conectar.
- **El campo de dirección IP está vacío y el radio no ha descubierto el TGXL** — Ingrese la dirección IP del TGXL manualmente. Puede encontrarla en la tabla DHCP de su router o en el panel frontal del TGXL.

## Relacionados

- [Conectar TGXL, PGXL o Antenna Genius por IP](connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Solucionar TUNE que no funciona tras actualizar al firmware 4.2 (configurar conexión directa al TGXL)](fix-tune-not-working-after-upgrading-to-firmware-4-2-configure-direct-tgxl-connection.md)
- [Configurar la potencia TX máxima por banda y el modo de sintonía](../../features/radio-setup/set-per-band-tx-max-power-and-tune-mode.md)
- [Descripción general de Radio Setup](../../features/radio-setup/overview.md)
