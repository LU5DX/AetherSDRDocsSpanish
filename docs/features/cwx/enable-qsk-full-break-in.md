# Activar QSK (Full Break-in)

QSK (full break-in) permite que el radio reciba entre cada dit y dah mientras transmite en CW. Actívelo en la vista CWX Setup para que el radio cambie a recepción durante las pausas en el envío.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El panel CWX requiere una conexión de radio activa.
- Configure el slice activo en modo CW, CWL o CWU para que el panel CWX esté disponible.

## Pasos

1. Abra el panel CWX en la ventana principal.
2. Haga clic en **Setup** en la parte inferior del panel para cambiar a la vista Setup.
3. Haga clic en **QSK** para activarlo. El botón se resalta cuando está activo.

Para desactivar QSK, haga clic en **QSK** nuevamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---------|----------------|----------------------|------------------------|
| **QSK** | Activa o desactiva QSK (full break-in). | Desactivado | `CwxQsk` |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | `CwxDelay` |

## Cómo interactúan Send y Live

En la versión v0.9.2.1, los botones **Send** y **Live** ya no funcionan como un grupo mutuamente excluyente simple. Su comportamiento depende del estado actual del panel:

- **Live** es un conmutador. Haga clic una vez para activar el tecleo carácter por carácter en tiempo real; haga clic nuevamente para desactivarlo. El estado marcado del botón siempre refleja el estado live del modelo, incluso si el estado fue modificado externamente.
- **Send** se comporta de manera diferente según si **Live** está activo al momento de hacer clic:
  - Si **Live** está actualmente **desactivado**, hacer clic en **Send** envía el búfer escrito de inmediato.
  - Si **Live** está actualmente **activado**, hacer clic en **Send** primero desactiva el modo live y regresa el panel a la vista de envío normal. El búfer **no** se retransmite, ya que es posible que algunos caracteres ya hayan sido enviados carácter por carácter.
- Hacer clic en **Setup** siempre desactiva el modo live antes de cambiar a la vista Setup.

## Relacionados

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en tiempo real](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
