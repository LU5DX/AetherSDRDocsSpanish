# Conectar TGXL, PGXL o Antenna Genius por IP

Utilice esta página para conectar manualmente un dispositivo TGXL, PGXL o Antenna Genius a AetherSDR cuando el descubrimiento automático no haya detectado el dispositivo.

## Antes de comenzar

- AetherSDR ya debe estar conectado a una radio FLEX-8600. La pestaña Peripherals solo está disponible cuando hay una conexión de radio activa.
- Tenga lista la dirección IP del dispositivo TGXL, PGXL o Antenna Genius.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila del dispositivo que desea conectar (TGXL, PGXL o Antenna Genius).
4. Ingrese la dirección IP del dispositivo en el campo correspondiente.
5. Haga clic en **Connect** para ese dispositivo.

Para desconectar un dispositivo, haga clic en **Disconnect** en su fila.

## Relacionado

- [Descripción general de Radio Setup](../../features/radio-setup/overview.md)
- [Conectar manualmente a un AG a través de una red remota](manually-connect-to-an-ag-over-a-remote-network.md)
- [Cambiar MTU de red para configuraciones VPN/remotas](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)

---

# Radio Setup — Actualización de firmware (cambios en v0.9.3)

## Seleccionar un archivo de firmware

En v0.9.3 el botón **Browse .ssdr...** ha sido renombrado a **Select Installer...**. El botón ahora acepta tres tipos de archivo además del firmware extraído previamente:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador WiX de SmartSDR | `.msi` | FlexRadio v4.2 y posterior |
| Instalador autoejecutable de SmartSDR | `.exe` | Lanzamientos antiguos de SmartSDR |
| Archivo de firmware extraído | `.ssdr` | Como en versiones anteriores de AetherSDR |

El gestor de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (OLE/MSI magic versus encabezado MZ PE/COFF) y extrae la carga útil `.ssdr` sin requerir herramientas externas.

### Para preparar firmware desde un instalador local

1. Descargue el instalador de SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo `.msi`, `.exe` o `.ssdr`.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para ver el progreso y cualquier error.
7. Cuando la preparación se complete, haga clic en **Upload Firmware** para enviar el firmware a la radio.

## Cambio de comportamiento de Check for Update

Cuando **Check for Update** encuentra una versión de firmware más nueva, AetherSDR ahora muestra un mensaje informativo en lugar de ofrecer una descarga en la aplicación:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com,  
> then click 'Select Installer...' to stage it.

Descargue el instalador desde flexradio.com de forma independiente, luego utilice **Select Installer...** como se describe arriba.
