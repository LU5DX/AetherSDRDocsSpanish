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

## Función de cada control

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---------|----------------|----------------|------------------------|
| **QSK** | Activa o desactiva QSK (full break-in). | Desactivado | `CwxQsk` |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | `CwxDelay` |

## Temas relacionados

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
