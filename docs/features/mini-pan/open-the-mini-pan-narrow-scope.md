# Abrir el mini-pan de alcance estrecho

Abra el Mini-Pan, un alcance de banda estrecha centrado en la banda pasante de recepción del VFO activo, para observar una porción distinta del espectro, independiente del panadapter principal.

## Antes de comenzar

- Conéctese a su radio FLEX-8600.
- Asegúrese de que el panel de applets esté visible (se muestra por defecto y también está disponible en el Modo Mínimo).

## Pasos

1. En el panel de applets, haga clic en el mosaico Mini-Pan.
2. Se abre el alcance Mini-Pan, que muestra la banda pasante de recepción del VFO activo con una línea fina sobre la frecuencia de la portadora.
3. Para cerrar el alcance, haga clic en el botón de cierre de su barra de título (el alcance se oculta; no consume recursos del radio cuando está oculto).

El Mini-Pan flota sobre otras aplicaciones por defecto. También puede acoplarlo, mantenerlo siempre en primer plano o cerrarlo mediante los controles de su barra de título.

## Función de cada control

| Control | Comportamiento | Valor predeterminado / Rango | Clave de ajuste |
| --- | --- | --- | --- |
| Mosaico Mini-Pan | Abre y cierra el alcance. | — | — |
| Alcance (clic derecho) | Abre un menú para elegir el ancho de banda. | ±5 kHz (10 kHz de ancho total) | `MiniPan` |
| Lectura del VFO | Muestra la frecuencia del VFO seguido, dibujada dentro de la traza en la misma fila que las etiquetas de ancho. | — | — |
| Controles de la barra de título | Flotar, acoplar, siempre en primer plano, cerrar. Se gestionan mediante la barra de título estándar del contenedor. | — | — |

El rango en dBm del alcance es fijo, de -130 a -40. La lectura de frecuencia y la línea fina están centradas en el centro de la banda pasante, no en la portadora.

## Consejos

- El alcance está centrado en el centro de la banda pasante, no en la portadora, por lo que en SSB la señal recibida aparece en el centro de la vista.
- El alcance refleja los ajustes de Línea/Relleno FFT del panadapter principal, por lo que coincidirá con la apariencia de su espectro principal.
- El Mini-Pan es solo una vista: no crea ningún panadapter ni slice, por lo que abrirlo no tiene ningún costo para el radio.

## Solución de problemas

- **El mosaico Mini-Pan no es visible** — El panel de applets puede estar oculto. Consulte el menú View para ver los ajustes del panel de applets, o entre en el Modo Mínimo donde se muestra el panel de applets.
- **El alcance muestra una lectura de marcador `—.———`** — No hay una frecuencia de VFO válida disponible. Verifique que esté conectado a un radio y que haya un slice válido activo.

## Relacionado

- [Descripción general del Mini-Pan](overview.md)
- [Cambie el ancho del mini-pan con un clic derecho (5 o 10 kHz)](change-the-mini-pan-span-with-a-right-click-5-or-10-khz.md)
