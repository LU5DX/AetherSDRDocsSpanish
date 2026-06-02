# Agregar o quitar botones de publicación

Configure hasta 12 botones de publicación que envíen mensajes MQTT con un solo clic. Cada botón tiene una etiqueta, un tema y una carga útil que usted define en la pestaña Publish Buttons del cuadro de diálogo MQTT Settings.

## Antes de comenzar

- MQTT debe estar compilado en su versión de AetherSDR (el cuadro de diálogo está protegido por la puerta de compilación `HAVE_MQTT`).
- Se debe configurar una conexión al broker MQTT. Consulte Configurar la conexión al broker MQTT.

## Pasos

1. Abra el cuadro de diálogo MQTT Settings: **Settings > MQTT...**.
2. Haga clic en la pestaña **Publish Buttons**.
3. Para agregar un botón, haga clic en **Add**. Aparece una nueva fila en la tabla con las celdas Label, Topic y Payload vacías.
4. Haga doble clic en cada celda y escriba los valores que desee.
5. Para quitar uno o más botones, seleccione sus filas (haga clic en el número de fila a la izquierda, o presione Ctrl+clic en varias filas) y haga clic en **Remove**.
6. Haga clic en **Apply** para guardar sin cerrar, o en **Ok** para guardar y cerrar.

## Función de cada control

| Control | Comportamiento | Límite |
|---|---|---|
| **Add** | Inserta una nueva fila en la tabla de botones. Deshabilitado cuando hay 12 filas presentes. | 12 botones como máximo |
| **Remove** | Elimina las filas seleccionadas de la tabla de botones. | — |
| **Label** (celda de tabla) | Texto mostrado en el botón de publicación en el applet de MQTT. | Texto editable |
| **Topic** (celda de tabla) | Cadena del tema MQTT que se envía al hacer clic en el botón. | Texto editable |
| **Payload** (celda de tabla) | Cadena de la carga útil MQTT que se envía al hacer clic en el botón. | Texto editable |

## Temas de publicación internos de AetherSDR

El cuadro de grupo **Internal AetherSDR Topics** en la parte inferior de la pestaña Publish Buttons enumera los temas que se publican automáticamente cuando MQTT está conectado. Estos temas no son configurables por el usuario:

`aethersdr/cw/decode`

## Almacenamiento de configuración

Todas las definiciones de botones se guardan en `MqttSettings` (clave JSON anidada `buttons`) al hacer clic en Apply u Ok.

## Consejos

- Las filas con Label, Topic *y* Payload vacíos se omiten al guardar; puede dejar filas sin terminar.
- Las definiciones de botones se comparten entre el cuadro de diálogo MQTT Settings y el panel del applet MQTT.

## Relacionado

- Configurar la conexión al broker MQTT (host, puerto, credenciales, TLS)
