# Resumen del Mini-Pan

El Mini-Pan es un visor de banda estrecha compacto y desmontable (ancho de ±5 o ±10 kHz) centrado en la banda de recepción del VFO activo. Funciona de forma independiente del panadapter principal, brindándole una vista de cerca de la señal recibida que puede mantener por encima de otras aplicaciones, y permanece accesible desde el panel de applets incluso cuando el panadapter principal está oculto en el Modo Mínimo.

## Antes de comenzar

- Necesita una radio FLEX-8600 conectada.
- El panel de applets debe estar visible (o debe estar en el Modo Mínimo).

## Cómo funciona

El Mini-Pan es un applet, no un objeto de radio — no crea ningún panadapter ni slice. En su lugar, re-corta los marcos FFT que el pan del slice activo ya está transmitiendo, por lo que abrirlo no le cuesta nada adicional a la radio.

La vista está centrada en el centro de la banda de paso, no en la portadora, por lo que en SSB la señal recibida se sitúa en el medio del visor en lugar de pegarse a un borde. El trazo refleja la configuración de Línea/Relleno FFT del pan de origen y su rango en dBm, y la escala vertical del visor está fija de -130 dBm a -40 dBm.

Una lectura de frecuencia y un marcador de línea fina para la portadora se dibujan dentro del trazo, en la misma fila que las etiquetas de ancho. El detalle útil del visor lo determina el ancho de bin del panadapter principal, no el ancho en píxeles del propio applet.

El applet informa dos intenciones de vuelta a la ventana principal: si desea una fuente de espectro (visible u oculta) y cuándo cambia su ancho. Cuando está oculto — ya sea por el conmutador de la bandeja, el botón de cierre del contenedor, una flotación o un acoplamiento — la fuente se detiene, así que un applet oculto no cuesta nada por marco.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango válido | Clave de configuración |
| --- | --- | --- | --- | --- |
| **Ancho** (clic derecho en el visor) | Abre un menú para elegir el ancho de frecuencia del mini-pan; al seleccionarlo, re-corta el siguiente marco a la nueva ventana. | ±5 kHz | ±5 kHz (ancho de 10 kHz), ±10 kHz (ancho de 20 kHz) | `MiniPan` |
| **Lectura de VFO** | Muestra la frecuencia del VFO seguido y un marcador de línea fina, dibujados dentro del visor en la misma fila que las etiquetas de ancho. | — | — | — |

La elección del ancho se guarda en el objeto AppSettings `MiniPan` (el campo `spanKHz`). Si el valor se edita manualmente fuera de las dos opciones del menú, se restablece al predeterminado de ±5 kHz.

Flotar, acoplar, mantener siempre encima y cerrar se manejan mediante el ContainerTitleBar estándar que envuelve al applet — no están en el menú de clic derecho.

Para abrir el Mini-Pan: Panel de applets > ficha **Mini-Pan**.

## Consejos

- El rango vertical en dBm del visor es fijo y coincide con el rango del pan de origen — no se autoescala de forma independiente, por lo que la altura de una señal coincide con la del panadapter principal.
- En el Modo Mínimo, el panel de applets es la interfaz principal, así que el botón de bandeja **Mini-Pan** es el único punto de acceso a esta función.

## Relacionados

- [Abra el visor de banda estrecha mini-pan](open-the-mini-pan-narrow-scope.md)
- [Cambie el ancho del mini-pan con un clic derecho (5 o 10 kHz)](change-the-mini-pan-span-with-a-right-click-5-or-10-khz.md)
