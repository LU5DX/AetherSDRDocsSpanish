# Agregar o quitar botones de publicación

Configure hasta 12 botones de publicación que envíen mensajes MQTT con un solo clic. Cada botón tiene una etiqueta, un tema y una carga útil que usted define en la pestaña Botones de Publicación del diálogo Configuración MQTT.

## Antes de empezar

- MQTT debe estar compilado en su versión de AetherSDR (el diálogo está protegido por la puerta de compilación `HAVE_MQTT`).
- Debe configurarse una conexión con un broker MQTT. Consulte Configure MQTT broker connection.

## Pasos

1. Abra el diálogo Configuración MQTT: **Settings > MQTT...**.
2. Haga clic en la pestaña **Publish Buttons**.
3. Para agregar un botón, haga clic en **Add**. Aparece una nueva fila en la tabla con las celdas Label, Topic y Payload vacías.
4. Haga doble clic en cada celda y escriba los valores deseados.
5. Para eliminar uno o más botones, seleccione sus filas (haga clic en el número de fila a la izquierda, o Ctrl+clic en varias filas) y haga clic en **Remove**.
6. Haga clic en **Apply** para guardar sin cerrar, u **Ok** para guardar y cerrar.

## Función de cada control

| Control | Comportamiento | Límite |
|---|---|---|
| **Add** | Inserta una nueva fila en la tabla de botones. Se desactiva cuando hay 12 filas presentes. | 12 botones como máximo |
| **Remove** | Elimina las filas seleccionadas de la tabla de botones. | — |
| **Label** (celda de tabla) | Texto mostrado en el botón de publicación en el applet MQTT. | Texto editable |
| **Topic** (celda de tabla) | Cadena del tema MQTT que se envía al hacer clic en el botón. | Texto editable |
| **Payload** (celda de tabla) | Cadena de la carga útil MQTT que se envía al hacer clic en el botón. | Texto editable |

Todas las definiciones de botones se guardan en `MqttSettings` (clave JSON anidada `buttons`) al hacer clic en Apply u Ok.

## Consejos

- Las filas con Label, Topic *y* Payload vacíos se omiten al guardar; puede dejar filas sin completar.
- Las definiciones de botones se comparten entre el diálogo Configuración MQTT y el panel del applet MQTT.

## Relacionado

- Configure MQTT broker connection (host, port, credentials, TLS)
