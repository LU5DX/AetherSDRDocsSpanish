# Omitir todo el clúster NR desde el mosaico ADSP de la cadena RX

Omita todos los reductores de ruido del lado del cliente (NR2, NR4, MNR, DFNR, RN2, BNR) a la vez usando el mosaico ADSP en la cadena RX. El mosaico recuerda qué reductor de ruido estaba activo antes de la omisión, por lo que al hacer clic nuevamente se restaura ese módulo.

## Antes de comenzar

- El contenedor de la Cadena de Audio Aetherial debe estar visible. Haga clic en el botón de la bandeja **PUDU** en la barra lateral derecha para activarlo o desactivarlo.
- Haga clic en **RX** en la fila del encabezado para mostrar la cadena DSP de RX.

## Pasos

1. Localice el mosaico **ADSP** en la tira de la cadena RX. Se encuentra entre **RADIO** (izquierda) y **SPEAK** (derecha).
   - Cuando un reductor de ruido está activo, el mosaico muestra su nombre corto (ej. `NR2`, `NR4`, `BNR`).
   - Cuando ningún reductor de ruido está activo, el mosaico muestra `ADSP`.

2. **Haga un solo clic** en el mosaico **ADSP**.

   - Todos los reductores de ruido del lado del cliente se omiten. La etiqueta del mosaico muestra `ADSP`.
   - AetherSDR toma una instantánea en memoria de qué reductor de ruido estaba activo.

3. Para restaurar el reductor de ruido anterior, **haga un solo clic** en el mosaico **ADSP** nuevamente.

   - El módulo previamente activo se vuelve a habilitar y su nombre corto reaparece en el mosaico. Si no había ningún módulo activo al momento de la omisión, se habilita NR2 como valor predeterminado.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Mosaico ADSP** | Haga clic para omitir todo el clúster NR. La etiqueta cambia para mostrar el nombre corto del módulo activo (`NR2`, `NR4`, `BNR`) o `ADSP` cuando ninguno está encendido. Haga doble clic para abrir el diálogo de Configuración de AetherDSP. |
| **Botón BYPASS** | Deshabilita todas las etapas en la cadena actual (TX o RX). No afecta la omisión de ADSP — operan de forma independiente. |

## Consejos

- La omisión de ADSP es independiente del botón **BYPASS**. Omitir todas las etapas de RX con **BYPASS** no afecta el estado del mosaico ADSP, y viceversa.
- Haga doble clic en el mosaico **ADSP** para abrir la Configuración de AetherDSP y ajustar finamente los parámetros individuales del reductor de ruido.

## Relacionados

- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Ver de un vistazo si el audio del PC, el reductor de ruido y la salida de audio están activos (mosaicos de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
