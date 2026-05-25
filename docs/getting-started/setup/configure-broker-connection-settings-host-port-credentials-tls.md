# Configurar ajustes de conexión del broker (host, puerto, credenciales, TLS)

Configure la dirección del broker MQTT, la autenticación y las opciones TLS que AetherSDR utiliza para conectarse al broker MQTT de su estación.

## Antes de comenzar

- El applet MQTT debe estar visible en la barra lateral derecha. Si está oculto, haga clic en el botón de la bandeja MQTT para mostrarlo.
- Necesita el nombre de host o dirección IP de su broker, el puerto y cualquier nombre de usuario y contraseña requeridos.

## Pasos

1. Abra `Settings > MQTT...` para mostrar el cuadro de diálogo de Configuración MQTT.
2. En la pestaña **Broker Connection**, ingrese lo siguiente:
   - **Host** — el nombre de host o dirección IP de su broker.
   - **Port** — el puerto TCP (el valor predeterminado depende de su broker; los valores comunes son 1883 para TCP simple o 8883 para TLS).
   - **Username** — opcional; déjelo en blanco si su broker no requiere autenticación.
   - **Password** — opcional; se almacena en su llavero del sistema cuando habilita la conexión por primera vez (no en texto plano).
3. Para habilitar TLS:
   - Marque **Use TLS**.
   - Si su broker utiliza un certificado CA personalizado, ingrese la ruta del archivo en **CA Certificate File** (o haga clic en **Browse...** para ubicarlo).
4. Haga clic en **OK** para guardar los ajustes y cerrar el cuadro de diálogo.
5. En el applet MQTT, haga clic en **Off** para cambiarlo a **On**. AetherSDR se conecta usando los nuevos ajustes. La etiqueta de estado cambia a **Connected** (verde) si tiene éxito, o muestra un mensaje de error si la conexión falla.

## Qué hace cada control

| Control | Valor predeterminado | Notas | Clave de ajuste |
|---------|---------------------|-------|-----------------|
| Host | (vacío) | Dirección del broker | (almacenada en el archivo de ajustes) |
| Port | (vacío) | Puerto TCP para la conexión | (almacenada en el archivo de ajustes) |
| Username | (vacío) | Nombre de usuario de autenticación | (almacenada en el archivo de ajustes) |
| Password | (vacío) | Almacenada en el llavero del sistema al usarse por primera vez | — |
| Use TLS | sin marcar | Activar/desactivar cifrado TLS | (almacenada en el archivo de ajustes) |
| CA Certificate File | (vacío) | Ruta al certificado CA personalizado para TLS | (almacenada en el archivo de ajustes) |

## Consejos

- La contraseña se migra a su llavero del sistema la primera vez que habilita la conexión MQTT. Si la migración falla, AetherSDR registra una advertencia y conserva la entrada en texto plano para reintentarlo.
- Si habilita la conexión ("On") pero la contraseña aún no se ha cargado desde el llavero, el estado muestra **Waiting for keychain** hasta que se complete la lectura del llavero.

## Solución de problemas

- **El estado muestra "Disconnected" después de activar On** — Verifique que el host y el puerto sean correctos y accesibles desde su máquina. Si usa TLS, confirme que la ruta del certificado CA sea válida.
- **El estado muestra un mensaje de error** — El broker rechazó la conexión. Confirme el nombre de usuario y la contraseña, y que los ajustes TLS coincidan con la configuración de su broker.
- **"Waiting for keychain" nunca se resuelve** — El llavero del sistema puede estar bloqueado o no disponible. Desbloquee su llavero y cambie la conexión a Off y luego a On nuevamente.

## Relacionado

- [Connect to a station MQTT broker](connect-to-a-station-mqtt-broker.md)
- [Enable TLS with a custom CA certificate](../../features/mqtt/enable-tls-with-a-custom-ca-certificate.md)
- [Open MQTT settings from the applet](../../features/mqtt/open-mqtt-settings-from-the-applet.md)
