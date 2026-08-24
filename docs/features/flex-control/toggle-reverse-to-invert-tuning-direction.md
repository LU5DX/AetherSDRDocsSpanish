# Configuración de AetherControl / FlexControl

Esta página describe el diálogo de AetherControl / FlexControl, que configura el controlador rotatorio físico y la rueda de sintonización virtual en pantalla.

## Abrir el diálogo

1. Abra el menú **Settings**.
2. Haga clic en **AetherControl...**.

## Conexión física del FlexControl

El indicador **Physical** muestra si un dispositivo FlexControl está conectado y qué puerto serie utiliza.

- Haga clic en **Detect** para buscar un FlexControl conectado.
- Haga clic en **Close** para desconectar el dispositivo físico.

Si el dispositivo físico se desconecta, AetherSDR reintenta la conexión automáticamente. El intervalo de reintento comienza en 2 segundos y aumenta hasta un máximo de 30 segundos si el dispositivo no reaparece. Cuando el dispositivo se vuelve a conectar, es posible que se le asigne un puerto serie diferente; AetherSDR vuelve a detectar el puerto automáticamente.

## Rueda virtual

La **Wheel** es un control rotatorio virtual. Gírela con el ratón o el trackpad para sintonizar el slice activo. Muestra la frecuencia actual y la lectura del modo.

| Control | Etiqueta | Comportamiento | Clave de configuración |
|---------|----------|----------------|------------------------|
| Indicador | **Wheel** | Control rotatorio virtual para sintonizar el slice activo. Muestra frecuencia y modo. | — |
| Botón de alternancia | **Compact** | Oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz minimalista. | — |
| Botón de alternancia | **External Spin** | Habilita gestos de giro de rueda al arrastrar sobre el panadapter. | — |
| Botón de alternancia | **Reverse** | Invierte la dirección de sintonización de la rueda. | `FlexControlInvertDir` |
| Control deslizante | **Wheel Tightness** | Ajusta el arrastre de inercia de la rueda virtual. 0 = firme (detención rápida), 100 = suelto (inercia larga). Principalmente para trackpads; no afecta al FlexControl físico. | `FlexControlVirtualWheel` (JSON anidado, campo `looseness`) |
| Control deslizante | **Mouse Sensitivity** | Ajusta cuánto movimiento capturado del ratón/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity`) |

### Notas sobre Wheel Tightness

- El control deslizante **Wheel Tightness** reemplaza al antiguo control *Spin Sensitivity* (v26.5.3).
- El ajuste se almacena como parte de un objeto JSON anidado bajo `FlexControlVirtualWheel`. La clave plana anterior `FlexControlVirtualWheelLooseness` se migra automáticamente al leerla.

### Notas sobre Mouse Sensitivity

- Introducido en v26.5.3.
- Los deltas del puntero se limitan a 15° (π/12) por evento para evitar saltos.
- Re-anclaje diferido: cuando el puntero cruza la zona muerta central, el ancla se elimina; el siguiente movimiento re-ancla sin calcular un delta.

## Acciones de la rueda

Asigne acciones al presionar y al hacer doble clic en la rueda.

| Control | Etiqueta | Comportamiento | Clave de configuración |
|---------|----------|----------------|------------------------|
| Cuadro combinado | **Push (action)** | Asigna una acción al presionar la rueda (un solo toque). Las opciones incluyen ciclo de modo, zoom por pasos, restablecer zoom, banda arriba/abajo y más. | `FlexControlButtonAction_*` |
| Cuadro combinado | **Double-tap (action)** | Asigna una acción al hacer doble toque en la rueda. | — |

## Botones auxiliares

Cinco botones auxiliares configurables (1–5) se encuentran debajo de la rueda. Cada botón tiene su propia acción de toque simple y doble toque.

1. Haga clic en un botón auxiliar para seleccionarlo. El botón se resalta con un punto auxiliar.
2. Elija la acción **Aux single-tap** en el cuadro combinado.
3. Elija la acción **Aux double-tap** en el cuadro combinado.

| Control | Etiqueta | Comportamiento | Clave de configuración |
|---------|----------|----------------|------------------------|
| Grupo de botones | **Aux buttons (1-5)** | Cinco botones configurables, cada uno con acciones de toque simple y doble toque. | — |
| Cuadro combinado | **Aux single-tap** | Asigna una acción al toque simple del botón auxiliar seleccionado. | — |
| Cuadro combinado | **Aux double-tap** | Asigna una acción al doble toque del botón auxiliar seleccionado. | — |

## Relacionados

- [Invertir la dirección de sintonización en el AetherControl](reverse-tuning-direction-on-the-aethercontrol.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Ajustar la sensibilidad del ratón para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Ajustar la firmeza de la rueda virtual](adjust-wheel-tightness-for-the-virtual-wheel.md)
