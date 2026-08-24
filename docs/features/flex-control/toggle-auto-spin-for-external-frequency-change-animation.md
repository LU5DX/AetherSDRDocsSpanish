# Alternar la animación de giro automático para cambios de frecuencia externos

Active o desactive la animación automática de giro de la rueda virtual que se reproduce cuando una fuente externa cambia la frecuencia de la franja, como al hacer clic en el panadapter o usar comandos CAT.

## Antes de comenzar

- Abra el diálogo AetherControl mediante **Settings > AetherControl...**

## Pasos

1. Haga clic en **External Spin** para activar o desactivar la animación.

Cuando está activada, arrastrar sobre el panadapter o cambiar la frecuencia desde una fuente externa activa una animación de giro de la rueda virtual. Cuando está desactivada, los cambios de frecuencia ocurren inmediatamente sin animación.

## Qué hace cada control

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Botón de alternancia | External Spin | Activa o desactiva la animación de giro en la rueda virtual cuando los cambios de frecuencia se originan fuera de la rueda. Clave de ajuste: `FlexControlVirtualExternalSpin` |
| Botón de alternancia | Reverse | Invierte la dirección de sintonización de la rueda. |
| Botón de alternancia | Compact | Alterna el modo compacto: oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz mínima. |
| Control deslizante | Wheel Tightness | Ajusta la resistencia de inercia de la rueda virtual; 0 = firme (detención rápida), 100 = suelto (inercia prolongada). Principalmente para trackpads; no afecta al FlexControl físico. Clave de ajuste: `FlexControlVirtualWheel` (JSON anidado, campo de holgura). |
| Control deslizante | Mouse Sensitivity | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. Clave de ajuste: `FlexControlVirtualWheel` (JSON anidado, campo de sensibilidad). |
| Cuadro combinado | Push (action) | Asigna una acción a la presión de la rueda (toque simple). Las opciones incluyen ciclo de modo, zoom por pasos, restablecer zoom, subir/bajar banda, RIT, XIT, volumen maestro, volumen de audio de la franja, volumen de auriculares, AGCT, APF y más. Clave de ajuste: `FlexControlButtonAction_*`. |
| Cuadro combinado | Double-tap (action) | Asigna una acción al doble toque en la rueda. |
| Botón pulsador | Aux buttons (1-5) | Cinco botones auxiliares configurables; etiquetados con puntos auxiliares para indicar la selección activa. |
| Cuadro combinado | Aux single-tap combo | Asigna una acción al toque simple en el botón auxiliar seleccionado. |
| Cuadro combinado | Aux double-tap combo | Asigna una acción al doble toque en el botón auxiliar seleccionado. |

## Indicadores

| Indicador | Significado |
|-----------|-------------|
| Wheel | Rueda virtual FlexControl que muestra la frecuencia y el modo de la franja activa. Gírela con el mouse o el tacto para sintonizar. |
| Physical | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Use los botones Detect/Close para gestionar el dispositivo físico. |

## Reconexión automática del dispositivo físico

El diálogo AetherControl se reconecta automáticamente a un dispositivo FlexControl físico cuando se desconecta y se vuelve a insertar, o cuando el puerto USB cambia durante una reconexión.

- Cuando la conexión del dispositivo se pierde (cable USB desconectado, dispositivo apagado o error de puerto), el diálogo muestra un estado de desconexión y comienza a reintentar automáticamente.
- Los reintentos comienzan en intervalos de 2 segundos y aumentan gradualmente hasta un máximo de 30 segundos entre intentos, de modo que un dispositivo que no regresa no inunda el registro.
- Cada reintento vuelve a detectar el dispositivo en lugar de reutilizar el nombre del puerto anterior, por lo que una renumeración USB que asigna un puerto diferente aún se recupera correctamente.
- Una vez que el dispositivo se detecta y se abre, el diálogo muestra el estado "Connected" y el temporizador de reintentos se restablece.

## Opciones de acciones de la rueda

Las siguientes acciones se pueden asignar a la presión de la rueda, al doble toque o a los toques de los botones auxiliares:

| ID de acción | Descripción |
|-----------|-------------|
| WheelRit | RIT (Sintonización incremental de recepción) |
| WheelXit | XIT (Sintonización incremental de transmisión) |
| WheelVolume | Volumen maestro |
| WheelSliceAudio | Volumen de audio de la franja |
| WheelHeadphoneVolume | Volumen de auriculares |
| WheelAgcT | AGCT (Umbral de control automático de ganancia) |
| WheelApf | APF (Filtro de pico de audio) |

## Notas

- **Área de desplazamiento**: El diálogo completo de AetherControl incluye un área de desplazamiento para su contenido. Cuando la altura del diálogo supera la altura disponible de la pantalla, el área de contenido se desplaza verticalmente. El tamaño mínimo de ventana en modo no compacto es de 430×610 píxeles, pero el diálogo se reducirá más en pantallas pequeñas manteniendo el acceso por desplazamiento a todos los controles.
- **Ajuste según la pantalla**: El diálogo se adapta a la altura disponible de la pantalla (excluyendo la barra de tareas) para evitar abrirse más alto que el espacio de trabajo. En modo compacto, el diálogo se redimensiona para ajustarse al diseño mínimo de solo rueda. En modo no compacto, el ancho mínimo sigue el ancho del contenido para evitar recortes horizontales.

## Relacionados

- [Usar la rueda virtual para sintonizar la franja activa](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Configurar el controlador de hardware AetherControl / FlexControl](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
