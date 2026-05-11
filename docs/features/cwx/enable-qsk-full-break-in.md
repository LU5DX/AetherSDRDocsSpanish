# Habilitar QSK (Operación en Modo Intermitente Completo)

QSK (operación en modo intermitente completo) permite que la radio reciba entre cada punto y raya mientras transmite CW. Actívelo en la vista de configuración de CWX para que la radio cambie a recepción durante las pausas en su envío.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa con la radio.
- Configure la franja activa en modo CW, CWL o CWU para que el panel CWX esté disponible.

## Pasos

1. Abra el panel CWX en la ventana principal.
2. Haga clic en **Setup** en la parte inferior del panel para cambiar a la vista de configuración.
3. Haga clic en **QSK** para activarlo. El botón se resalta cuando está activo.

Para desactivar QSK, haga clic en **QSK** nuevamente.

## Funciones de cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---------|----------------|----------------------|------------------------|
| **QSK** | Activa o desactiva QSK (operación en modo intermitente completo). | Desactivado | `CwxQsk` |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | `CwxDelay` |
| **Speed:** | Velocidad CW en WPM. | 20 | `CwxSpeedWpm` |
| **Send (vista)** | Cambia al área de envío en vivo con historial y campo de texto. | – | – |
| **Live (vista)** | Cambia a la vista de envío en vivo. | – | – |
| **Setup (vista)** | Cambia al editor de macros y configuración QSK. | – | – |
| **Desplazamiento del historial de envío** | Muestra búferes de envío anteriores con resaltado de caracteres. | – | – |
| **Área de texto de envío** | Escriba caracteres CW; Enter envía el búfer. | – | – |
| **F1 … F12 (macros)** | Envía la macro preescrita para esa tecla de función. | – | `CwxMacro_F1..F12` |
| **F1 … F12 editores de macros** | Editores en la vista de configuración para cada macro. | – | `CwxMacro_F1..F12` |
| **Leyenda de prosignos** | Muestra accesos directos para prosignos CW comunes (=, +, (, &, $). | – | – |

## Cómo interactúan Enviar y En Vivo

En la versión v0.9.2.1, los botones **Send** y **Live** ya no actúan como un grupo mutuamente excluyente simple. Su comportamiento depende del estado actual del panel:

- **Live** es un botón de alternancia. Haga clic una vez para activar el tecleo carácter por carácter en vivo; haga clic nuevamente para desactivarlo. El estado marcado del botón siempre refleja el estado en vivo del modelo, incluso si el estado fue cambiado externamente.
- **Send** se comporta de manera diferente dependiendo de si **Live** está activo cuando hace clic en él:
  - Si **Live** está actualmente **desactivado**, al hacer clic en **Send** se envía el búfer escrito inmediatamente.
  - Si **Live** está actualmente **activado**, al hacer clic en **Send** primero se desactiva el modo en vivo y se devuelve el panel a la vista normal de envío. El búfer **no** se retransmite, porque algunos caracteres ya pueden haber sido tecleados carácter por carácter.
- Al hacer clic en **Setup** siempre se desactiva el modo en vivo antes de cambiar a la vista de configuración.

## Comportamiento de las teclas F1–F12 y Escape

Las teclas de función F1–F12 y la tecla **Escape** están disponibles como accesos directos de toda la aplicación solo cuando el panel CWX está visible. Esto evita conflictos de accesos directos con el panel DVK (Teclado de Voz Digital), que registra su propio conjunto de accesos directos F1–F12 cuando está visible.

- Mientras el panel CWX está visible: F1–F12 activan las macros CW correspondientes, y **Escape** limpia el búfer de envío.
- Mientras el panel CWX está oculto (y el panel DVK está visible en su lugar): F1–F12 activan las macros DVK.
- Los accesos directos se habilitan automáticamente cuando se muestra el panel CWX y se deshabilitan cuando se oculta.

## Relacionados

- [Visión general de CWX](overview.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1-F12](trigger-a-cw-macro-with-f1-f12.md)
