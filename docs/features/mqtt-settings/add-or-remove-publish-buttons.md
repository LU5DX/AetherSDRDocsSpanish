# Agregar o quitar botones de publicación

Configure hasta 12 botones de publicación que envíen mensajes MQTT con un solo clic. Cada botón tiene una etiqueta, un tema y una carga útil que usted define en la pestaña Publish Buttons del diálogo MQTT Settings.

La pestaña Publish Buttons también muestra los temas internos que AetherSDR publica automáticamente. En la versión v26.6.3, puede habilitar o deshabilitar la mayoría de estos temas de publicación internos de forma individual.

## Antes de comenzar

- MQTT debe estar compilado en su versión de AetherSDR (el diálogo está protegido por la compuerta de compilación `HAVE_MQTT`).
- Debe configurarse una conexión a un broker MQTT. Consulte Configurar conexión al broker MQTT.

## Pasos

1. Abra el diálogo MQTT Settings: **Settings > MQTT...**.
2. Haga clic en la pestaña **Publish Buttons**.
3. Para agregar un botón, haga clic en **Add**. Aparecerá una nueva fila en la tabla con las celdas Label, Topic y Payload vacías.
4. Haga doble clic en cada celda y escriba los valores que desee.
5. Para quitar uno o más botones, seleccione sus filas (haga clic en el número de fila a la izquierda, o Ctrl+clic en varias filas) y haga clic en **Remove**.
6. Para habilitar o deshabilitar un tema de publicación interno, marque o desmarque su casilla en el cuadro de grupo **Internal AetherSDR Topics**.
7. Haga clic en **Apply** para guardar sin cerrar, o en **Ok** para guardar y cerrar.

## Función de cada control

| Control | Comportamiento | Límite |
|---|---|---|
| **Add** | Inserta una nueva fila en la tabla de botones. Deshabilitado cuando hay 12 filas. | 12 botones como máximo |
| **Remove** | Elimina las filas seleccionadas de la tabla de botones. | — |
| **Label** (celda de tabla) | Texto mostrado en el botón de publicación en el applet MQTT. | Texto editable |
| **Topic** (celda de tabla) | Cadena del tema MQTT enviada al hacer clic en el botón. | Texto editable |
| **Payload** (celda de tabla) | Cadena de carga útil MQTT enviada al hacer clic en el botón. | Texto editable |

## Temas de publicación internos de AetherSDR

El cuadro de grupo **Internal AetherSDR Topics** en la parte inferior de la pestaña Publish Buttons muestra los temas que AetherSDR publica automáticamente siempre que MQTT esté conectado. Cada tema tiene una casilla de verificación; desmarque un tema para dejar de publicarlo.

| Tema | Descripción | Predeterminado | Habilitado por defecto |
|---|---|---|---|
| `aethersdr/cw/decode` | Texto decodificado en CW | Sí | Sí |
| `aethersdr/radio/state` | Estado VFO / modo / TX de la radio | Sí | No |
| `aethersdr/ax25/rx` | Tramas AX.25 recibidas | Sí | No |

El tema **CW decoded text** (`aethersdr/cw/decode`) está habilitado por defecto; los otros dos temas de publicación están deshabilitados por defecto y deben marcarse para activarlos.

## Almacenamiento de configuración

- Todas las definiciones de botones se guardan en `MqttSettings` (clave JSON anidada `buttons`) al hacer clic en Apply u Ok.
- El estado de habilitación/deshabilitación de temas internos se guarda en `AppSettings` bajo claves como `mqtt_internal_aethersdr_radio_state`.

## Consejos

- Las filas con Label, Topic *y* Payload vacíos se omiten al guardar; puede dejar filas sin terminar.
- Las definiciones de botones se comparten entre el diálogo MQTT Settings y el panel del applet MQTT.

## Relacionado

- Configurar conexión al broker MQTT (host, puerto, credenciales, TLS)
- Configurar suscripciones MQTT
