# Cerrar un panadaptador adicional

Cuando tiene varios panadaptadores abiertos en un diseño de múltiples slices, puede cerrar cualquier adicional para recuperar espacio en pantalla. Esta página explica cómo cerrar un panadaptador que ya no necesita.

## Antes de comenzar

- Su radio debe estar conectado. El botón × (cerrar) solo está disponible cuando AetherSDR está conectado a un FLEX-8600.
- Debe tener más de un panadaptador abierto. El botón × (cerrar) está oculto en el modo de panadaptador único.

## Pasos

1. Localice la barra de título del panadaptador que desea cerrar. Está en la parte superior del panadaptador y muestra una etiqueta como "Slice A" o "Slice B".
2. Haga clic en el botón × en el extremo derecho de esa barra de título.

El panadaptador se cierra inmediatamente. Los panadaptadores restantes se expanden para llenar el espacio disponible.

## Consejos

- Si no puede ver el botón ×, está en modo de panadaptador único; solo hay un panadaptador abierto y no se permite cerrarlo.
- Si el panadaptador se ha extraído a una ventana flotante, el botón × permanece en la barra de título de la ventana flotante, en la esquina superior derecha. Haga clic allí.

## Solución de problemas

- **El botón × no es visible** — El radio está desconectado o solo hay un panadaptador abierto. AetherSDR oculta el botón × en ambos casos. Conéctese al radio y agregue un segundo panadaptador antes de intentarlo de nuevo.

## Menú contextual del texto de decodificación CW

Al hacer clic derecho en cualquier lugar del área de texto de decodificación CW, se abre un menú contextual. Además de los comandos de edición de texto estándar (Seleccionar todo, Copiar, etc.), el menú incluye un elemento **Clear**. Al elegir **Clear**, se borra todo el búfer de decodificación CW de inmediato. Esto equivale a hacer clic en el botón **CLR** en la barra de herramientas del panel CW.

## Coloración TX/RX de decodificación CW

En el panel de decodificación CW, el texto recibido y el texto transmitido (enviado por usted) se muestran en diferentes colores para que pueda distinguir su propio envío del CW entrante. Los colores son:

- **Verde**: Coste de confianza < 0.15 (alta confianza)
- **Amarillo**: Coste de confianza < 0.35
- **Naranja**: Coste de confianza < 0.60
- **Rojo**: Coste de confianza >= 0.60 (baja confianza)
- **Cian** (`#5fc8ff`): Texto decodificado de su propia transmisión

Al cambiar entre transmisión y recepción, se inserta automáticamente un espacio para evitar que las secuencias de texto coloreado se fusionen.

## Título del slice con Multi-Flex

En sesiones Multi-Flex, el título del slice que se muestra en la barra de título del panadaptador utiliza la letra de índice proporcionada por el radio, de modo que el título coincida con la insignia del slice. Esto garantiza la coherencia cuando varios clientes están conectados al mismo radio.

## Tema del panadaptador (v26.6.1)

En v26.6.1, el panadaptador y su panel de decodificación CW utilizan ahora estilos basados en temas en lugar de colores fijos. El degradado de la barra de título, los puntos de agarre de arrastre, el título del slice, las etiquetas de estadísticas y el fondo del panel CW hacen referencia a tokens de color del tema. Esto significa que el panadaptador se adapta automáticamente a temas claros y oscuros sin necesidad de anulaciones manuales de color. El sistema de temas reemplaza las hojas de estilo de color fijo anteriores con valores basados en tokens como `{{color.background.1}}`, `{{color.text.secondary}}` y `{{color.accent}}`.

## Relacionados

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
- [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md)
