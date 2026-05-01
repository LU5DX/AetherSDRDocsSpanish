# Conectar TGXL, PGXL, Antenna Genius o ShackSwitch por IP

Use esta página para conectar manualmente un dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch a AetherSDR cuando el descubrimiento automático no haya detectado el dispositivo.

## Antes de comenzar

- AetherSDR ya debe estar conectado a un radio FLEX-8600. La pestaña Peripherals solo está disponible cuando una conexión de radio está activa.
- Tenga lista la dirección IP del dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila del dispositivo que desea conectar (TGXL, PGXL, Antenna Genius o ShackSwitch).
4. Ingrese la dirección IP del dispositivo en el campo correspondiente.
5. Haga clic en **Connect** para ese dispositivo.

Para desconectar un dispositivo, haga clic en **Disconnect** en su fila.

## Pestaña Peripherals — filas de dispositivos

| Dispositivo | Puerto predeterminado | Notas |
|---|---|---|
| TGXL | 9010 | Requerido para recuperar TUNE en firmware 4.2+. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort`. Si el campo IP está vacío y el radio ya ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| PGXL | 9008 | Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Antenna Genius (AG) | 9007 | Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra estado **Connected** solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. |
| ShackSwitch | 9007 | Usa el protocolo AG UDP/TCP. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de transmisión AG. El autodescubrimiento por UDP también funciona sin ingresar manualmente una IP. La fila está oculta del estado **Connected** si un Antenna Genius (que no sea ShackSwitch) es el dispositivo conectado. |

## Abrir la interfaz web de ShackSwitch

Cada fila de ShackSwitch incluye un botón **⚙ Web UI**. Al hacer clic en él se abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema.

AetherSDR determina el puerto de la interfaz web de la siguiente manera:

1. Si la baliza ShackSwitch conectada anuncia un `webPort` mayor a 1024, se usa ese puerto.
2. Si no, se usa el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se usa el puerto 5000 como respaldo.

El botón usa la dirección IP almacenada en `SS_ManualIp`. Si ese campo está vacío y un ShackSwitch está actualmente conectado, se usa la dirección de peer en vivo en su lugar. El botón no hace nada si no se puede determinar ninguna dirección IP.

## Relacionado

- [Descripción general de Radio Setup](../../features/radio-setup/overview.md)
- [Conectar manualmente a un AG en una red remota](manually-connect-to-an-ag-over-a-remote-network.md)
- [Cambiar MTU de red para configuraciones VPN/remota](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)

---

# Radio Setup — Actualización de Firmware (cambios v0.9.3)

## Seleccionar un archivo de firmware

En v0.9.3, el botón **Browse .ssdr...** ha sido renombrado a **Select Installer...**. El botón ahora acepta tres tipos de archivo además del firmware previamente extraído:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador SmartSDR WiX | `.msi` | FlexRadio v4.2 y posterior |
| Instalador autoejecutable de SmartSDR | `.exe` | Versiones antiguas de SmartSDR |
| Archivo de firmware extraído | `.ssdr` | Como en versiones anteriores de AetherSDR |

El almacenador de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (magic OLE/MSI versus encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` sin requerir herramientas externas.

### Para preparar firmware de un instalador local

1. Descargue el instalador de SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo `.msi`, `.exe` o `.ssdr`.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para el progreso y cualquier error.
7. Cuando la preparación esté completa, haga clic en **Upload Firmware** para enviar el firmware al radio.

## Cambio de comportamiento de Check for Update

Cuando **Check for Update** encuentra una versión de firmware más nueva, AetherSDR ahora muestra un mensaje informativo en lugar de ofrecer una descarga en la aplicación:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com,  
> then click 'Select Installer...' to stage it.

Descargue el instalador de flexradio.com de forma independiente, luego use **Select Installer...** como se describe arriba.
