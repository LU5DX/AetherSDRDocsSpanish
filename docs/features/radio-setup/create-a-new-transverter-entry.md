# Crear una nueva entrada de transverter

Use esta página para agregar una definición de transverter a su FLEX-8600, de modo que AetherSDR conozca el desplazamiento de frecuencia IF-a-RF y los parámetros de operación para la banda de su transverter.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.
- Conozca el rango de frecuencia IF que usa su transverter y el desplazamiento de frecuencia RF que desea mostrar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **XVTR**.
3. Haga clic en **Create New Transverter**.
4. Aparece una nueva pestaña anidada. Configure los campos para la nueva entrada en esa pestaña.
5. Para restringir la entrada a solo recepción, establezca **RX Only:** en el estado habilitado.
6. Para eliminar una entrada que ya no necesita, haga clic en **Remove** en la pestaña de esa entrada.
7. Cierre el diálogo con **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Create New Transverter** | Botón | Agrega una nueva entrada de transverter y abre su pestaña de configuración. |
| **RX Only:** | Botón de alternancia | Fuerza el transverter a solo recepción, evitando la transmisión a través de él. |
| **Remove** | Botón | Elimina permanentemente la definición de transverter seleccionada. |

## Sugerencias

- Cada transverter obtiene su propia pestaña anidada dentro de la pestaña XVTR. Si tiene varios transverters, use esas pestañas para cambiar entre entradas.
- Si necesita volver a este diálogo más adelante para ajustar un transverter, vuelva a abrir `Settings > Radio Setup...` y vaya directamente a la pestaña **XVTR**.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar la potencia TX máxima por banda y el modo de ajuste](set-per-band-tx-max-power-and-tune-mode.md)
