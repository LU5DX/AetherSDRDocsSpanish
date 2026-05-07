# Conectar TGXL, PGXL, Antenna Genius o ShackSwitch por IP

Use esta página para conectar manualmente un dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch a AetherSDR cuando la detección automática no haya identificado el dispositivo.

## Antes de comenzar

- AetherSDR ya debe estar conectado a una radio FLEX-8600. La pestaña Peripherals solo está disponible cuando hay una conexión activa con la radio.
- Tenga lista la dirección IP del dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch.

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
| TGXL | 9010 | Necesario para recuperar TUNE en firmware 4.2+. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort`. Si el campo IP está vacío y la radio ya ha detectado el TGXL, la IP detectada se rellena automáticamente. |
| PGXL | 9008 | Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Antenna Genius (AG) | 9007 | Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado **Connected** solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. |
| ShackSwitch | 9007 | Utiliza el protocolo UDP/TCP de AG. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en el baliza de difusión de AG. La detección automática por UDP también funciona sin ingresar una IP manualmente. La fila se oculta del estado **Connected** si un Antenna Genius (que no es ShackSwitch) es el dispositivo conectado. |

## Abrir la interfaz web de ShackSwitch

Cada fila de ShackSwitch incluye un botón **⚙ Web UI**. Al hacer clic, se abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema.

AetherSDR determina el puerto para la interfaz web de la siguiente manera:

1. Si la baliza del ShackSwitch conectado anuncia un `webPort` mayor que 1024, se utiliza ese puerto.
2. De lo contrario, se utiliza el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se utiliza el puerto 5000 como valor predeterminado.

El botón utiliza la dirección IP almacenada en `SS_ManualIp`. Si ese campo está vacío y hay un ShackSwitch actualmente conectado, se utiliza la dirección del par activo. El botón no hace nada si no se puede determinar ninguna dirección IP.

## Relacionado

- [Radio Setup overview](../../features/radio-setup/overview.md)
- [Manually connect to an AG over a remote network](manually-connect-to-an-ag-over-a-remote-network.md)
- [Change network MTU for VPN/remote setups](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)

---

# Radio Setup — Actualización de firmware (cambios en v0.9.3)

## Selección de un archivo de firmware

En v0.9.3, el botón **Browse .ssdr...** ha sido renombrado a **Select Installer...**. El botón ahora acepta tres tipos de archivo además del firmware preextraído:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador WiX de SmartSDR | `.msi` | FlexRadio v4.2 y posteriores |
| Instalador autoextraíble de SmartSDR | `.exe` | Versiones anteriores de SmartSDR |
| Archivo de firmware extraído | `.ssdr` | Como en versiones anteriores de AetherSDR |

El preparador de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (marca mágica OLE/MSI frente a cabecera PE/COFF MZ) y extrae la carga útil `.ssdr` sin necesidad de herramientas externas.

### Para preparar firmware desde un instalador local

1. Descargue el instalador de SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo `.msi`, `.exe` o `.ssdr`.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para ver el avance y posibles errores.
7. Cuando la preparación esté completa, haga clic en **Upload Firmware** para enviar el firmware a la radio.

## Cambio en el comportamiento de Check for Update

Cuando **Check for Update** encuentra una versión de firmware más reciente, AetherSDR ahora muestra un mensaje informativo en lugar de ofrecer una descarga directa:

> Actualización disponible: v*X.Y.Z*  
> Descargue el instalador de SmartSDR desde flexradio.com,  
> luego haga clic en 'Select Installer...' para prepararlo.

Descargue el instalador de flexradio.com de forma independiente y luego use **Select Installer...** como se describió anteriormente.

---

# Radio Setup — Pestaña RX: Fuente de referencia de 10 MHz (cambios en v0.9.7)

## Cuadro combinado de fuente de oscilador

El cuadro combinado **10 MHz Reference Source:** en la pestaña **RX** se ha actualizado en v0.9.7. La lista de fuentes disponibles ahora se construye dinámicamente en función del hardware presente y del estado del oscilador reportado por la radio, en lugar de ser fija al abrir el diálogo.

### Opciones disponibles

| Etiqueta | Valor interno | Cuándo se muestra |
|---|---|---|
| Auto | `auto` | Siempre visible |
| TCXO | `tcxo` | Se muestra cuando hay hardware TCXO presente, se ha recibido el estado del oscilador, o la configuración actual o guardada es `tcxo` |
| GPSDO | `gpsdo` | Se muestra cuando hay hardware GPSDO presente o la configuración actual o guardada es `gpsdo` |
| External 10 MHz | `external` | Se muestra cuando hay una referencia externa presente, se ha recibido el estado del oscilador, o la configuración actual o guardada es `external` |

Anteriormente, la opción de referencia externa aparecía en el cuadro combinado como **External**. Ahora aparece como **External 10 MHz**.

### Indicación del estado de bloqueo

La etiqueta de estado de bloqueo junto al cuadro combinado ahora muestra información más detallada que el texto plano `<STATE> Locked / Unlocked` utilizado anteriormente.

| Situación | Ejemplo de texto mostrado |
|---|---|
| Estado del oscilador aún no recibido | `Waiting for oscillator status` |
| El modo Auto ha resuelto una fuente | `Auto -> GPSDO Locked` |
| La configuración guardada difiere del estado activo | `TCXO -> GPSDO Locked` |
| La configuración y el estado coinciden | `GPSDO Locked` |
| External seleccionado pero referencia no detectada | `External 10 MHz Unlocked (not detected)` |

El color de la etiqueta se actualiza automáticamente: verde (`#00c040`) cuando está bloqueado, rojo (`#c04040`) cuando no está bloqueado y gris (`#8aa8c0`) mientras espera el estado.
