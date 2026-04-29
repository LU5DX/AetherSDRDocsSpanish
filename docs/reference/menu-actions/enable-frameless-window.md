# Activar la ventana sin bordes

`View > Frameless Window` activa o desactiva el estilo de ventana sin bordes personalizado para la ventana principal de AetherSDR. Cuando está activado, AetherSDR gestiona su propia barra de título, lo que proporciona una apariencia uniforme en todos los entornos de escritorio y un control preciso sobre los elementos decorativos de la ventana.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Frameless Window está activado de forma predeterminada en la versión v0.9.0. Si actualizó desde una versión anterior, se fuerza su activación una vez de manera automática.

## Pasos

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Frameless Window`. Una marca de verificación junto al elemento indica que está activado.

Como alternativa, presione `Ctrl+Shift+F` para alternar la configuración sin abrir el menú.

## Qué hace cada control

| Control | Descripción | Predeterminado | Clave persistente |
|---|---|---|---|
| `View > Frameless Window` | Activa o desactiva `Qt::FramelessWindowHint` en la ventana principal. Cuando está activado, se eliminan las decoraciones nativas del sistema operativo y se reemplazan por la barra de título propia de AetherSDR de 20px. | Activado | `FramelessWindow` |

**Cuando Frameless Window está activado:**

- Aparece una barra de título personalizada de 20px en la parte superior de la ventana. Arrástrela para mover la ventana.
- Haga doble clic en la barra de título para maximizar o restaurar la ventana.
- Los botones de minimizar, maximizar y cerrar aparecen en la barra de título.
- Aparece un control de cambio de tamaño en la esquina inferior derecha de la ventana.

**Cuando Frameless Window está desactivado:**

- Se restauran las decoraciones nativas del sistema operativo.
- La barra de título personalizada y el control de cambio de tamaño de la esquina inferior derecha quedan ocultos.

## Consejos

- Si su entorno de escritorio o gestor de ventanas entra en conflicto con la barra de título personalizada de AetherSDR (por ejemplo, barras de título duplicadas o controles de ventana faltantes), desactive Frameless Window para volver a las decoraciones nativas.
- La configuración persiste entre reinicios mediante `FramelessWindow`.

## Solución de problemas

- **Dos barras de título visibles** — Su gestor de ventanas está dibujando su propia barra de título sobre la de AetherSDR. Vaya a `View > Frameless Window` y confirme que la marca de verificación esté presente. Si el problema persiste, revise la configuración de su gestor de ventanas para la opción de anular las decoraciones del lado del cliente.
- **La ventana no se puede mover ni redimensionar tras desactivar Frameless Window** — Es posible que la barra de título nativa aún no haya aparecido. Intente minimizar y restaurar la ventana para que el gestor de ventanas vuelva a dibujar sus decoraciones.

## Relacionados

- [Configurar la escala de la interfaz](configure-ui-scale.md)
- [Activar el modo mínimo](enable-minimal-mode.md)
