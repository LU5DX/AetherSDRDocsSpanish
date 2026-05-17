# Cerrar un panadapter adicional

Cuando tiene múltiples panadapters abiertos en un diseño de múltiples slices, puede cerrar cualquier panadapter adicional para recuperar espacio en pantalla. Esta página explica cómo cerrar un panadapter que ya no necesita.

## Antes de comenzar

- Su radio debe estar conectada. El botón × (cerrar) solo está disponible cuando AetherSDR está conectado a una FLEX-8600.
- Debe tener más de un panadapter abierto. El botón × (cerrar) está oculto en modo de un solo panel.

## Pasos

1. Localice la barra de título del panadapter que desea cerrar. Se encuentra en la parte superior del panadapter y muestra una etiqueta como "Slice A" o "Slice B".
2. Haga clic en el botón × en el extremo derecho de esa barra de título.

El panadapter se cierra de inmediato. Los panadapters restantes se expanden para llenar el espacio disponible.

## Consejos

- Si no puede ver el botón ×, está en modo de un solo panel — solo hay un panadapter abierto y no se permite cerrarlo.
- Si el panadapter ha sido extraído a una ventana flotante, el botón × aún está en la barra de título de la ventana flotante en la parte superior derecha. Haga clic allí.

## Solución de problemas

- **El botón × no es visible** — La radio está desconectada o solo hay un panadapter abierto. AetherSDR oculta el botón × en ambos casos. Conéctese a la radio y agregue un segundo panadapter antes de intentarlo nuevamente.

## Menú contextual del texto de decodificación CW

Al hacer clic con el botón derecho en cualquier lugar del área de texto de decodificación CW, se abre un menú contextual. Además de los comandos de edición de texto estándar (Seleccionar todo, Copiar, etc.), el menú incluye un elemento **Clear** (Borrar). Al elegir **Clear**, se borra todo el búfer de decodificación CW de inmediato. Esto es equivalente a hacer clic en el botón **CLR** en la barra de herramientas del panel CW.

## Colores de TX/RX en decodificación CW

En el panel de decodificación CW, el texto recibido y el texto transmitido (enviado por usted) se muestran en diferentes colores para que pueda distinguir su propia transmisión del CW entrante. Los colores son:

- **Verde**: Costo de confianza < 0.15 (alta confianza)
- **Amarillo**: Costo de confianza < 0.35
- **Naranja**: Costo de confianza < 0.60
- **Rojo**: Costo de confianza >= 0.60 (baja confianza)
- **Cian** (`#5fc8ff`): Texto decodificado de su propia transmisión con la llave

Al cambiar entre transmitir y recibir, se inserta automáticamente un espacio para evitar que las secuencias de texto coloreado se fusionen.

## Título del slice con Multi-Flex

En sesiones Multi-Flex, el título del slice que se muestra en la barra de título del panadapter utiliza la letra de índice proporcionada por la radio para que coincida con la insignia del slice. Esto garantiza consistencia cuando múltiples clientes están conectados a la misma radio.

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Haga clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Extraiga un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Maximice un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
