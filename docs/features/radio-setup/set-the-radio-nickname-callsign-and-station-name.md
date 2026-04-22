# Configurar el apodo, el indicativo y el nombre de estación del equipo

Configure un nombre legible, su indicativo y un identificador de estación en su FLEX-8600. Estos valores se almacenan en el equipo e identifican su cliente ante otras estaciones multiFLEX.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. La pestaña Radio en Radio Setup no está disponible sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el nombre que desea asignar al equipo y luego presione Tab o Enter para confirmar. AetherSDR envía el nuevo nombre al equipo de inmediato.
4. Localice el campo **Callsign**. Escriba su indicativo y luego presione Tab o Enter para confirmar.
5. Localice el campo **Station Name**. Escriba el nombre que identifica este cliente ante otras estaciones multiFLEX y luego presione Tab o Enter para confirmar. Si se deja vacío, AetherSDR utiliza el nombre de host del sistema operativo como valor predeterminado.
6. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado |
|---|---|---|---|
| **Nickname** | Campo de texto | Nombre descriptivo para el equipo. Se envía al equipo al confirmar. | Se obtiene del nombre actual del equipo si no se ha definido ningún apodo. |
| **Callsign** | Campo de texto | Indicativo de estación almacenado en el equipo. Se envía al equipo al confirmar. | Valor actual almacenado en el equipo. |
| **Station Name** | Campo de texto | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Se guarda localmente. Se envía al equipo al confirmar. | Nombre de host del sistema operativo si el campo nunca ha sido configurado. |

## Consejos

- Los tres campos envían su valor al equipo en cuanto se termina de editar (al perder el foco o al presionar Enter). No existe un botón Save independiente.
- **Station Name** se almacena en la configuración local de AetherSDR bajo la clave `StationName`. **Nickname** y **Callsign** se almacenan en el propio equipo, no en la configuración local de AetherSDR.

## Temas relacionados

- [Consultar el número de serie, la versión de hardware, la región y las opciones del equipo](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
