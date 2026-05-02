# Abrir el editor sin marco para agregar / quitar / ajustar bandas en cada lado

El editor sin marco es donde se realiza todo el trabajo activo de EQ: agregar y quitar bandas, arrastrarlas a nuevas frecuencias y ganancias, ajustar Q, cambiar tipos de filtro y seleccionar una familia de filtros. Las fichas de applet son solo de visualización; esta ventana flotante es la superficie de edición.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa de EQ TX o RX que desea editar debe existir en el widget CHAIN. Si la etapa aún no está en la cadena, agréguela primero desde allí.

## Pasos

1. Localice el widget CHAIN del lado que desea editar (TX o RX).
2. Haga doble clic en la etapa de EQ en el widget CHAIN de ese lado.
   - Al hacer doble clic en la etapa TX EQ se abre el editor con el título **Aetherial Parametric EQ — TX**.
   - Al hacer doble clic en la etapa RX EQ se abre el editor con el título **Aetherial Parametric EQ — RX**.
3. La ventana del editor sin marco aparece en su tamaño predeterminado (900 × 520 px). Su barra de título muestra qué lado está activo.
4. Para **agregar una banda**, utilice la fila de iconos en la parte superior del área del lienzo. Haga clic en el icono del tipo de banda correspondiente para insertar una banda en una posición predeterminada.
5. Para **quitar una banda**, selecciónela en el lienzo o en la fila de parámetros y use el control de eliminar en la fila de iconos.
6. Para **ajustar una banda**, arrástrela directamente sobre el lienzo:
   - Para bandas peak y shelf: arrastre para ajustar frecuencia y ganancia simultáneamente.
   - Para bandas HP/LP: arrastre para ajustar frecuencia y Q.
   - Mantenga presionado **Shift** mientras arrastra para ajustar solo Q.
   - Haga clic en el icono de una banda para recorrer los tipos de filtro disponibles.
7. Para cambiar la **familia de filtros** aplicada al cálculo matemático en cascada HP/LP, abra el menú desplegable en la franja superior y seleccione una de las opciones: **Butterworth**, **Chebyshev**, **Bessel** o **Elliptic**.
8. Para congelar la traza de pico del analizador durante el ajuste, haga clic en **Peak Hold** en la franja de encabezado del editor. El botón se vuelve ámbar cuando está activo. Haga clic de nuevo para reanudar la caída normal (~10 dB/seg).
9. Para descartar todas las ediciones y volver a los valores predeterminados, haga clic en **Reset**. Esto restaura el recuento y los parámetros predeterminados de 10 bandas y restablece la familia de filtros a Butterworth. El restablecimiento se guarda inmediatamente.
10. Para cerrar el editor, use el botón de cierre en la barra de título sin marco del editor. Las fichas de applet continúan mostrando la curva sumada para cada uno de sus lados respectivos.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado |
|---|---|---|
| Lienzo (arrastrar — peak/shelf) | Ajusta la frecuencia y la ganancia de la banda seleccionada | Predeterminados por banda |
| Lienzo (arrastrar — HP/LP) | Ajusta la frecuencia y Q de la banda seleccionada | Predeterminados por banda |
| Lienzo (Shift + arrastrar) | Ajusta solo Q de la banda seleccionada | — |
| Icono de banda (clic) | Recorre la banda seleccionada por los tipos de filtro disponibles | — |
| Menú desplegable de familia de filtros | Establece la topología matemática para las cascadas HP/LP: Butterworth (banda de paso máximamente plana), Chebyshev (transición más pronunciada, rizado de banda de paso de 1 dB), Bessel (fase lineal, caída más suave), Elliptic (transición más pronunciada, rizado en ambas bandas). Se guarda por ruta como `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. | Butterworth |
| Peak Hold | Congela la traza de retención de pico por bin del analizador en su nivel máximo observado. Se encuentra en la franja de encabezado del editor. Se vuelve ámbar cuando está activado. Desactívelo para reanudar la caída normal (~10 dB/seg). Se aplica solo al editor flotante, no a la ficha de applet acoplada. | Off (desactivado) |
| Reset | Restaura todas las bandas a sus valores predeterminados, restablece el recuento de bandas a las 10 bandas predeterminadas, establece la familia de filtros en Butterworth y guarda inmediatamente. Información de herramienta: "Reset all bands to default values". Se encuentra en la franja de encabezado del editor. | — |
| Output Fader | Fader combinado vertical con medidor de nivel en el borde derecho del editor flotante. Arrastre para establecer la ganancia maestra post-EQ; la rueda de desplazamiento ajusta en pasos de 0.5 dB; haga doble clic para restablecer a 0 dB. La barra de nivel detrás del controlador muestra el pico post-EQ suavizado en tiempo real con el mismo gradiente verde-ámbar-rojo que el medidor de nivel Tube. Se guarda por separado por ruta como `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. Rango: −36 a +12 dB. Se encuentra solo en el editor flotante, no en la ficha de applet acoplada. | 0 dB |
| Smoothing | Aplica promediado de potencia por fracción de octava a la traza del analizador para su visualización — no afecta el cálculo matemático del EQ. Fracción más baja = más suavizado (1/3 es el más suavizado; 1/96 es efectivamente desactivado). El suavizado se aplica después de la actualización de retención de pico en cada fotograma, por lo que tanto la traza en vivo del analizador como la traza de retención de pico se suavizan para su visualización. Compartido entre los editores TX y RX. Se guarda como `ClientEqSmoothingFraction`. Información de herramienta: "Fractional-octave smoothing applied to the analyzer trace. Lower fraction = smoother (1/3 = most, 1/96 = off). Affects display only — EQ math is unchanged." Se encuentra en la franja de encabezado del editor (solo en el editor flotante). | Off (1/96) |
| Fila de iconos de tipo de filtro | Una fila de 8 iconos dibujados de forma personalizada (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana peak, rampa shelf, pendiente HP/LP) en el color de paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro de esa banda; al hacer clic también se selecciona la banda, resaltando su controlador en el lienzo y su columna en la fila de parámetros. Se encuentra solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está en bypass. | — |
| Fila de texto de parámetros | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores de Freq, Gain y Q de cada banda. Los valores se actualizan en tiempo real durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. Se encuentra solo en el editor flotante. | — |
| Líneas guía de corte de filtro (TX / RX) | Líneas verticales amarillas discontinuas superpuestas en el lienzo en los cortes de filtro TX bajo/alto actuales de la radio (ficha TX) o los bordes de la banda de paso RX (ficha RX). Estas líneas se actualizan automáticamente cada vez que la radio reporta un cambio de filtro. Al acercar el cursor a una línea, este cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real. | — |

