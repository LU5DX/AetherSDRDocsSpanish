# Habilitar Ventana Sin Marco

`View > Frameless Window` activa o desactiva el estilo de ventana sin marco personalizado para la ventana principal de AetherSDR. Cuando está habilitado, AetherSDR gestiona su propia barra de título, ofreciéndole una apariencia consistente en todos los entornos de escritorio y un control preciso sobre los bordes de la ventana.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- La ventana sin marco está activada de forma predeterminada en la versión 0.9.0. Si ha actualizado desde una versión anterior, se fuerza su activación automática una vez.

## Pasos

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Frameless Window`. Una marca de verificación junto al elemento indica que está activado.

Alternativamente, presione `Ctrl+Shift+F` para alternar la configuración sin abrir el menú.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave persistida |
|---|---|---|---|
| `View > Frameless Window` | Alterna `Qt::FramelessWindowHint` en la ventana principal. Cuando está activado, se eliminan las decoraciones nativas de la ventana del sistema operativo y se reemplazan por la barra de título personalizada de AetherSDR de 20 píxeles. | Activado | `FramelessWindow` |

**Cuando la ventana sin marco está activada:**

- Aparece una barra de título personalizada de 20 píxeles en la parte superior de la ventana. Arrástrela para mover la ventana.
- Haga doble clic en la barra de título para maximizar o restaurar la ventana.
- Los botones de minimizar, maximizar y cerrar aparecen en la barra de título.
- Aparece un asa de redimensionamiento en la esquina inferior derecha de la ventana.

**Cuando la ventana sin marco está desactivada:**

- Se restauran las decoraciones nativas de la ventana del sistema operativo.
- La barra de título personalizada y el asa de redimensionamiento de la esquina inferior derecha quedan ocultos.

## Consejos

- Si su entorno de escritorio o gestor de ventanas entra en conflicto con la barra de título personalizada de AetherSDR (por ejemplo, barras de título duplicadas o controles de ventana faltantes), desactive la ventana sin marco para volver a las decoraciones nativas.
- La configuración persiste entre reinicios mediante `FramelessWindow`.

## Solución de problemas

- **Dos barras de título visibles** — Su gestor de ventanas está dibujando su propia barra de título sobre la de AetherSDR. Vaya a `View > Frameless Window` y confirme que la marca de verificación esté presente. Si el problema persiste, revise la configuración de su gestor de ventanas para anular las decoraciones del lado del cliente.
- **La ventana no se puede mover ni redimensionar después de desactivar la ventana sin marco** — Es posible que la barra de título nativa aún no haya aparecido. Intente minimizar y restaurar la ventana para que el gestor de ventanas vuelva a dibujar sus decoraciones.

## Relacionados

- [Configure UI Scale](configure-ui-scale.md)
- [Enable Minimal Mode](enable-minimal-mode.md)
