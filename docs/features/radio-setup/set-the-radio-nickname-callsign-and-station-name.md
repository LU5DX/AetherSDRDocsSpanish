# Establecer el apodo, indicativo y nombre de estación del equipo

Establezca un apodo legible, su indicativo y un nombre de estación en el FLEX-8600 conectado. Estos valores identifican el equipo y este cliente ante otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Los controles de la pestaña Radio no están disponibles sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar al equipo.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre al equipo de inmediato.
5. En el campo **Callsign**, escriba el indicativo de su estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica este cliente ante otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en **Close** para cerrar el cuadro de diálogo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Nickname** | Etiqueta descriptiva para el equipo. Se envía al equipo como nombre del radio. | Nombre reportado por el equipo | — |
| **Callsign** | Indicativo de su estación, almacenado en el equipo. | _(en blanco)_ | — |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. | Nombre de host del sistema operativo | `StationName` |

## Consejos

- Si **Nickname** se deja en blanco, AetherSDR rellena automáticamente el campo con el nombre reportado por el equipo en la red.
- **Station Name** utiliza de forma predeterminada el nombre de host del sistema operativo cuando no se ha guardado ningún valor. Para restaurar el valor predeterminado, borre el campo y presione Tab; luego vuelva a ingresar el nombre de host manualmente si es necesario.
- Los cambios en **Nickname** y **Callsign** se envían al equipo en el momento en que abandona cada campo. No se requiere ningún paso adicional de guardado o aplicación.
- **Station Name** se guarda localmente en la configuración de AetherSDR y también se envía al equipo como identificador de estación cliente para multiFLEX.

## Relacionado

- [Verificar número de serie, versión de hardware, región y opciones del equipo](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
