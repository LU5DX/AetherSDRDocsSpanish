# Crear una nueva entrada de transverter

Esta página explica cómo agregar una definición de transverter a su FLEX-8600 para que AetherSDR pueda mostrar y sintonizar la frecuencia de salida del transverter en lugar de la frecuencia FI del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Radio Setup requiere una conexión activa con el radio.
- Conozca el rango de frecuencia FI y el desplazamiento de frecuencia de salida del transverter antes de comenzar.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **XVTR**.
3. Haga clic en **Create New Transverter**.

Una nueva entrada de transverter aparece como una pestaña anidada dentro de la pestaña XVTR.

4. Configure la entrada usando los controles de la nueva pestaña (rango de frecuencia, desplazamiento, nombre y configuración de solo RX — consulte a continuación).
5. Para eliminar una entrada en cualquier momento, seleccione su pestaña y haga clic en **Remove**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Create New Transverter** | Botón | Agrega una nueva entrada de transverter y crea una pestaña anidada para ella. |
| **RX Only:** | Botón de alternancia | Cuando está habilitado, impide transmitir a través de este transverter. |
| **Remove** | Botón | Elimina permanentemente la entrada de transverter seleccionada. |

## Consejos

- La pestaña XVTR utiliza pestañas anidadas: una pestaña por transverter, más una pestaña para crear nuevas entradas. Si tiene varios transverters, seleccione la pestaña anidada correcta antes de hacer clic en **Remove**.
- Si desea un transverter que no pueda transmitir (por ejemplo, un convertidor descendente solo de recepción), habilite **RX Only:** inmediatamente después de crear la entrada.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Configurar la potencia máxima de TX y el modo de sintonía por banda](set-per-band-tx-max-power-and-tune-mode.md)
