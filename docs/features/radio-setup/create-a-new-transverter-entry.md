# Crear una nueva entrada de transverter

Use esta página para agregar una definición de transverter a su FLEX-8600. Una vez creada, la radio expone el desplazamiento de frecuencia IF a RF del transverter, de modo que pueda sintonizar en la frecuencia de operación real en lugar de la frecuencia IF.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña XVTR solo está activa mientras haya una conexión de radio presente.
- Conozca el rango de frecuencia IF que utiliza su transverter y su desplazamiento de RF.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **XVTR**.
3. Haga clic en **Create New Transverter**.
4. Aparece una nueva pestaña anidada dentro de la pestaña XVTR. Configure la entrada usando los campos de esa pestaña.
5. Para restringir la entrada solo a recepción, habilite **RX Only:**.
6. Para eliminar una entrada que ya no necesita, haga clic en **Remove (xvtr)** en su pestaña.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Create New Transverter** | Botón | Agrega una nueva entrada de transverter y abre su pestaña de configuración. |
| **RX Only:** | Botón de alternancia | Cuando está habilitado, impide transmitir a través de este transverter. |
| **Remove (xvtr)** | Botón | Elimina permanentemente la definición del transverter de la radio. |

## Consejos

- Cada transverter tiene su propia pestaña anidada dentro de la pestaña XVTR. Si tiene varios transverters, cambie entre ellos usando esas pestañas internas.
- **RX Only:** es útil durante la configuración inicial cuando desea verificar la operación de recepción antes de permitir la transmisión.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Configurar la potencia TX máxima por banda y el modo de ajuste](set-per-band-tx-max-power-and-tune-mode.md)
