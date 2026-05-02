# Conectar TGXL, PGXL, Antenna Genius o ShackSwitch por IP

Use esta página para conectar manualmente un dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch a AetherSDR cuando el descubrimiento automático no haya detectado el dispositivo.

## Antes de comenzar

- AetherSDR debe estar ya conectado a una radio FLEX-8600. La pestaña Peripherals solo está disponible cuando hay una conexión de radio activa.
- Tenga a mano la dirección IP del dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila correspondiente al dispositivo que desea conectar (TGXL, PGXL, Antenna Genius o ShackSwitch).
4. Ingrese la dirección IP del dispositivo en el campo correspondiente.
5. Haga clic en **Connect** para ese dispositivo.

Para desconectar un dispositivo, haga clic en **Disconnect** en su fila.

## Pestaña Peripherals — filas de dispositivos

| Dispositivo | Puerto predeterminado | Notas |
|---|---|---|
| TGXL | 9010 | Necesario para recuperar TUNE con firmware 4.2+. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort`. Si el campo de IP está vacío y la radio ya descubrió el TGXL, la IP descubierta se completa automáticamente. |
| PGXL | 9008 | Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Antenna Genius (AG) | 9007 | Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado **Connected** solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. |
| ShackSwitch | 9007 | Utiliza el protocolo UDP/TCP de AG. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en el beacon de difusión de AG. El descubrimiento automático por UDP también funciona sin ingresar una IP manualmente. La fila se oculta del estado **Connected** si el dispositivo conectado es un Antenna Genius (no ShackSwitch). |

## Abrir la interfaz web del ShackSwitch

Cada fila de ShackSwitch incluye un botón **⚙ Web UI**. Al hacer clic, se abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema.

AetherSDR determina el puerto de la interfaz web de la siguiente manera:

1. Si el beacon del ShackSwitch conectado anuncia un `webPort` mayor que 1024, se utiliza ese puerto.
2. De lo contrario, se utiliza el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se utiliza el puerto 5000 como valor de respaldo.

El botón utiliza la dirección IP almacenada en `SS_ManualIp`. Si ese campo está vacío y hay un ShackSwitch conectado actualmente, se utiliza en su lugar la dirección del par activo. El botón no hace nada si no se puede determinar ninguna dirección IP.

## Relacionado

- [Descripción general de Radio Setup](../../features/radio-setup/overview.md)
- [Conectar manualmente un AG a través de una red remota](manually-connect-to-an-ag-over-a-remote-network.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)

---

# Radio Setup — Actualización de firmware (cambios en v0.9.3)

## Seleccionar un archivo de firmware

En v0.9.3, el botón **Browse .ssdr...** ha sido renombrado a **Select Installer...**. El botón ahora acepta tres tipos de archivo además del firmware ya extraído:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador SmartSDR WiX | `.msi` | FlexRadio v4.2 y posteriores |
| Instalador autoextraíble SmartSDR | `.exe` | Versiones anteriores de SmartSDR |
| Archivo de firmware extraído | `.ssdr` | Como en versiones anteriores de AetherSDR |

El preparador de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (encabezado OLE/MSI frente a encabezado PE/COFF MZ) y extrae el contenido `.ssdr` sin requerir herramientas externas.

### Para preparar firmware desde un instalador local

1. Descargue el instalador de SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo `.msi`, `.exe` o `.ssdr`.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para ver el avance y cualquier error.
7. Cuando la preparación esté completa, haga clic en **Upload Firmware** para enviar el firmware a la radio.

## Cambio de comportamiento en Check for Update

Cuando **Check for Update** encuentra una versión de firmware más reciente, AetherSDR ahora muestra un mensaje informativo en lugar de ofrecer una descarga dentro de la aplicación:

> Actualización disponible: v*X.Y.Z*  
> Descargue el instalador de SmartSDR desde flexradio.com  
> y luego haga clic en 'Select Installer...' para prepararlo.

Descargue el instalador desde flexradio.com de forma independiente y luego use **Select Installer...** como se describe arriba.
