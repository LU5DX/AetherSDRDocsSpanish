# Descubrimiento automático de un Antenna Genius en la LAN

AetherSDR escucha dispositivos 4O3A Antenna Genius en la red local mediante descubrimiento UDP. Cuando se detecta un dispositivo, el applet Antenna Genius aparece automáticamente y se conecta sin ninguna configuración manual.

## Antes de comenzar

- El Antenna Genius debe estar encendido y conectado al mismo segmento de LAN que el equipo donde se ejecuta AetherSDR.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Inicie AetherSDR. El descubrimiento comienza de inmediato en segundo plano — no se requiere ninguna acción manual.
2. Cuando se detecta un dispositivo, el botón de bandeja **AG** aparece en la barra lateral derecha. Haga clic en **AG** para abrir el applet Antenna Genius.
3. Verifique la etiqueta de estado debajo del selector de dispositivo. Muestra **Device found** cuando el descubrimiento tiene éxito, y luego cambia a **Connected — \<name\> v\<version\>** una vez que se completa la conexión automática.
4. Confirme que el **Device combo** muestra su dispositivo con el nombre y la dirección IP correspondientes.
5. Si la etiqueta de estado muestra **Connected — \<name\> v\<version\>** y el botón **Connect / Disconnect** ahora indica **Disconnect**, el applet está conectado y listo para usarse.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Device combo | Lista todos los dispositivos encontrados por descubrimiento UDP. Selecciona y conecta automáticamente al primer dispositivo detectado. | Vacío hasta que el descubrimiento encuentra un dispositivo | — |
| Connect / Disconnect | Conecta al dispositivo seleccionado en el combo; cambia a **Disconnect** cuando está conectado. | **Connect** | — |
| Manual IP | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse directamente al puerto 9007. Se usa cuando el dispositivo no está en la LAN local. | Vacío (restaura el último valor utilizado al reiniciar) | `AG_ManualIp` |
| Status label | Muestra el estado actual del descubrimiento y la conexión. | **No device found** | — |

## Consejos

- AetherSDR se conecta automáticamente al primer dispositivo descubierto. Si tiene más de un Antenna Genius en la LAN, use el **Device combo** para seleccionar el correcto antes de hacer clic en **Connect**.
- Si los controles del Puerto B no son visibles después de conectarse, el dispositivo ha reportado un solo puerto de radio. Esto es normal.
- El valor ingresado en **Manual IP** se guarda como `AG_ManualIp` y se restaura la próxima vez que AetherSDR inicia, por lo que no es necesario volver a ingresarlo después de un reinicio.

## Solución de problemas

- **La etiqueta de estado permanece en "No device found"** — El Antenna Genius puede estar en un segmento de red o subred diferente que bloquea el tráfico de difusión UDP. Use el campo **Manual IP** para conectarse directamente por dirección IP. Consulte [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no es una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — El dispositivo era accesible pero la conexión falló. Verifique que el firmware del Antenna Genius esté en ejecución y que ningún cortafuegos esté bloqueando el puerto 9007.
- **El botón de bandeja AG no aparece** — El descubrimiento aún no ha encontrado un dispositivo. Espere unos segundos; si el botón sigue sin aparecer, verifique que el dispositivo esté encendido y en la misma LAN, o use **Manual IP** para conectarse directamente.

## Relacionados

- [Descripción general del Antenna Genius](overview.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o el Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
