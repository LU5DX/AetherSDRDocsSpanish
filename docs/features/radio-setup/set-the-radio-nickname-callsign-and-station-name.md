# Configurar el apodo, indicativo y nombre de estación del radio

Use esta página para asignar un apodo legible, un indicativo y un nombre de estación a su FLEX-8600. Estos valores identifican el radio y este cliente ante otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Radio (tab) en Radio Setup requiere una conexión activa con el radio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio** si no está seleccionada.
3. En el grupo **Radio Identification**, localice el campo **Nickname** y escriba el nombre que desea asignarle al radio.
4. Presione Tab o haga clic fuera del campo. AetherSDR envía el nuevo apodo al radio de inmediato.
5. Localice el campo **Callsign** y escriba su indicativo.
6. Presione Tab o haga clic fuera del campo. AetherSDR envía el indicativo al radio de inmediato.
7. Localice el campo **Station Name** y escriba el nombre para este cliente de estación. Si lo deja en blanco, AetherSDR utiliza el nombre de host del sistema operativo por defecto.
8. Presione Tab o haga clic fuera del campo. AetherSDR guarda el valor localmente y lo envía al radio.
9. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave persistente |
|---|---|---|---|
| **Nickname** | Etiqueta descriptiva para el radio, enviada al radio como `radio name`. | Nombre existente del radio | — (almacenado en el radio) |
| **Callsign** | Indicativo de la estación, enviado al radio como `radio callsign`. | Indicativo existente del radio | — (almacenado en el radio) |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se envía como `client station`. | Nombre de host del SO | `StationName` |

## Consejos

- **Nickname** y **Callsign** se almacenan en el propio radio, por lo que persisten cuando diferentes computadoras cliente se conectan al mismo radio.
- **Station Name** se almacena localmente en la configuración de AetherSDR (`StationName`) y también se anuncia al radio cada vez que lo edita. Otros clientes multiFLEX ven este nombre para distinguir qué estación es cuál.
- Los cambios surten efecto en cuanto sale de cada campo — no existe un botón Save independiente para estos tres campos.

## Relacionado

- [Verificar número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
