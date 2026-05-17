# Habilitar QSK (Operación Full Break-in)

QSK (operación full break-in) permite que la radio reciba entre cada punto y raya al transmitir en CW. Actívelo en la vista de configuración de CWX para que la radio cambie a recepción durante las pausas en su envío.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión de radio activa.
- Configure la banda activa (slice) en modo CW, CWL o CWU para que el panel CWX esté disponible.

## Pasos

1. Abra el panel CWX en la ventana principal.
2. Haga clic en **Setup** en la parte inferior del panel para cambiar a la vista de configuración.
3. Haga clic en **QSK** para activarlo. El botón se resalta cuando está activo.

Para desactivar QSK, haga clic en **QSK** nuevamente.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---------|--------------|---------------------|------------------------|
| **QSK** | Activa o desactiva QSK (full break-in). | Desactivado | `CwxQsk` |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | `CwxDelay` |
| **Speed:** | Velocidad CW en WPM. | 20 | `CwxSpeedWpm` |
| **Send (vista)** | Cambia al área de envío en vivo con historial y campo de texto. | – | – |
| **Live (vista)** | Cambia a la vista de envío en vivo. | – | – |
| **Setup (vista)** | Cambia al editor de macros y configuración QSK. | – | – |
| **Desplazamiento de historial de envío** | Muestra búferes de envío anteriores con resaltado de caracteres. | – | – |
| **Área de texto de envío** | Escriba caracteres CW; Enter envía el búfer. | – | – |
| **F1 … F12 (macros)** | Envía la macro preescrita para esa tecla de función. | – | `CwxMacro_F1..F12` |
| **F1 … F12 editores de macros** | Editores de la vista de configuración para cada macro. | – | `CwxMacro_F1..F12` |
| **Leyenda de prosignos** | Muestra accesos directos para prosignos CW comunes (=, +, (, &, $). | – | – |

## Cómo interactúan Send y Live

En la versión v26.5.2.1, los botones **Send** y **Live** ya no actúan como un grupo mutuamente excluyente simple. Su comportamiento depende del estado actual del panel:

- **Live** es un conmutador. Haga clic una vez para habilitar la activación carácter por carácter en vivo; haga clic de nuevo para deshabilitarla. El estado marcado del botón siempre refleja el estado en vivo del modelo, incluso si el estado se cambió externamente.
- **Send** se comporta de manera diferente según si **Live** está activo al hacer clic:
  - Si **Live** está actualmente **desactivado**, hacer clic en **Send** envía el búfer escrito de inmediato.
  - Si **Live** está actualmente **activado**, hacer clic en **Send** primero desactiva el modo en vivo y devuelve el panel a la vista de envío normal. El búfer **no** se retransmite, porque algunos caracteres ya pueden haberse activado carácter por carácter.
- Hacer clic en **Setup** siempre desactiva el modo en vivo antes de cambiar a la vista de configuración.

## Menú contextual de burbujas de historial

Cada mensaje enviado aparece como una burbuja de historial en el área de **desplazamiento de historial de envío**. Haga clic derecho en cualquier burbuja para abrir un menú contextual con las siguientes acciones:

- **Resend** — Envía el mensaje seleccionado nuevamente y agrega una nueva burbuja de historial con la marca de tiempo actual.
- **Clear History** — Elimina todas las burbujas de historial del área de desplazamiento.

## Comportamiento de F1–F12 y la tecla Escape

Las teclas de función F1–F12 y la tecla **Escape** están disponibles como accesos directos en toda la aplicación. Los accesos directos se habilitan o deshabilitan según el modo de la banda activa (slice), no por la visibilidad del panel. Esto garantiza que las teclas funcionen tanto si el panel CWX está visible como si no, evitando conflictos con el panel DVK (Digital Voice Keyer).

- Cuando la banda activa está en modo CW, CWL o CWU: F1–F12 activan las macros CW correspondientes, y **Escape** limpia el búfer de envío.
- Cuando la banda activa está en un modo de voz: F1–F12 activan macros DVK en su lugar.
- Los accesos directos son gestionados automáticamente por MainWindow según el modo de la banda activa.

## Relacionados

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
