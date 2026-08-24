# Estado de Salud de la Radio

El diálogo de Estado de Salud de la Radio es una vista de diagnóstico en vivo, de solo lectura, de los registros de salud y estado de la radio conectada, agrupados según lo que reporte el backend de la radio. Es útil para monitorear cosas como indicadores de sobrecarga del ADC, temperatura u otra telemetría reportada por la radio, sin escribir nada en ella.

## Antes de comenzar

- Una radio FLEX-8600 debe estar conectada a AetherSDR.
- La radio debe reportar registros de salud; si no lo hace, el diálogo lo explica en lugar de mostrar una tabla vacía.

## Cómo funciona

El diálogo consulta al backend de la radio cada 500 ms para obtener una instantánea de salud y la muestra en una tabla con dos columnas: **Register** y **Value**. Los registros se agrupan bajo encabezados de sección en negrita, según lo reporte el backend.

- Un guion (—) en la columna **Value** significa que la radio no ha reportado ese registro; esto *no* es lo mismo que un valor de cero.
- Los valores booleanos se muestran como **Yes** o **No**, en lugar de `true`/`false` o `1`/`0`. Por ejemplo, un indicador de sobrecarga del ADC se lee como "Yes" o "No", no como un conteo.
- Los valores numéricos se muestran con dos decimales cuando corresponde.
- Si la radio no reporta ningún registro de salud, el diálogo muestra el mensaje "This radio reports no health registers." en lugar de una tabla inventada o rellena con ceros.
- Si no hay ninguna radio conectada, el diálogo muestra "Not connected."

El diálogo es estrictamente de solo lectura. Nada en esta pantalla escribe en la radio.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Health register table** | Enumera los registros de salud/estado en dos columnas: **Register** y **Value**. Las filas se pueden seleccionar pero no editar. Los colores alternados de fila y la ausencia de líneas de cuadrícula facilitan la lectura. |
| **Copy** | Copia toda la instantánea de salud al portapapeles como texto plano, incluidos los encabezados de sección y los pares registro/valor indentados. La línea de estado cambia brevemente a "Copied to clipboard" para confirmar. |
| **Status line** | Muestra "Updating every 500 ms" mientras el diálogo está activo, o los mensajes indicados anteriormente cuando está inactivo. |

## Consejos

- La tabla conserva la posición de desplazamiento y la selección de filas entre actualizaciones, lo que facilita observar un registro específico mientras se actualiza.
- Use **Copy** para capturar una instantánea para un ticket de soporte o una publicación en un foro; el texto del portapapeles ya viene formateado con encabezados de sección.
- La posición y el tamaño del diálogo se recuerdan entre sesiones (persistidos en `RadioHealthDialogGeometry`), de modo que puede dejarlo abierto en una esquina mientras opera.

## Solución de problemas

- **La tabla está vacía pero la radio está conectada** — O bien la radio no reporta registros de salud, o el backend aún no ha recibido ninguno. La línea de estado le indicará cuál es el caso: "This radio reports no health registers." significa que la radio realmente no tiene ninguno que mostrar.
- **Los valores se muestran como un guion (—)** — La radio aún no ha reportado ese registro en particular. Esto es normal para registros que solo aparecen bajo ciertas condiciones; espere al siguiente ciclo de actualización. Un guion nunca es un cero inventado.

## Relacionado

- [View the connected radio's health registers](../../getting-started/setup/view-the-connected-radio-s-health-registers.md)
