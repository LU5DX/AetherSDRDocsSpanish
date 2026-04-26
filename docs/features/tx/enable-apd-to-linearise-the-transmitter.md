# Habilitar APD para linealizar el transmisor

APD (Predistorsión Adaptativa) reduce la no linealidad del transmisor aplicando un ecualizador de corrección a la señal TX. Actívelo para mejorar la pureza espectral, especialmente en SSB y modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. APD requiere una conexión de radio activa.
- Abra el applet TX Controls si no está visible.

## Pasos

1. Haga clic en el botón **TX** de la bandeja en la barra lateral derecha para abrir el applet TX Controls, si no está visible.
2. Haga clic en **APD**. El fondo del botón se torna verde cuando está habilitado.
3. Observe los indicadores de estado a la derecha de **APD**:
   - **Cal** se ilumina en verde mientras el radio se calibra.
   - **Avail** se ilumina en verde cuando hay un resultado de calibración disponible pero aún no aplicado.
   - **Active** se ilumina en verde cuando el ecualizador está aplicado y APD está completamente operativo.
4. Cuando **Active** está encendido, APD está en funcionamiento. No se requiere ninguna acción adicional.
5. Para deshabilitar APD, haga clic en **APD** nuevamente. El botón vuelve a su estado apagado y los tres indicadores se atenúan.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado |
|---|---|---|---|
| **APD** | Botón de alternancia | Habilita o deshabilita la predistorsión adaptativa en el radio. Verde cuando está activo, apagado cuando está inactivo. | Apagado |
| **Active** | Indicador | Se ilumina en verde cuando APD está activo y el ecualizador se aplica a la señal TX. | Atenuado |
| **Cal** | Indicador | Se ilumina en verde cuando APD está activo y el radio aún se está calibrando. | Atenuado |
| **Avail** | Indicador | Se ilumina en verde cuando APD está activo y hay una calibración disponible pero aún no aplicada. | Atenuado |

## Consejos

- La progresión normal tras habilitar APD es: **Cal** → **Avail** → **Active**. Si el indicador se detiene en **Cal** o **Avail**, transmitir una señal proporciona al radio los datos necesarios para completar la calibración.
- El estado de APD se controla en el propio radio. Si desconecta y reconecta, los estados de los indicadores reflejarán lo que reporte el radio.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Ajustar la potencia de salida RF](set-rf-output-power.md)
- [Cambiar perfiles TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
