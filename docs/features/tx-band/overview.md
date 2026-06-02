# Resumen de configuración de bandas de TX

El diálogo de configuración de bandas de TX permite ver y ajustar los parámetros de transmisión por banda en su FLEX-8600, incluyendo límites de potencia, potencia de sintonía, ajustes de inhibición y control de amplificador externo. Use esta página para personalizar el comportamiento de TX para cada banda de radioaficionado.

## Antes de comenzar

- Debe haber una radio FLEX-8600 conectada y encendida.
- La aplicación debe tener una conexión activa con la radio.

## Cómo funciona

El diálogo de configuración de bandas de TX abre una interfaz con pestañas que muestra una pestaña por banda. Cada pestaña contiene controles de configuración de transmisión específicos para esa banda:

- **Límites de potencia** – Establece la potencia máxima de salida (en vatios) para la banda seleccionada. Ajustable desde 0 W hasta el máximo de la radio.
- **Potencia de sintonía** – Establece el nivel de potencia utilizado durante las operaciones de sintonía. Generalmente es menor que el límite de potencia principal para evitar sobreexcitar la antena.
- **Habilitar/deshabilitar banda** – Activa o desactiva la disponibilidad de la banda para transmitir. Deshabilitar una banda evita la transmisión accidental fuera de las frecuencias permitidas.
- **Ajustes de inhibición** – Controla qué salidas de TX (ACC TX, TX1, TX2, TX3) se suprimen durante la sintonía. Se configura mediante el menú `Settings > Inhibit during TUNE`.
- **Control de amplificador externo** – Configura las salidas de relé y clave para amplificadores externos por banda.

También se puede acceder al diálogo desde el menú principal: **`Settings > TX Band Settings...`**

El diálogo utiliza un contenedor de tema persistente identificado como `dialog/txBand`, que aplica un estilo consistente a la ventana sin bordes.

## Función de cada control

| Control | Propósito | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Ajustes por banda (pestaña) | Muestra la configuración de transmisión para una sola banda, incluyendo límites de potencia, activación/desactivación y opciones de inhibición. | (ninguno) | (varía según el control dentro de la pestaña) | (ninguna) |
| Casilla Habilitar banda | Activa o desactiva la TX en la banda seleccionada. Sin marcar = TX inhibida. | (habilitado) | Activado/Desactivado | (clave interna por banda de la radio) |
| Deslizador/entrada de Límite de potencia | Establece la potencia máxima de TX para la banda. | (varía según la banda) | 0 – máximo de la radio (W) | (clave interna por banda de la radio) |
| Deslizador/entrada de Potencia de sintonía | Establece la potencia utilizada durante la sintonía. | (varía) | 0 – máximo de la radio (W) | (clave interna por banda de la radio) |

## Consejos

- Use la activación/desactivación de bandas para evitar la transmisión accidental en bandas donde no tenga licencia o antena.
- El menú **Inhibit during TUNE** permite suprimir salidas de TX específicas (ACC TX, TX1, TX2, TX3) durante la sintonía, útil para evitar activar un amplificador durante los ciclos de sintonía.
- Los cambios realizados en la configuración de bandas de TX se envían directamente a la radio; no se necesita un botón separado de "Guardar".
- El diálogo utiliza la clase base PersistentDialog de la versión v26.5.2.1, por lo que la posición y el tamaño de la ventana se recuerdan entre sesiones.

## Relacionados

- Radio Setup...
- Inhibit during TUNE
