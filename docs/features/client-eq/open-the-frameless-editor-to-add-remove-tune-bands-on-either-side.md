# Abrir el editor sin marco para agregar, eliminar y ajustar bandas en cualquier lado

El editor sin marco es donde se realiza todo el trabajo activo de ecualización: agregar y eliminar bandas, arrastrarlas a nuevas frecuencias y ganancias, ajustar la Q, cambiar tipos de filtro y seleccionar una familia de filtros. Los mosaicos del applet son solo de visualización; esta ventana flotante es la superficie de edición.

## Antes de comenzar

- El contenedor principal de Aetherial Audio (TXDSP) debe estar visible en el panel del applet.
- La etapa de ecualización TX o RX que desea editar debe existir en el widget CHAIN. Si la etapa aún no está en la cadena, agréguela allí primero.

## Pasos

1. Localice el widget CHAIN para el lado que desea editar (TX o RX).
2. Haga doble clic en la etapa de EQ en el widget CHAIN para ese lado.
   - Hacer doble clic en la etapa de EQ de TX abre el editor con el título **Aetherial Parametric EQ — TX**.
   - Hacer doble clic en la etapa de EQ de RX abre el editor con el título **Aetherial Parametric EQ — RX**.
3. La ventana del editor sin marco aparece con su tamaño predeterminado (900 × 520 px). Su barra de título indica qué lado está activo.
4. Para **agregar una banda**, utilice la fila de iconos en la parte superior del área del lienzo. Haga clic en el icono del tipo de banda correspondiente para insertar una banda en una posición predeterminada.
5. Para **eliminar una banda**, selecciónela en el lienzo o en la fila de parámetros y utilice el control de eliminación en la fila de iconos.
6. Para **ajustar una banda**, arrástrela directamente sobre el lienzo:
   - Para bandas de pico y shelf: arrastre para ajustar la frecuencia y la ganancia simultáneamente.
   - Para bandas HP/LP: arrastre para ajustar la frecuencia y la Q.
   - Mantenga presionado **Shift** mientras arrastra para ajustar únicamente la Q.
   - Haga clic en el icono de una banda para recorrer los tipos de filtro disponibles.
7. Para cambiar la **familia de filtros** aplicada al cálculo en cascada HP/LP, abra el menú desplegable en la franja superior y seleccione una de las siguientes opciones: **Butterworth**, **Chebyshev**, **Bessel** o **Elliptic**.
8. Para congelar la traza de pico del analizador mientras ajusta, haga clic en **Peak Hold**. Haga clic nuevamente para reanudar la caída normal.
9. Para descartar todas las ediciones y volver a los valores predeterminados, haga clic en **Reset**. Esto restaura el número de bandas y los parámetros predeterminados, y restablece la familia de filtros a Butterworth. El restablecimiento se guarda de inmediato.
10. Para cerrar el editor, utilice el botón de cierre en la barra de título sin marco del editor. Los mosaicos del applet continúan mostrando la curva sumada para sus respectivos lados.

## Qué hace cada control

| Control | Función | Valor predeterminado | Clave de persistencia |
|---|---|---|---|
| Lienzo (arrastrar — pico/shelf) | Ajusta la frecuencia y la ganancia de la banda seleccionada | Valores predeterminados por banda | `ClientEqRxBands` / `ClientEqTxBands` |
| Lienzo (arrastrar — HP/LP) | Ajusta la frecuencia y la Q de la banda seleccionada | Valores predeterminados por banda | `ClientEqRxBands` / `ClientEqTxBands` |
| Lienzo (Shift + arrastrar) | Ajusta únicamente la Q de la banda seleccionada | — | `ClientEqRxBands` / `ClientEqTxBands` |
| Icono de banda (clic) | Recorre los tipos de filtro disponibles para la banda seleccionada | — | `ClientEqRxBands` / `ClientEqTxBands` |
| Menú desplegable de familia de filtros | Establece la topología matemática para las cascadas HP/LP: Butterworth (banda de paso maximalmente plana), Chebyshev (transición más pronunciada, rizado de 1 dB en la banda de paso), Bessel (fase lineal, caída más suave), Elliptic (transición más pronunciada, rizado en ambas bandas) | Butterworth | `ClientEqRxBands` / `ClientEqTxBands` |
| Peak Hold | Congela la traza de pico por bin del analizador en el nivel máximo observado | Desactivado (sin marcar) | — |
| Reset | Restaura todas las bandas a sus valores predeterminados, restablece el número de bandas al valor predeterminado, establece la familia de filtros en Butterworth y guarda de inmediato | — | `ClientEqRxBands` / `ClientEqTxBands` |

## Consejos

- El editor es una única ventana compartida que se reutiliza para ambos lados. Si lo abre en el lado TX mientras ya muestra el lado RX, el título y el contenido cambian a TX. No es posible tener los editores de TX y RX abiertos simultáneamente.
- Los cambios se guardan de inmediato a través del motor de audio. Cerrar el editor no descarta el trabajo no guardado.
- El bypass no se controla desde el interior del editor. Para habilitar o poner en bypass una etapa de EQ, utilice el gesto de clic simple del widget CHAIN sobre esa etapa.

## Solución de problemas

- **Hacer doble clic en la etapa de EQ no tiene efecto** — es posible que la etapa no esté completamente inicializada si no hay una conexión de radio activa. Conéctese a un FLEX-8600 e inténtelo de nuevo.
- **El botón Peak Hold permanece encendido después de dejar de usarlo** — haga clic en **Peak Hold** nuevamente para desmarcarlo y reanudar la caída normal del analizador.

## Temas relacionados

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Inspeccionar la curva de EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
