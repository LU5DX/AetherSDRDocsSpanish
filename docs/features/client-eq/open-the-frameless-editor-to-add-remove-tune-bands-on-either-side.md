# Abrir el editor sin marco para agregar, eliminar y ajustar bandas en cada lado

El editor sin marco es donde se realiza todo el trabajo activo de ecualización: agregar y eliminar bandas, arrastrarlas a nuevas frecuencias y niveles de ganancia, ajustar Q, cambiar tipos de filtro y seleccionar una familia de filtros. Las fichas del applet son solo de visualización; esta ventana flotante es la superficie de edición.

## Antes de comenzar

- El contenedor padre Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa de ecualización TX o RX que desea editar debe existir en el widget CHAIN. Si la etapa aún no está en la cadena, agréguela primero desde allí.

## Pasos

1. Ubique el widget CHAIN del lado que desea editar (TX o RX).
2. Haga doble clic en la etapa de ecualización dentro del widget CHAIN de ese lado.
   - Hacer doble clic en la etapa TX EQ abre el editor con el título **Aetherial Parametric EQ — TX**.
   - Hacer doble clic en la etapa RX EQ abre el editor con el título **Aetherial Parametric EQ — RX**.
3. La ventana del editor sin marco aparece en su tamaño predeterminado (900 × 520 px). Su barra de título indica qué lado está activo.
4. Para **agregar una banda**, use la fila de iconos en la parte superior del área del lienzo. Haga clic en el icono del tipo de banda correspondiente para insertar una banda en una posición predeterminada.
5. Para **eliminar una banda**, selecciónela en el lienzo o en la fila de parámetros y use el control de eliminación de la fila de iconos.
6. Para **ajustar una banda**, arrástrela directamente sobre el lienzo:
   - Para bandas de pico y de shelving: arrastre para ajustar frecuencia y ganancia simultáneamente.
   - Para bandas HP/LP: arrastre para ajustar frecuencia y Q.
   - Mantenga presionado **Shift** mientras arrastra para ajustar solo Q.
   - Haga clic en el icono de una banda para recorrer los tipos de filtro disponibles.
7. Para cambiar la **familia de filtros** aplicada al cálculo en cascada HP/LP, abra el menú desplegable en la franja superior y seleccione una de las siguientes opciones: **Butterworth**, **Chebyshev**, **Bessel** o **Elliptic**.
8. Para congelar la traza de pico del analizador mientras ajusta, haga clic en **Peak Hold** en la franja de encabezado del editor. El botón se pone ámbar cuando está activo. Vuelva a hacer clic para reanudar la caída normal (~10 dB/sec).
9. Para descartar todas las ediciones y volver a los valores predeterminados, haga clic en **Reset**. Esto restaura el conteo predeterminado de 10 bandas y sus parámetros, y establece la familia de filtros nuevamente en Butterworth. El restablecimiento se guarda de inmediato.
10. Para cerrar el editor, use el botón de cierre en la barra de título sin marco del editor. Las fichas del applet continúan mostrando la curva sumada para cada lado correspondiente.

## Qué hace cada control

| Control | Función | Valor predeterminado |
|---|---|---|
| Lienzo (arrastrar — pico/shelf) | Ajusta la frecuencia y la ganancia de la banda seleccionada | Valores predeterminados por banda |
| Lienzo (arrastrar — HP/LP) | Ajusta la frecuencia y Q de la banda seleccionada | Valores predeterminados por banda |
| Lienzo (Shift + arrastrar) | Ajusta solo Q de la banda seleccionada | — |
| Icono de banda (clic) | Recorre los tipos de filtro disponibles para la banda seleccionada | — |
| Menú desplegable de familia de filtros | Establece la topología matemática para las cascadas HP/LP: Butterworth (banda de paso máximamente plana), Chebyshev (transición más pronunciada, rizado de 1 dB en la banda de paso), Bessel (fase lineal, caída más suave), Elliptic (transición más pronunciada, rizado en ambas bandas). Se conserva por ruta como `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. | Butterworth |
| Peak Hold | Congela la traza de pico por bin del analizador en su nivel máximo observado. Se encuentra en la franja de encabezado del editor. Se pone ámbar cuando está activado. Desactívelo para reanudar la caída normal (~10 dB/sec). Se aplica solo al editor flotante, no a la ficha del applet acoplado. | Desactivado |
| Reset | Restaura todas las bandas a sus valores predeterminados, restablece el conteo de bandas a las 10 bandas predeterminadas, establece la familia de filtros en Butterworth y guarda de inmediato. Información de herramienta: "Reset all bands to default values". Se encuentra en la franja de encabezado del editor. | — |
| Output Fader | Fader combinado vertical con medidor de nivel en el borde derecho del editor flotante. Arrastre para establecer la ganancia maestra post-ecualización; la rueda del ratón ajusta en pasos de 0.5 dB; doble clic restablece a 0 dB. La barra de nivel detrás del control muestra el pico post-ecualización suavizado en tiempo real con el mismo degradado verde-ámbar-rojo que el medidor de nivel Tube. Se conserva por separado según la ruta como `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. Rango: −36 a +12 dB. Se encuentra solo en el editor flotante, no en la ficha del applet acoplado. | 0 dB |

## Consejos

- El editor es una ventana única compartida que se reutiliza para ambos lados. Si se abre en el lado TX mientras ya muestra el lado RX, el título y el contenido cambian a TX. No es posible tener los editores TX y RX abiertos simultáneamente.
- Los cambios se guardan de inmediato a través del motor de audio. Cerrar el editor no descarta el trabajo no guardado.
- El bypass no se controla desde dentro del editor. Para activar o desactivar el bypass de una etapa de ecualización, use el gesto de clic simple del widget CHAIN sobre esa etapa.
- La traza de pico en la ficha del applet acoplado cae continuamente a ~10 dB/sec. El botón **Peak Hold** en el editor flotante congela la traza solo dentro de la vista del editor.

## Solución de problemas

- **Hacer doble clic en la etapa EQ no produce ningún resultado** — es posible que la etapa no esté completamente inicializada si no hay una conexión de radio activa. Conéctese a un FLEX-8600 e inténtelo de nuevo.
- **El botón Peak Hold permanece encendido después de dejar de usarlo** — haga clic en **Peak Hold** nuevamente para desactivarlo y reanudar la caída normal del analizador.

## Relacionados

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Desactivar la etapa EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Inspeccionar la curva TX EQ y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva RX EQ y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Verificar que la curva sumada coincide con el objetivo esperado](verify-the-summed-curve-matches-your-mental-target.md)
