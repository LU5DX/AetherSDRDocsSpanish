# Descripción general de Configuración de bandas de TX

El cuadro de diálogo Configuración de bandas de TX permite ver y configurar los parámetros de transmisión por banda en su FLEX-8600, incluidos los límites de potencia, la potencia de sintonización, los ajustes de inhibición y el control del amplificador externo. Use esta página para adaptar el comportamiento de TX para cada banda de radioaficionado.

## Antes de comenzar

- Debe haber un radio FLEX-8600 conectado y encendido.
- La aplicación debe tener una conexión activa con el radio.

## Cómo funciona

El cuadro de diálogo Configuración de bandas de TX abre una interfaz con pestañas que muestra una pestaña por banda. Cada pestaña contiene controles de configuración de transmisión específicos para esa banda:

- **Límites de potencia** – Establece la potencia máxima de salida (en vatios) para la banda seleccionada. Ajustable desde 0 W hasta el máximo del radio.
- **Potencia de sintonización** – Establece el nivel de potencia utilizado durante las operaciones de sintonización. Generalmente es más bajo que el límite de potencia principal para evitar sobrecargar la antena.
- **Habilitar/deshabilitar banda** – Activa o desactiva si la banda está disponible para transmitir. Deshabilitar una banda evita la transmisión accidental fuera de las frecuencias permitidas.
- **Ajustes de inhibición** – Controla qué salidas de TX (ACC TX, TX1, TX2, TX3) se suprimen durante la sintonización. Se configura a través del menú `Settings > Inhibit during TUNE`.
- **Control del amplificador externo** – Configura las salidas de relé y clave para amplificadores externos por banda.

También se puede acceder al cuadro de diálogo desde el menú principal: **`Settings > TX Band Settings...`**

## Qué hace cada control

| Control | Propósito | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Configuración por banda (pestaña) | Muestra la configuración de transmisión para una sola banda, incluidos los límites de potencia, las opciones de habilitar/deshabilitar y las opciones de inhibición. | (ninguno) | (varía según el control dentro de la pestaña) | (ninguna) |
| Casilla de verificación Band Enable | Habilita o deshabilita TX en la banda seleccionada. Sin marcar = TX inhibida. | (habilitado) | On/Off | (clave por banda interna del radio) |
| Deslizador/campo Power Limit | Establece la potencia máxima de TX para la banda. | (varía según la banda) | 0 – máx. del radio (W) | (clave por banda interna del radio) |
| Deslizador/campo Tune Power | Establece la potencia utilizada durante la sintonización. | (varía) | 0 – máx. del radio (W) | (clave por banda interna del radio) |

## Consejos

- Use la opción habilitar/deshabilitar banda para evitar la transmisión accidental en bandas donde no tenga licencia o antena.
- El menú **Inhibit during TUNE** permite suprimir salidas de TX específicas (ACC TX, TX1, TX2, TX3) durante la sintonización — útil para evitar activar un amplificador durante los ciclos de sintonización.
- Los cambios realizados en Configuración de bandas de TX se envían directamente al radio; no se necesita un botón "Save" aparte.

## Relacionados

- [Radio Setup...](radio-setup-dialog.md)
- [Inhibit during TUNE](inhibit-during-tune.md)
