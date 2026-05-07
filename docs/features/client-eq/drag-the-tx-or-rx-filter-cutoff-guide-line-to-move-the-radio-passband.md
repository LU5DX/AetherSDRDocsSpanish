# Arrastre la línea guía de corte de TX o RX para mover la banda pasante del radio

El lienzo del editor de EQ muestra líneas verticales amarillas discontinuas en los bordes de corte actuales del filtro de TX o RX del radio. Arrastrar estas líneas mueve la banda pasante del radio en tiempo real, lo que le permite ajustar la forma de su EQ a los límites reales del filtro sin salir del editor de EQ.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El editor flotante para el lado correspondiente (TX o RX) debe estar abierto. Las líneas guía se pueden arrastrar solo en el lienzo del editor sin marco, no en el mosaico del applet acoplado.
- Para abrir el editor flotante, haga doble clic en la etapa EQ en el widget CHAIN en el lado TX o RX. Consulte [Abra el editor sin marco para agregar/eliminar/ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Pasos

1. Abra el editor flotante para el lado que desea ajustar: haga doble clic en la etapa EQ en el widget CHAIN. La barra de título del editor muestra "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice las líneas verticales amarillas discontinuas en el lienzo. Hay dos: una en el borde de corte bajo y otra en el borde de corte alto de la banda pasante actual del radio.
3. Mueva el puntero hacia una de las líneas amarillas discontinuas. Cuando el puntero esté lo suficientemente cerca de la línea, el cursor cambiará a una flecha de redimensionamiento horizontal.
4. Haga clic y arrastre la línea hacia la izquierda o la derecha. El corte de filtro correspondiente del radio se actualiza en tiempo real mientras arrastra.
5. Suelte para establecer la nueva posición de corte.
6. Repita el proceso con la otra línea guía si desea ajustar el borde opuesto de la banda pasante.

## Qué hace cada control

| Control                                    | Comportamiento                                                                                                                                                                                                                                                                                                                                                 | Notas                                                                                                                                                                                                                                                 |
|--------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Líneas guía de corte de filtro (TX)        | Líneas verticales amarillas discontinuas en el lienzo del editor de TX que marcan los cortes de filtro bajo y alto de TX actuales del radio. Arrastre en el editor para mover la banda pasante de TX del radio en tiempo real.                                                                                                                                  | El cursor cambia a una flecha de redimensionamiento horizontal al pasar el ratón cerca de una línea.                                                                                                                                                  |
| Líneas guía de corte de filtro (RX)        | Líneas verticales amarillas discontinuas en el lienzo del editor de RX que marcan los bordes de la banda pasante de RX del slice activo (en el dominio de la frecuencia de audio). Arrastre en el editor para mover la banda pasante de RX del radio en tiempo real.                                                                                            | El cursor cambia a una flecha de redimensionamiento horizontal al pasar el ratón cerca de una línea.                                                                                                                                                  |
| Suavizado                                  | Aplica un promediado de potencia por fracción de octava a la traza del analizador para su visualización; no afecta el cálculo de EQ. Una fracción más baja = más suavizado (1/3 es el máximo suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores de TX y RX.                                                                         | Tooltip: "Suavizado de fracción de octava aplicado a la traza del analizador. Fracción más baja = más suavizado (1/3 = máximo, 1/96 = desactivado). Afecta solo la visualización: el cálculo de EQ no cambia." Ubicado en la franja del encabezado del editor (solo editor flotante). |
| Fila de iconos de tipo de filtro           | Una fila de 8 iconos personalizados (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma de filtro actual (campana pico, rampa estante, pendiente HP/LP) en el color de la paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro para esa banda; al hacer clic también se selecciona la banda, resaltando su asa en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está desviada. Implementado por ClientEqIconRow.                                                                                                      |
| Fila de texto de parámetros                | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores de Freq, Gain y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. En la versión 0.9.7, el fondo de la fila es transparente, por lo que ya no oscurece la franja del plan de bandas de audio directamente encima; las etiquetas están alineadas en la parte inferior dentro de cada columna. | Ubicado solo en el editor flotante. Implementado por ClientEqParamRow.                                                                                                                                                                                 |
| Líneas guía de corte de filtro (TX / RX)   | Líneas verticales amarillas discontinuas superpuestas en el lienzo en los cortes de filtro bajo/alto de TX actuales del radio (mosaico TX) o en los bordes de la banda pasante de RX (mosaico RX). Al pasar el ratón cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente del radio en tiempo real.                       | Arrastrar las guías de corte de TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías de RX escribe en el SliceModel activo. Pase 0 para un borde con el fin de suprimir esa guía.                     |

## Consejos

- Las líneas guía son visibles tanto en el mosaico del applet acoplado como en el editor flotante, pero el arrastre solo está activo en el lienzo del editor flotante.
- Una línea guía está ausente cuando el valor de corte correspondiente es 0 o no está establecido por el radio.
- Observe la fila de texto de parámetros en la parte inferior del editor mientras arrastra para confirmar los bordes de banda pasante resultantes.

## Solución de problemas

- **El cursor no cambia a una flecha de redimensionamiento horizontal cerca de la línea** — Está pasando el ratón sobre el mosaico del applet acoplado, no sobre el lienzo del editor flotante. Abra el editor flotante haciendo doble clic en la etapa EQ en el widget CHAIN y vuelva a intentarlo.
- **No se ven líneas amarillas discontinuas en el lienzo** — El radio no ha informado valores de corte de filtro, o ambos valores de corte son 0. Verifique que el radio esté conectado y que un slice esté activo.

## Relacionados

- [Abra el editor sin marco para agregar/eliminar/ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspeccione la curva de EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccione la curva de EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Lea los valores exactos de frecuencia/ganancia/Q en la fila de texto de parámetros](read-exact-freq-gain-q-values-in-the-parameter-text-row.md)
