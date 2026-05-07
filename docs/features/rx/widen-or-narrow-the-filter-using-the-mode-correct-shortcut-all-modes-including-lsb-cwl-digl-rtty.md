# Ampliar o reducir el filtro usando el acceso directo de corrección por modo (todos los modos, incluidos LSB/CWL/DIGL/RTTY)

Use el acceso directo de ampliar/reducir para recorrer los valores preestablecidos de ancho de filtro por modo: una pulsación amplía el filtro, la otra lo reduce. El acceso directo siempre aplica anchos de filtro adecuados al modo del segmento activo, por lo que nunca obtendrá un filtro de ancho de CW en SSB ni un filtro de ancho de radiodifusión en RTTY.

## Antes de comenzar

- Debe haber una radio conectada.
- El applet de controles de recepción (RX Controls) debe estar visible (botón de bandeja **RX** en la barra lateral derecha).

## Pasos

1. En el applet RX Controls, haga clic en el **menú desplegable Mode** y seleccione el modo que desea utilizar (USB, LSB, CW, AM, SAM, DIGU, DIGL, RTTY, FM, etc.). La lista de valores preestablecidos de filtro y los tamaños de paso se actualizan para ese modo.
2. Haga clic en el botón de triángulo apuntando a la izquierda (◀) junto al indicador de ancho de filtro para reducirlo, o en el botón de triángulo apuntando a la derecha (▶) para ampliarlo.

Cada clic recorre la lista de valores preestablecidos del modo. El ancho de filtro actual se muestra en el indicador **2.7K** (ancho de filtro).

## Función de cada control

| Control | Valor predeterminado | Comportamiento | Notas |
|---------|---------------------|----------------|-------|
| **Valores preestablecidos de ancho de filtro (◀ / ▶)** | Ver más abajo | Recorre los anchos de filtro por modo en orden descendente (◀) o ascendente (▶). | El método `stepFilterWidth(direction)` recorre la lista de valores preestablecidos por modo para una corrección de ampliación/reducción según el modo (#2208). |
| **2.7K (ancho de filtro)** | Dependiente del modo | Muestra el ancho de banda actual del filtro del segmento activo. | Se actualiza cuando se aplica un valor preestablecido. La lectura se comparte con el panel VFO y utiliza formato sensible al modo (#2197). |

## Valores preestablecidos de ancho de filtro por modo

| Modo | Valores preestablecidos (Hz) |
|------|------------------------------|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW | 50, 100, 250, 400 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin valores preestablecidos de filtro (botones ocultos) |

## Relacionado

- [Seleccionar un valor preestablecido de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar de modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
