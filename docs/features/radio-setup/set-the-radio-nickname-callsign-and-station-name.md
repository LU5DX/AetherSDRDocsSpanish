# Establecer el apodo, indicativo y nombre de estación del radio

Establezca el nombre legible, el indicativo y el identificador de estación almacenados en su FLEX-8600. Estos valores aparecen en las listas de clientes de multiFLEX y ayudan a identificar su radio en la red.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de la pestaña Radio (tab) no están disponibles sin una conexión activa al radio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio** si no está seleccionada.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el nombre que desea asignar al radio.
4. Presione Tab o haga clic fuera del campo. AetherSDR envía el nuevo apodo al radio de inmediato.
5. En el campo **Callsign**, escriba el indicativo de su estación.
6. Presione Tab o haga clic fuera del campo. AetherSDR envía el indicativo al radio de inmediato.
7. En el campo **Station Name**, escriba el nombre para esta estación cliente. Este valor identifica su instancia de AetherSDR ante otras estaciones multiFLEX. Si se deja vacío, se usa de forma predeterminada el nombre de host del sistema operativo.
8. Presione Tab o haga clic fuera del campo. AetherSDR guarda el valor localmente y lo envía al radio de inmediato.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Configuración persistida |
|---|---|---|---|
| **Nickname** | Nombre descriptivo asignado al radio. | Se completa con el nombre almacenado en el radio, si está definido. | Se almacena en el radio, no en AppSettings. |
| **Callsign** | Indicativo de estación almacenado en el radio. | Se completa con el indicativo almacenado en el radio, si está definido. | Se almacena en el radio, no en AppSettings. |
| **Station Name** | Nombre de este cliente AetherSDR, enviado al radio como identificador de estación cliente. | Nombre de host del sistema operativo si no se ha guardado ningún valor. | `StationName` |

## Consejos

- Cada campo se guarda en cuanto termina de editarlo — no hay un botón Save independiente. Mueva el foco fuera del campo para activar la actualización.
- **Station Name** es especialmente útil en configuraciones multiFLEX donde más de un cliente se conecta al mismo radio simultáneamente. Defina un nombre distinto en cada equipo.

## Relacionados

- [Verificar número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
