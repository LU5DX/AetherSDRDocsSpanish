# Activar QSK Full Break-in (Operación Ininterrumpida)

QSK (operación ininterrumpida) permite que la radio reciba entre cada punto y raya mientras transmite CW. Actívelo en la vista de configuración de CWX para que la radio cambie a recepción durante las pausas en su envío.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa con la radio.
- Configure la franja activa en modo CW, CWL o CWU para que el panel CWX esté disponible.

## Pasos

1. Abra el panel CWX en la ventana principal.
2. Haga clic en **Setup** en la parte inferior del panel para cambiar a la vista de configuración.
3. Haga clic en **QSK** para activarlo. El botón se resalta cuando está activo.

Para desactivar QSK, haga clic en **QSK** nuevamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---------|---------------|----------------------|------------------------|
| **QSK** | Activa o desactiva QSK (operación ininterrumpida). | Desactivado | `CwxQsk` |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | `CwxDelay` |

## Cómo interactúan Send y Live

En la versión 0.9.2.1, los botones **Send** y **Live** ya no actúan como un simple grupo mutuamente excluyente. Su comportamiento depende del estado actual del panel:

- **Live** es un conmutador. Haga clic una vez para habilitar la manipulación carácter por carácter en vivo; haga clic nuevamente para deshabilitarla. El estado marcado del botón siempre refleja el estado en vivo del modelo, incluso si el estado se cambió externamente.
- **Send** se comporta de manera diferente según si **Live** está activo al hacer clic:
  - Si **Live** está actualmente **desactivado**, al hacer clic en **Send** se envía el búfer escrito inmediatamente.
  - Si **Live** está actualmente **activado**, al hacer clic en **Send** primero se desactiva el modo en vivo y se devuelve el panel a la vista de envío normal. El búfer **no** se retransmite, porque algunos caracteres ya pueden haberse manipulado carácter por carácter.
- Al hacer clic en **Setup**, siempre se desactiva el modo en vivo antes de cambiar a la vista de configuración.

## Relacionado

- [Descripción general de CWX](overview.md)
- [Enviar un búfer de CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro de CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
