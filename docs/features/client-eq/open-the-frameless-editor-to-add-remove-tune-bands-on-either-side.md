# Abrir el editor sin marco para agregar, eliminar y ajustar bandas en cualquier lado

El editor sin marco es donde se agregan, eliminan y ajustan las bandas de EQ individuales para la cadena TX o RX. Los mosaicos del applet muestran la curva resultante en modo de solo lectura; toda la edición ocurre en esta ventana flotante.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe ser visible en el panel de applets.
- La etapa de EQ del lado que desea editar (TX o RX) debe estar habilitada. Si aún no lo está, consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).

## Pasos

1. Localice el widget CHAIN dentro del contenedor Aetherial Audio (TXDSP).
2. Haga doble clic en la etapa de EQ del lado que desea editar — la etapa TX para abrir "Aetherial Parametric EQ — TX", o la etapa RX para abrir "Aetherial Parametric EQ — RX".
3. El editor sin marco se abre con su tamaño predeterminado (900 × 520 px). La barra de título muestra qué ruta está activa.
4. Para **agregar una banda**, haga clic en una ranura vacía en la fila de iconos ubicada en la parte superior del área del lienzo.
5. Para **eliminar una banda**, selecciónela en la fila de iconos o haciendo clic en su controlador en el lienzo, y luego use el control de eliminación en esa fila.
6. Para **ajustar una banda**:
   - Arrastre un nodo de pico o de shelving en el lienzo horizontalmente para ajustar la frecuencia, verticalmente para ajustar la ganancia.
   - Mantenga presionado Shift y arrastre para ajustar el Q.
   - Arrastre un nodo HP o LP horizontalmente para ajustar la frecuencia; arrastre verticalmente para ajustar el Q.
   - Haga clic en el icono de una banda para cambiar cíclicamente su tipo de filtro.
7. Para cambiar la familia de filtros utilizada en el cálculo en cascada HP/LP, seleccione una opción del menú desplegable en la franja superior derecha del editor: **Butterworth**, **Chebyshev**, **Bessel** o **Elliptic**.
8. Para cambiar a la otra ruta sin cerrar el editor, haga doble clic en la etapa de EQ opuesta en el widget CHAIN. El título y el contenido del editor se actualizan para reflejar la nueva ruta.
9. Cierre el editor haciendo clic en el botón de cierre de la barra de título del editor. La configuración de las bandas se guarda automáticamente en `ClientEqTxBands` o `ClientEqRxBands`.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| Lienzo | Pantalla interactiva de respuesta en frecuencia. Arrastre los nodos de banda para ajustar. | Objetivo de edición; el mosaico del applet es solo de visualización. |
| Fila de iconos | Un icono por banda. Haga clic para seleccionar o cambiar cíclicamente el tipo de filtro. | Se reconstruye al agregar o eliminar bandas. |
| Fila de parámetros | Lectura numérica e ingreso de valores para la frecuencia, ganancia y Q de la banda seleccionada. | Se actualiza en tiempo real durante los arrastres en el lienzo. |
| Menú desplegable de familia de filtros | Define el cálculo en cascada HP/LP para la ruta activa. Opciones: **Butterworth**, **Chebyshev**, **Bessel**, **Elliptic**. Predeterminado: Butterworth. | Se aplica solo a los tipos de banda HP y LP; los picos y shelves usan topología fija de segundo orden. |
| Fader de salida | Control deslizante vertical y medidor en el borde derecho. Establece la ganancia de salida maestra para la ruta activa. | Ajusta `setMasterGain` para el EQ vinculado; el valor se guarda al cambiar. |
| Barra de título | Muestra "Aetherial Parametric EQ — TX" o "— RX". Arrastre para mover la ventana. | Una instancia de editor compartida; el título cambia cuando se cambia la ruta. |

## Consejos

- El editor reutiliza una única instancia de ventana para ambas rutas. La etiqueta de la barra de título es el indicador confiable del lado que está editando en ese momento.
- El analizador FFT en tiempo real dentro del editor funciona a 25 Hz mientras el editor está abierto y se detiene automáticamente al cerrarlo.
- Las indicaciones de interacción impresas en la parte superior del editor ("Drag peak/shelf = freq + gain · drag HP/LP = freq + Q · Shift + drag for Q · click icon to cycle type") resumen los gestos del lienzo.

## Solución de problemas

- **El doble clic en la etapa de EQ no hace nada** — La etapa de EQ puede estar omitida o el contenedor Aetherial Audio puede no haberse cargado completamente. Verifique que la etapa esté habilitada mediante el widget CHAIN y vuelva a intentarlo.
- **Los cambios en las bandas no se escuchan** — Verifique que `ClientEqRxEnabled` o `ClientEqTxEnabled` esté activado para la ruta correspondiente. Una etapa omitida pasa el audio sin modificaciones independientemente de la configuración de las bandas.

## Relacionados

- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Inspeccionar la curva de EQ TX y el espectro en tiempo real](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ RX y el espectro en tiempo real](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Verificar que la curva sumada coincida con el objetivo previsto](verify-the-summed-curve-matches-your-mental-target.md)
