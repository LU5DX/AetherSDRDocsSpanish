# Recuperar TGXL TUNE en el firmware 4.2 configurando una conexión directa

El firmware 4.2 de FlexRadio eliminó la ruta de comandos `tgxl autotune` del lado de la radio. Configurar una conexión TCP directa desde AetherSDR al TGXL restaura el botón TUNE enviando el comando de autoajuste directamente al TGXL en lugar de enrutarlo a través de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- Su TGXL debe estar encendido y accesible en la red desde la máquina que ejecuta AetherSDR.
- Conozca la dirección IP del TGXL. Si la radio ya ha descubierto el TGXL, AetherSDR la completará automáticamente.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el cuadro de diálogo Radio Setup.
2. Haga clic en la pestaña `Peripherals`.
3. Localice la fila del TGXL. Si el campo de dirección IP está vacío, ingrese la dirección IP del TGXL. El puerto predeterminado es `9010`; déjelo sin cambios a menos que su red requiera un puerto diferente.
4. Haga clic en `Connect` en la fila del TGXL.
5. Verifique que el botón cambie a `Disconnect`, lo que indica que la conexión TCP directa está activa.
6. Cierre el cuadro de diálogo. El botón TUNE ahora envía el comando de autoajuste directamente al TGXL.

AetherSDR guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectarse exitosamente y se reconectará automáticamente en el próximo inicio.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Campo de dirección IP (TGXL) | Dirección IP del TGXL en su red. Se completa automáticamente con la dirección descubierta por la radio si está disponible. | — | `TGXL_ManualIp` |
| Campo de puerto (TGXL) | Puerto TCP para la conexión directa al TGXL. | `9010` | `TGXL_ManualPort` |
| `Connect` / `Disconnect` (TGXL) | Abre o cierra la conexión TCP directa al TGXL. Cuando está conectado, TUNE envía el comando de autoajuste directamente al TGXL. | Connect | — |

## Consejos

- El TGXL activa el PTT de la radio a través de su cable de interbloqueo de hardware. No se necesita configuración adicional de PTT en AetherSDR para que la sintonía funcione una vez que la conexión directa está activa.
- Si la radio ya descubrió el TGXL en la LAN, el campo de dirección IP se completa automáticamente. Solo necesita hacer clic en `Connect`.
- Los valores guardados de `TGXL_ManualIp` y `TGXL_ManualPort` persisten entre reinicios, por lo que solo necesita realizar esta configuración una vez.

## Visualización de la fuente de referencia de 10 MHz (v0.9.7)

El cuadro combinado `10 MHz Reference Source:` en la pestaña `RX` se actualizó en la v0.9.7. La lista de fuentes disponibles y la etiqueta de estado de bloqueo a su lado ahora se comportan de manera diferente a versiones anteriores.

### Cuadro combinado de fuente

El cuadro combinado ahora se completa dinámicamente según el hardware presente en la radio conectada y la configuración y el estado actual del oscilador reportados por la radio. Pueden aparecer las siguientes fuentes:

| Entrada | Cuándo se muestra |
|---|---|
| Auto | Siempre se muestra. |
| TCXO | Se muestra cuando la radio reporta que hay un TCXO presente, o cuando el estado actual o reportado hace referencia a TCXO. |
| GPSDO | Se muestra cuando la radio reporta que hay un GPSDO presente, o cuando el estado actual o reportado hace referencia a GPSDO. |
| External 10 MHz | Se muestra cuando la radio reporta que hay una referencia externa presente o activa, o cuando el estado actual o reportado hace referencia a externa. Nota: la etiqueta cambió de "External" a "External 10 MHz" en la v0.9.7. |

El cuadro combinado selecciona automáticamente la configuración de oscilador guardada cuando se abre el cuadro de diálogo. Si la configuración guardada no está en la lista, se intenta el estado reportado actual; si este también está ausente, se selecciona Auto.

### Etiqueta de estado de bloqueo

La etiqueta de estado junto al cuadro combinado se actualizó para mostrar información más detallada:

- Cuando está seleccionado Auto y la radio ha cambiado a una fuente específica, la etiqueta muestra **Auto -> \<fuente\>** seguido de **Locked** o **Unlocked**.
- Cuando la fuente solicitada difiere de la fuente activa, la etiqueta muestra **\<solicitada\> -> \<activa\>** seguido de **Locked** o **Unlocked**.
- Cuando la fuente solicitada y la activa coinciden, la etiqueta muestra **\<fuente\> Locked** o **\<fuente\> Unlocked**.
- Cuando se selecciona External 10 MHz pero no se detecta ninguna referencia externa, la etiqueta agrega **(not detected)**.
- Mientras se espera que la radio reporte el estado del oscilador, la etiqueta muestra **Waiting for oscillator status**.

El color de la etiqueta es verde cuando está bloqueada y rojo cuando está desbloqueada. Antes de que la radio reporte cualquier estado del oscilador, la etiqueta se muestra en un gris neutro.

## Solución de problemas

- **El botón `Connect` no cambia a `Disconnect`** — El TGXL no es accesible en la IP y puerto ingresados. Confirme que el TGXL esté encendido, verifique que el puerto `9010` no esté bloqueado por un cortafuegos y confirme que la dirección IP sea correcta.
- **TUNE aún no funciona después de conectarse** — Confirme que la etiqueta `Disconnect` se muestre en la fila del TGXL, lo que confirma que la conexión directa está activa. Si el botón volvió a `Connect`, la conexión se perdió; verifique la estabilidad de la red y reconéctese.
- **El campo de dirección IP está vacío y la radio no ha descubierto el TGXL** — Ingrese la dirección IP del TGXL manualmente. Puede encontrarla en la tabla DHCP de su enrutador o en el panel frontal del TGXL.
- **El cuadro combinado de fuente de referencia de 10 MHz muestra solo Auto** — La radio aún no ha reportado el estado del hardware del oscilador. Espere un momento para que la conexión se inicialice completamente, luego vuelva a abrir el cuadro de diálogo. Si una fuente conocida como GPSDO no aparece, confirme que el hardware esté correctamente instalado y que el firmware de la radio sea 4.2 o posterior.
- **El estado de bloqueo muestra "Waiting for oscillator status"** — La radio aún no ha enviado el estado del oscilador. Esto se soluciona automáticamente una vez que la radio responda; no se requiere ninguna acción.

## Relacionados

- [Connect TGXL, PGXL or Antenna Genius by IP](connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Fix TUNE not working after upgrading to firmware 4.2 (configure direct TGXL connection)](fix-tune-not-working-after-upgrading-to-firmware-4-2-configure-direct-tgxl-connection.md)
- [Set per-band TX max power and tune mode](../../features/radio-setup/set-per-band-tx-max-power-and-tune-mode.md)
- [Radio Setup overview](../../features/radio-setup/overview.md)