## Consejos

- El editor es una única ventana compartida que se reutiliza para ambos lados. Si lo abre en el lado TX mientras ya muestra el lado RX, su título y contenido cambian a TX. No es posible tener los editores TX y RX abiertos simultáneamente.
- Los cambios se guardan inmediatamente a través del motor de audio. Cerrar el editor no descarta el trabajo no guardado.
- El bypass no se controla desde dentro del editor. Para activar o poner en bypass una etapa de EQ, use el gesto de clic simple del widget CHAIN sobre esa etapa.
- La traza de retención de pico en la ficha de applet acoplada cae continuamente a ~10 dB/seg. El botón **Peak Hold** en el editor flotante congela la traza solo dentro de la vista del editor.
- Las líneas guía de corte de filtro amarillas discontinuas visibles tanto en la ficha de applet acoplada como en el editor flotante se actualizan en tiempo real cada vez que la radio cambia su banda de paso TX o RX, manteniendo la referencia visual siempre actualizada.
- El suavizado de visualización (configurado con el combo **Smoothing**) se aplica después de cada actualización de retención de pico. La propia traza de retención de pico siempre rastrea los bins sin procesar para una detección precisa de picos; la versión suavizada es solo para visualización.

## Solución de problemas

- **Al hacer doble clic en la etapa de EQ no ocurre nada** — es posible que la etapa no esté completamente inicializada si no hay una conexión de radio activa. Conéctese a un FLEX-8600 e inténtelo de nuevo.
- **El botón Peak Hold permanece encendido después de dejar de usarlo** — haga clic en **Peak Hold** de nuevo para desactivarlo y reanudar la caída normal del analizador.
- **Las líneas guía de corte de filtro no aparecen** — si la radio reporta un valor de corte de 0 para alguno de los bordes, esa línea guía se suprime. Verifique que la radio tenga un modo activo y un slice seleccionado.

## Relacionado

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Inspeccionar la curva TX EQ y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva RX EQ y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Verificar que la curva sumada coincida con el objetivo previsto](verify-the-summed-curve-matches-your-mental-target.md)
<!-- docmesh:llm version=V0.9.5.1 date=2026-05-01 -->
