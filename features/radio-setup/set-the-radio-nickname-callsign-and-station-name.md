# Configurar el apodo, indicativo y nombre de estación del radio

Configure un apodo legible, su indicativo de estación y un nombre de estación en el FLEX-8600 conectado. Estos valores identifican el radio y este cliente ante otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los campos de la pestaña Radio (tab) no son editables mientras está desconectado.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar al radio.
4. Presione Tab o haga clic fuera del campo. AetherSDR envía el nuevo apodo al radio de inmediato.
5. Localice el campo **Callsign**. Escriba su indicativo.
6. Presione Tab o haga clic fuera del campo. AetherSDR envía el indicativo al radio de inmediato.
7. Localice el campo **Station Name**. Escriba el nombre que identifica este cliente ante otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo. AetherSDR guarda el valor localmente y lo envía al radio de inmediato.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Nickname** | Etiqueta descriptiva para el radio. Se almacena en el radio. | Nombre reportado por el radio | — |
| **Callsign** | Indicativo de la estación. Se almacena en el radio. | Valor reportado por el radio | — |
| **Station Name** | Identifica este cliente ante otras estaciones multiFLEX. Se almacena localmente y se envía al radio al cambiar. | Nombre de host del sistema operativo | `StationName` |

## Consejos

- Los cambios surten efecto en cuanto sale de cada campo — no hay un botón de guardado independiente.
- **Station Name** toma por defecto el nombre de host del sistema operativo si el campo nunca ha sido configurado. Para restaurar ese valor predeterminado, borre el campo y presione Tab; revertirá al nombre de host la próxima vez que se abra el diálogo.
- **Nickname** y **Callsign** se almacenan en el radio mismo. **Station Name** se almacena en la configuración local de AetherSDR bajo la clave `StationName` y también se envía al radio como identificador de la estación cliente.

## Solución de problemas

- **Los campos aparecen vacíos al abrir el diálogo** — Es posible que la conexión al radio no haya terminado de enviar su estado inicial. Cierre y vuelva a abrir el diálogo después de que la barra de estado del radio muestre que está conectado.
- **Los cambios no aparecen en otros clientes multiFLEX** — Confirme que el radio está en línea y que la sesión del protocolo SmartSDR está activa. Solo los valores enviados mientras está conectado son recibidos por los demás clientes.

## Relacionados

- [Verificar número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
