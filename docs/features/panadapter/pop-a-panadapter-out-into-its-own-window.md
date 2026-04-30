# Desacoplar un panadapter en su propia ventana

Cuando tiene más de un panadapter abierto, puede desacoplar cualquiera de ellos en una ventana flotante separada. Esto es útil para colocar el panadapter en un segundo monitor o cambiar su tamaño de forma independiente del diseño principal de AetherSDR.

## Antes de comenzar

- Conecte a una radio FLEX-8600. El botón de desacoplamiento solo está disponible cuando hay una conexión de radio activa.
- Abra al menos un panadapter adicional. En modo de un solo panadapter, el botón de desacoplamiento está oculto.

## Pasos

1. Localice la barra de título en la parte superior del panadapter que desea desacoplar. Muestra la etiqueta de slice (por ejemplo, **Slice A**) y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** en esa barra de título.

   El panadapter se desacopla en una ventana flotante sin marco.

3. Para mover la ventana flotante, haga clic y arrastre la tira de título en la parte superior de la ventana flotante.
4. Para cambiar el tamaño de la ventana flotante, arrastre el tirador de tamaño en su esquina inferior derecha.
5. Para acoplar la ventana nuevamente al diseño principal, haga clic en el botón **↩** en la barra de título de la ventana flotante.

## Qué hace cada control

| Control          | Descripción                                                                          | Predeterminado |
|------------------|--------------------------------------------------------------------------------------|---------|
| **⬈** (desacoplar)  | Desacopla el panadapter en una ventana flotante.                                      | —       |
| **↩** (acoplar)     | Devuelve el panadapter flotante al diseño principal.                                  | —       |
| **□** (maximizar) | Expande este panadapter para llenar el área principal.                                       | —       |
| **×** (cerrar)    | Cierra este panadapter.                                                              | —       |
| Título de slice      | Indicador que muestra qué slice está vinculado a este panadapter (Slice A a Slice H). | Slice A |

## Panel de decodificación CW

Cuando el panel de decodificación CW está abierto, aparece debajo del espectro y waterfall. El panel decodifica código Morse del audio de PC enrutado a AetherSDR.

> **Nota:** La decodificación CW requiere que el enrutamiento de audio de PC esté activo. Si no hay audio enrutado, el panel muestra la indicación **(requires PC Audio)**.

### Controles del panel de decodificación CW

| Control | Descripción | Predeterminado | Notas |
|---|---|---|---|
| **Etiqueta de estadísticas CW** | Muestra la altura de tono y velocidad detectadas, por ejemplo `750 Hz  20 WPM`. | — | Solo lectura; actualizado continuamente por el decodificador. |
| Regulador **Sens** | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. | 30 | Mapea el rango 0–100 a un umbral de costo de 1,0–0,1. Se guarda como `CwDecoderSensitivity`. |
| **🔒P** (Lock Pitch) | Bloquea la altura de tono del decodificador en la frecuencia sintonizada actual. | Desactivado | Alterna. |
| **🔒S** (Lock Speed) | Bloquea la velocidad del decodificador en la lectura actual de WPM. | Desactivado | Alterna. |
| Regulador **Lo** | Altura de tono mínima que busca el decodificador. Se limita a no ser mayor que **Hi**. | 500 Hz | Rango: 300–1200 Hz. |
| Regulador **Hi** | Altura de tono máxima que busca el decodificador. Se limita a no ser menor que **Lo**. | 700 Hz | Rango: 300–1200 Hz. |
| **CPY ALL** | Copia el texto decodificado completo al portapapeles. | — | — |
| **CPY VIS** | Copia solo el texto actualmente visible en el área de desplazamiento. | — | — |
| **CLR** | Borra el búfer de decodificación CW. | — | — |
| **✕** (cerrar CW) | Oculta el panel de decodificación CW. | — | — |
| **Texto de decodificación CW** | Pantalla rodante de solo lectura del CW decodificado, coloreada por confianza de decodificación. | — | Verde: costo < 0,15; Amarillo: costo < 0,35; Naranja: costo < 0,60; Rojo: costo ≥ 0,60. |

### Menú de contexto de texto de decodificación CW

Al hacer clic con el botón derecho dentro del área de **texto de decodificación CW** se abre un menú de contexto. El menú contiene las acciones de edición de texto estándar (Seleccionar todo, Copiar, etc.) seguidas de un separador y un elemento **Clear**. Al hacer clic en **Clear** en el menú de contexto, se produce el mismo efecto que al hacer clic en el botón **CLR**: vacía el búfer de decodificación inmediatamente.

## Consejos

- La ventana flotante no tiene marco. Use la tira de título dentro de la aplicación para arrastrarla y el tirador de tamaño en la esquina inferior derecha para cambiar su tamaño. No hay borde de ventana del sistema operativo.
- Las etiquetas del botón ⬈ e ↩ cambian para reflejar el estado actual: ⬈ cuando está acoplado, ↩ cuando está flotante.
- Utilice **Lo** e **Hi** juntos para delimitar el rango de altura de tono para la señal que está copiando. Reducir el rango disminuye las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Para borrar texto decodificado rápidamente, haga clic con el botón derecho en el área de texto de decodificación y seleccione **Clear** en lugar de llegar al botón **CLR**.

## Solución de problemas

- **El botón ⬈ no es visible** — Tiene solo un panadapter abierto. Los botones de desacoplamiento, maximización y cierre están todos ocultos en modo de un solo panadapter. Abra un panadapter adicional para que aparezcan.
- **La ventana flotante no se puede mover** — Haga clic y arrastre la tira de título dentro de la ventana flotante, no el área de espectro. El área de espectro se utiliza para sintonización.
- **El área de texto de decodificación CW no muestra texto** — Verifique que el audio de PC esté enrutado a AetherSDR. El panel muestra **(requires PC Audio)** cuando el audio no está disponible.

## Relacionado

- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo de múltiples slices)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](overview.md)
