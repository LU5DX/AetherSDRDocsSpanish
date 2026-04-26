# Crear una nueva entrada de transverter

Use esta página para agregar una definición de transverter a su FLEX-8600 de modo que AetherSDR pueda mostrar y sintonizar frecuencias de RF por encima del rango nativo del equipo.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El diálogo Radio Setup requiere una conexión activa con el equipo.
- Conozca la frecuencia de FI que usa su transverter y el desplazamiento de frecuencia de RF que desea aplicar.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `XVTR`.
3. Haga clic en `Create New Transverter`.
4. Aparece una nueva pestaña anidada para la entrada del transverter. Configure la entrada usando los controles de esa pestaña.
5. Para restringir el transverter a solo recepción, active `RX Only:`.
6. Cierre el diálogo cuando termine. Los ajustes se envían al equipo de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Create New Transverter` | Botón de acción | Agrega una nueva entrada de transverter y abre una pestaña anidada para ella. |
| `RX Only:` | Botón de alternancia | Cuando está activado, impide transmitir a través de este transverter. |
| `Remove (xvtr)` | Botón de acción | Elimina la definición de transverter seleccionada del equipo. |

## Consejos

- Cada entrada de transverter aparece como su propia pestaña anidada dentro de la pestaña `XVTR`. Para editar una entrada existente, haga clic en su pestaña.
- Use `Remove (xvtr)` solo si ya no necesita la entrada. La eliminación es inmediata.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Configurar la potencia máxima de TX y el modo de ajuste por banda](set-per-band-tx-max-power-and-tune-mode.md)
