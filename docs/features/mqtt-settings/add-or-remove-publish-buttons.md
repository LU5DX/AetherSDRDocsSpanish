# Configurar botones de publicación MQTT

Configure hasta 12 botones de publicación que envían mensajes MQTT con un solo clic. Cada botón tiene una etiqueta, un tema y una carga útil que usted define en la pestaña Publish Buttons del diálogo MQTT Settings.

## Antes de comenzar

- MQTT debe estar compilado en su versión de AetherSDR (el diálogo está protegido por la compuerta de compilación `HAVE_MQTT`).
- Debe estar configurada una conexión con un broker MQTT. Consulte Configurar conexión con broker MQTT.

## Pasos

1. Abra el diálogo MQTT Settings: **Settings > MQTT...**.
2. Haga clic en la pestaña **Publish Buttons**.
3. Para agregar un botón, haga clic en **Add**. Aparece una nueva fila en la tabla con celdas vacías Label, Topic y Payload.
4. Haga doble clic en cada celda y escriba los valores que desee.
5. Para eliminar uno o más botones, seleccione sus filas (haga clic en el número de fila a la izquierda, o use Ctrl-clic para seleccionar varias filas) y haga clic en **Remove**.
6. Haga clic en **Apply** para guardar sin cerrar, o en **Ok** para guardar y cerrar.

## Qué hace cada control

| Control | Comportamiento | Límite |
|---|---|---|
| **Add** | Inserta una nueva fila en la tabla de botones. Se deshabilita cuando hay 12 filas presentes. | 12 botones como máximo |
| **Remove** | Elimina las filas seleccionadas de la tabla de botones. | — |
| **Label** (celda de tabla) | Texto mostrado en el botón de publicación en el applet MQTT. | Texto editable |
| **Topic** (celda de tabla) | Cadena de tema MQTT enviada al hacer clic en el botón. | Texto editable |
| **Payload** (celda de tabla) | Cadena de carga útil MQTT enviada al hacer clic en el botón. | Texto editable |

## Almacenamiento de configuración

- Todas las definiciones de botones se guardan en `MqttSettings` (clave JSON anidada `buttons`) al hacer clic en Apply u Ok.

## Consejos

- Las filas con Label, Topic *y* Payload vacíos se omiten al guardar; puede dejar filas sin completar.
- Las definiciones de botones se comparten entre el diálogo MQTT Settings y el panel del applet MQTT.

## Relacionado

- Configurar conexión con broker MQTT (host, puerto, credenciales, TLS)
- Configurar suscripciones MQTT

---

# Configurar conexión con broker MQTT

Configure la conexión entre AetherSDR y su broker MQTT, incluidos host, puerto, credenciales y ajustes TLS.

## Antes de comenzar

- MQTT debe estar compilado en su versión de AetherSDR (el diálogo está protegido por la compuerta de compilación `HAVE_MQTT`).

## Pasos

1. Abra el diálogo MQTT Settings: **Settings > MQTT...**.
2. En la pestaña **Broker**, configure la conexión:
   - **Host**: Introduzca el nombre de host o la dirección IP de su broker MQTT. El valor predeterminado es `localhost`.
   - **Port**: Introduzca el puerto TCP de su broker. El valor predeterminado es `1883`. El rango válido es 1–65535. El puerto cambia automáticamente entre 1883 y 8883 al alternar TLS.
   - **User**: Introduzca el nombre de usuario del broker si se requiere autenticación (opcional).
   - **Password**: Introduzca la contraseña del broker si se requiere autenticación (opcional). El campo está enmascarado.
   - **Use TLS**: Marque para habilitar el cifrado TLS. Marcar o desmarcar esta opción cambia automáticamente el puerto entre 1883 y 8883.
   - **CA cert**: Si TLS está habilitado, introduzca la ruta a un archivo de certificado CA, o haga clic en **Browse** para seleccionar uno. Déjelo en blanco para usar el paquete de CA del sistema. Este campo solo es visible cuando TLS está marcado.
