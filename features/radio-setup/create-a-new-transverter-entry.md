# Crear una nueva entrada de transverter

Use esta página para agregar una definición de transverter a su FLEX-8600, de modo que AetherSDR pueda aplicar el desplazamiento de frecuencia correcto y mostrar la frecuencia de salida del transverter en el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña `XVTR` no está disponible cuando está desconectado.
- Tenga a mano la frecuencia FI que utiliza su transverter (la frecuencia en la que el FLEX-8600 transmitirá y recibirá realmente) y el rango de frecuencia de salida que desea mostrar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña `XVTR`.
3. Haga clic en `Create New Transverter`.

Aparece una nueva entrada de transverter como pestaña anidada dentro de la pestaña `XVTR`. Configure la entrada usando los controles descritos a continuación.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Create New Transverter` | Botón | Agrega una nueva entrada de transverter como pestaña anidada. |
| `RX Only:` | Botón de alternancia | Cuando está habilitado, impide transmitir a través de este transverter. Úselo para conversores de solo recepción o cuando desee proteger el hardware conectado a la salida. |
| `Remove` | Botón | Elimina permanentemente la definición de transverter seleccionada del radio. |

## Consejos

- Si solo desea monitorear una banda de transverter sin arriesgar una transmisión hacia el conversor, habilite `RX Only:` inmediatamente después de crear la entrada.
- Para eliminar un transverter que ya no necesita, seleccione su pestaña y haga clic en `Remove`.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Configurar la potencia máxima de TX y el modo de ajuste por banda](set-per-band-tx-max-power-and-tune-mode.md)
