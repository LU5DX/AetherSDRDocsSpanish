# Configurar el apodo, indicativo y nombre de estación del equipo

Cambie la forma en que el equipo y este cliente se identifican: el apodo aparece en las listas de conexión, el indicativo se almacena en el equipo y el nombre de estación identifica a este cliente de AetherSDR ante otras estaciones multiFLEX.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Los controles de la pestaña Radio no están disponibles sin una conexión activa.

## Pasos

1. Vaya a `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio** si no está seleccionada.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el nombre que desea usar para este equipo y presione Tab o Enter para confirmar.
4. En el mismo grupo, localice el campo **Callsign**. Escriba su indicativo y presione Tab o Enter para confirmar.
5. Localice el campo **Station Name**. Escriba el nombre que identifica a este cliente ante otras estaciones multiFLEX y presione Tab o Enter para confirmar.
6. Haga clic en **Close**.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Persistencia |
|---|---|---|---|
| **Nickname** | Nombre descriptivo almacenado en el equipo. Se envía al equipo al terminar la edición. | Se obtiene del nombre actual del equipo si no se ha definido un apodo. | En el equipo (no en la configuración de la aplicación AetherSDR) |
| **Callsign** | Indicativo de estación almacenado en el equipo. Se envía al equipo al terminar la edición. | Indicativo actual del equipo. | En el equipo |
| **Station Name** | Identifica a este cliente de AetherSDR ante otras estaciones multiFLEX. Se envía al equipo como nombre de estación del cliente. | Nombre de host del sistema operativo si el campo no se ha definido anteriormente. | `StationName` |

## Sugerencias

- Cada campo se aplica de inmediato al presionar Tab o Enter; no existe un botón de guardar independiente para estos campos.
- **Station Name** usa por defecto el nombre de host del sistema operativo si nunca se ha introducido un valor. Para restaurar ese valor predeterminado, borre el campo, presione Enter y vuelva a abrir el cuadro de diálogo; mostrará el nombre de host nuevamente.

## Relacionado

- [Consultar número de serie, versión de hardware, región y opciones del equipo](check-radio-serial-hardware-version-region-and-options.md)