3. Haga clic en **Apply** para guardar sin cerrar, o en **Ok** para guardar y cerrar.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Host** | Nombre de host o dirección IP del broker. | Se almacena en `MqttHost`. |
| **Port** | Puerto TCP del broker. | Se almacena en `MqttPort`. Cambia automáticamente entre 1883 y 8883 al alternar TLS. |
| **User** | Nombre de usuario del broker (opcional). | Se almacena en `MqttUser`. |
| **Password** | Contraseña del broker (opcional, enmascarada). | Se almacena en el llavero del sistema cuando está disponible; de lo contrario, se almacena solo para la sesión. |
| **Use TLS** | Habilita el cifrado TLS. | Se almacena en `MqttTls`. Muestra/oculta la fila del certificado CA. |
| **CA cert** | Ruta a un archivo de certificado CA. En blanco significa usar el paquete de CA del sistema. | Se almacena en `MqttCaFile`. La fila solo es visible cuando TLS está marcado. |
| **Apply** | Guarda todos los ajustes (conexión, temas, botones, contraseña) sin cerrar el diálogo. | Parte del QDialogButtonBox con Ok y Cancel. |

## Almacenamiento de contraseña

- Cuando AetherSDR se compila con soporte de llavero, la contraseña se almacena en el llavero del sistema (por ejemplo, Keychain en macOS, kwallet en Linux o Credential Manager en Windows).
- Cuando AetherSDR se compila sin soporte de llavero, la contraseña se almacena **solo en memoria** y debe volver a introducirse cada vez que se inicia la aplicación. Nunca se escribe en el almacén de configuración.
- Si anteriormente almacenó la contraseña en texto plano en la configuración (de una versión anterior), AetherSDR la migra al nuevo método de almacenamiento en el primer inicio y elimina la copia antigua en texto plano.

## Relacionado

- Configurar suscripciones MQTT
- Agregar o eliminar botones de publicación

---

# Configurar suscripciones MQTT

Suscríbase a temas MQTT y muestre sus mensajes en la superposición del panadapter. Usted define la lista de temas suscritos en la pestaña Subscriptions del diálogo MQTT Settings.

## Antes de comenzar

- MQTT debe estar compilado en su versión de AetherSDR (el diálogo está protegido por la compuerta de compilación `HAVE_MQTT`).
- Debe estar configurada una conexión con un broker MQTT. Consulte Configurar conexión con broker MQTT.

## Pasos

1. Abra el diálogo MQTT Settings: **Settings > MQTT...**.
2. Haga clic en la pestaña **Subscriptions**.
3. Para agregar una suscripción, haga clic en **Add**. Aparece una nueva fila en la tabla.
4. Haga doble clic en la celda **Topic** y escriba la cadena de tema a la que desea suscribirse.
5. Para mostrar mensajes en la superposición del panadapter, marque la casilla **Display** de esa fila.
6. Para eliminar una o más suscripciones, seleccione sus filas y haga clic en **Remove**.
7. Haga clic en **Apply** para guardar sin cerrar, o en **Ok** para guardar y cerrar.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Add** | Inserta una nueva fila en la tabla de suscripciones. | — |
| **Remove** | Elimina las filas seleccionadas de la tabla de suscripciones. | — |
| **Topic** (celda de tabla) | Cadena de tema MQTT a la que suscribirse. | Texto editable. |
| **Display** (celda de tabla) | Casilla; cuando está marcada, los mensajes de este tema se muestran en la superposición del panadapter. | — |

## Temas internos de AetherSDR

El cuadro de grupo **Internal AetherSDR Topics** en la parte inferior de la pestaña Subscriptions enumera los temas a los que AetherSDR se suscribe automáticamente siempre que MQTT está conectado. Estas suscripciones son de solo lectura y no se pueden eliminar.

AetherSDR se suscribe automáticamente a estos temas internos cuando se establece la conexión MQTT:

- `aethersdr/cw/decode` — Texto decodificado de CW
- `aethersdr/radio/state` — Estado de VFO / modo / TX de la radio
- `aethersdr/ax25/rx` — Tramas AX.25 recibidas

## Almacenamiento de configuración

- Todas las definiciones de suscripciones se guardan en `MqttSettings` al hacer clic en Apply u Ok.

## Relacionado

- Configurar conexión con broker MQTT (host, puerto, credenciales, TLS)
- Agregar o eliminar botones de publicación
