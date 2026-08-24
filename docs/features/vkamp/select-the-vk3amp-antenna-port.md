# Seleccionar el puerto de antena del VK3AMP

Seleccione qué puerto de antena (1–3) el amplificador VK3AMP enruta la RF hacia él. La propia tabla de control del amplificador puede anular una selección en unos 50 ms, por lo que el applet refleja el estado en vivo en lugar de asumir que su clic fue aceptado.

## Antes de comenzar

- Se requiere una conexión de radio (el applet está deshabilitado sin una).
- Abra el applet VK3AMP Amplifier desde el panel Applet > mosaico VKAMP.

## Pasos

1. Espere a que la píldora de estado de conexión del amplificador en el encabezado del applet muestre un estado conectado.
2. En la fila ANT, haga clic en el puerto de antena que desea usar: **1**, **2** o **3**.
3. Confirme que el clic surtió efecto. La lectura ANT del applet (junto a "ANT" en la cuadrícula de información) y el resaltado del botón solo se mueven después de que el estado en vivo del amplificador confirme la selección.

## Qué hace cada control

| Control | Propósito | Notas |
| --- | --- | --- |
| **1** | Seleccionar puerto de antena 1 | La pantalla de solo lectura refleja el estado en vivo; la propia tabla del amplificador puede revertir una selección en ~50 ms. |
| **2** | Seleccionar puerto de antena 2 | Igual que el anterior. |
| **3** | Seleccionar puerto de antena 3 | Igual que el anterior. |

## Consejos

- Los botones de antena se tratan como pantallas de solo lectura, no como botones optimistas. Si su clic no parece registrarse, puede ser porque la tabla de control del amplificador rechazó o revirtió la selección — verifique la lectura ANT del applet y el puerto resaltado para conocer el estado autoritativo.

## Relacionado

- [Descripción general del amplificador VK3AMP](overview.md)
- [Pasar por alto el amplificador VK3AMP](bypass-the-vk3amp-amplifier.md)
- [Monitorear la potencia directa y reflejada en el amplificador VK3AMP](monitor-forward-and-reflected-power-on-the-vk3amp-amplifier.md)
- [Restablecer el amplificador VK3AMP](reset-the-vk3amp-amplifier.md)
