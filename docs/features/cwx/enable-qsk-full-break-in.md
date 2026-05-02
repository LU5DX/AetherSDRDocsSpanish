# Activar QSK (ruptura total)

QSK (ruptura total o *full break-in*) permite que la radio reciba entre cada dit y dah mientras transmite en CW. Actívelo en la vista CWX Setup para que la radio cambie a recepción durante las pausas en el envío.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión de radio activa.
- Configure el slice activo en modo CW, CWL o CWU para que el panel CWX esté disponible.

## Pasos

1. Abra el panel CWX en la ventana principal.
2. Haga clic en **Setup** en la parte inferior del panel para cambiar a la vista Setup.
3. Haga clic en **QSK** para activarlo. El botón se resalta cuando está activo.

Para desactivar QSK, haga clic en **QSK** nuevamente.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---------|---------------|---------------------|----------------------|
| **QSK** | Activa o desactiva QSK (ruptura total). | Desactivado | `CwxQsk` |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | `CwxDelay` |

## Interacción entre Send y Live

En la versión v0.9.2.1, los botones **Send** y **Live** ya no funcionan como un grupo mutuamente excluyente simple. Su comportamiento depende del estado actual del panel:

- **Live** es un botón de alternancia. Haga clic una vez para activar el envío carácter a carácter en tiempo real; haga clic nuevamente para desactivarlo. El estado marcado del botón siempre refleja el estado *live* del modelo, incluso si dicho estado fue modificado externamente.
- **Send** se comporta de forma diferente según si **Live** está activo al momento de hacer clic:
  - Si **Live** está actualmente **desactivado**, al hacer clic en **Send** se envía el búfer escrito de inmediato.
  - Si **Live** está actualmente **activado**, al hacer clic en **Send** primero se desactiva el modo *live* y el panel vuelve a la vista de envío normal. El búfer **no** se retransmite, ya que es posible que algunos caracteres ya hayan sido enviados carácter a carácter.
- Hacer clic en **Setup** siempre desactiva el modo *live* antes de cambiar a la vista Setup.

## Temas relacionados

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en tiempo real](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
