# Conectar TGXL, PGXL, Antenna Genius o ShackSwitch por IP

Use esta página para conectar manualmente un dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch a AetherSDR cuando el descubrimiento automático no lo ha detectado.

## Antes de comenzar

- AetherSDR ya debe estar conectado a una radio FLEX-8600. La pestaña Peripherals solo está disponible cuando hay una conexión activa con la radio.
- Tenga lista la dirección IP del dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila del dispositivo que desea conectar (TGXL, PGXL, Antenna Genius o ShackSwitch).
4. Ingrese la dirección IP del dispositivo en el campo correspondiente.
5. Haga clic en **Connect** para ese dispositivo.

Para desconectar un dispositivo, haga clic en **Disconnect** en su fila.

### Borrar una dirección IP guardada

Si previamente guardó una dirección IP manual para un periférico y desea eliminarla:

- Borre el campo de dirección IP y haga clic en **Connect** (mientras está desconectado). AetherSDR elimina los ajustes guardados `ManualIp` y `ManualPort` y ya no se conectará automáticamente al iniciar.
- Si borra el campo IP y cierra el diálogo Radio Setup (sin hacer clic en Connect ni Disconnect), AetherSDR trata el campo borrado de la misma manera: elimina los ajustes guardados y desconecta el dispositivo si estaba conectado.

## Pestaña Peripherals — filas de dispositivos

| Dispositivo | Puerto predeterminado | Notas |
|---|---|---|
| TGXL | 9010 | Necesario para recuperar TUNE en firmware 4.2+. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort`. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, se rellena automáticamente con la IP descubierta. |
| PGXL | 9008 | Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Antenna Genius (AG) | 9007 | Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado **Connected** solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. |
| ShackSwitch | 9007 | Usa el protocolo UDP/TCP de AG. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en el beacon de difusión de AG. El descubrimiento automático por UDP también funciona sin ingresar una IP manualmente. La fila se oculta del estado **Connected** si un Antenna Genius (que no es ShackSwitch) es el dispositivo conectado. |

## Abrir la interfaz web de ShackSwitch

Cada fila de ShackSwitch incluye un botón **⚙ Web UI**. Al hacer clic, se abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema.

AetherSDR determina el puerto para la interfaz web de la siguiente manera:

1. Si el beacon del ShackSwitch conectado anuncia un `webPort` mayor a 1024, se usa ese puerto.
2. De lo contrario, se usa el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se usa el puerto 5000 como valor de respaldo.

El botón usa la dirección IP almacenada en `SS_ManualIp`. Si ese campo está vacío y hay un ShackSwitch conectado actualmente, se usa la dirección del peer activo. El botón no hace nada si no se puede determinar ninguna dirección IP.

## Relacionado

- [Resumen de Radio Setup](../../features/radio-setup/overview.md)
- [Conectar manualmente a un AG a través de una red remota](manually-connect-to-an-ag-over-a-remote-network.md)
- [Cambiar MTU de red para configuraciones VPN/remotas](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)

---

# Radio Setup — Actualización de firmware (cambios v0.9.3)

## Seleccionar un archivo de firmware

En v0.9.3, el botón **Browse .ssdr...** ha sido renombrado a **Select Installer...**. El botón ahora acepta tres tipos de archivo además del firmware preextraído:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador WiX de SmartSDR | `.msi` | FlexRadio v4.2 y posteriores |
| Instalador autoextraíble de SmartSDR | `.exe` | Versiones anteriores de SmartSDR |
| Archivo de firmware extraído | `.ssdr` | Como en versiones anteriores de AetherSDR |

El preparador de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (marca OLE/MSI frente a cabecera PE/COFF MZ) y extrae la carga útil `.ssdr` sin necesidad de herramientas externas.

### Para preparar firmware desde un instalador local

1. Descargue el instalador de SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo `.msi`, `.exe` o `.ssdr`.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para ver el progreso y posibles errores.
7. Cuando la preparación esté completa, haga clic en **Upload Firmware** para enviar el firmware a la radio.

## Cambio en el comportamiento de Check for Update

Cuando **Check for Update** encuentra una versión de firmware más reciente, AetherSDR ahora muestra un mensaje informativo en lugar de ofrecer una descarga dentro de la aplicación:

> Actualización disponible: v*X.Y.Z*  
> Descargue el instalador de SmartSDR desde flexradio.com,  
> luego haga clic en 'Select Installer...' para prepararlo.

Descargue el instalador de flexradio.com de forma independiente y luego use **Select Installer...** como se describió anteriormente.

---

# Radio Setup — Pestaña RX: Fuente de referencia de 10 MHz (cambios v0.9.7)

## Cuadro combinado de fuente de oscilador

El cuadro combinado **10 MHz Reference Source:** en la pestaña **RX** se ha actualizado en v0.9.7. La lista de fuentes disponibles ahora se genera dinámicamente según el hardware presente y el estado del oscilador informado por la radio, en lugar de ser fija en el momento de abrir el diálogo.

### Opciones disponibles

| Etiqueta | Valor interno | Cuándo se muestra |
|---|---|---|
| Auto | `auto` | Siempre se muestra |
| TCXO | `tcxo` | Se muestra cuando hay hardware TCXO presente, se ha recibido el estado del oscilador, o el ajuste actual o guardado es `tcxo` |
| GPSDO | `gpsdo` | Se muestra cuando hay hardware GPSDO presente o el ajuste actual o guardado es `gpsdo` |
| External 10 MHz | `external` | Se muestra cuando hay una referencia externa presente, se ha recibido el estado del oscilador, o el ajuste actual o guardado es `external` |

Anteriormente, la opción de referencia externa aparecía en el combinado como **External**. Ahora aparece como **External 10 MHz**.

### Visualización del estado de bloqueo

La etiqueta de estado de bloqueo junto al combinado ahora muestra información más detallada que el texto simple `<STATE> Locked / Unlocked` usado anteriormente.

| Situación | Texto de ejemplo mostrado |
|---|---|
| Estado del oscilador aún no recibido | `Waiting for oscillator status` |
| Modo Auto ha resuelto a una fuente | `Auto -> GPSDO Locked` |
| Ajuste guardado difiere del estado activo | `TCXO -> GPSDO Locked` |
| Ajuste y estado coinciden | `GPSDO Locked` |
| External seleccionado pero referencia no detectada | `External 10 MHz Unlocked (not detected)` |

El color de la etiqueta se actualiza automáticamente: verde (`#00c040`) cuando está bloqueado, rojo (`#c04040`) cuando está desbloqueado y gris (`#8aa8c0`) mientras se espera el estado.

---

# Radio Setup — Pestaña Serial: Acciones de la rueda de sintonía FlexControl

## Acciones de rueda disponibles

A la perilla de sintonía FlexControl se le pueden asignar una o dos acciones personalizadas (una por pulsación de botón) en la pestaña **Serial**. A partir de v26.5.1, están disponibles dos nuevas acciones de rueda:

| Acción | Comportamiento |
|---|---|
| `WheelRit` | Ajusta RIT (Sintonización incremental del receptor) |
| `WheelXit` | Ajusta XIT (Sintonización incremental del transmisor) |

Estas se suman a las acciones de rueda existentes: `WheelFrequency`, `WheelVolume` y `WheelPower`.

### Para asignar una acción de rueda

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Serial**.
3. Localice la fila de FlexControl.
4. Haga clic en el cuadro combinado **Button n Action** para el botón deseado.
5. Seleccione la acción de rueda de la lista.
6. Cierre el diálogo. La acción surte efecto de inmediato.

---

# Radio Setup — Modo de ventana sin marco

A partir de v26.5.1, el diálogo Radio Setup usa una ventana sin marco con una barra de título personalizada cuando la aplicación se ejecuta en modo sin marco. Esto coincide con el aspecto de otros diálogos de AetherSDR.

- La barra de título personalizada incluye el nombre del diálogo ("Radio Setup") y los controles de ventana estándar (minimizar, cerrar).
- Puede arrastrar el diálogo por su barra de título.
- El diálogo se adapta automáticamente al ajuste de aplicación `FramelessWindow`.
