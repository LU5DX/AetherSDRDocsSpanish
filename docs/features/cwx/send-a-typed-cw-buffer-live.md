# Enviar un búfer de CW escrito en tiempo real

El panel CWX le permite escribir un mensaje y transmitirlo de inmediato en código Morse. Úselo cuando necesite enviar texto CW de forma libre que no esté almacenado en una macro.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión de radio activa.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando hay un modo CW activo.

## Pasos

1. Localice el panel CWX en el área central de la ventana principal.
2. Haga clic en **Send** en la barra inferior para mostrar la vista de envío. Serán visibles el historial de envíos con desplazamiento y el área de entrada de texto.
3. Haga clic en el **Send text area** (el campo de texto en la parte inferior de la vista de envío, que muestra el marcador de posición "Type CW message...").
4. Escriba su mensaje. Use caracteres alfanuméricos estándar. Consulte la leyenda de prosigns del panel para ver los atajos de los prosigns CW más comunes.
5. Presione **Enter** para transmitir el búfer. La radio comienza a enviar de inmediato. El texto enviado aparece como una burbuja en el historial de envíos con desplazamiento que se encuentra arriba.
6. Para detener la transmisión en cualquier momento, presione **Escape**. Esto borra el búfer y cancela el envío en curso.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Send** | Muestra la vista de envío con historial y entrada de texto. | Activo al abrir | — | — |
| **Live** | Muestra la vista de envío en tiempo real. | — | — | — |
| **Setup** | Muestra el editor de macros y los controles QSK. | — | — | — |
| **Speed:** | Velocidad de envío CW en WPM. | 20 | 5–100 | `CwxSpeedWpm` |
| Send history scroll | Muestra los búferes enviados anteriormente con resaltado de caracteres. Se desplaza hacia arriba a medida que se envían nuevos búferes. | — | — | — |
| Send text area | Campo de texto donde se escribe el mensaje CW. Presione Enter para enviar. | — | — | — |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | 0–2000 | `CwxDelay` |
| **QSK** | Activa el QSK de ruptura completa. | Off | On/Off | `CwxQsk` |
| Prosigns legend | Muestra los atajos para los prosigns CW más comunes. | — | — | — |

## Consejos

- Ajuste **Speed:** en la barra inferior antes de enviar o entre envíos. El valor de `CwxSpeedWpm` se guarda y se restaura en el siguiente inicio.
- El historial de envíos con desplazamiento empuja las burbujas anteriores hacia arriba a medida que se envían más búferes, de modo que las transmisiones recientes permanecen visibles en la parte inferior.
- Presionar **Escape** es seguro incluso cuando la radio está inactiva: borrar un búfer vacío no tiene ningún efecto.
- Los atajos de teclado F1–F12 activan macros cuando el slice activo está en modo CW o CWL. No interfieren con la entrada de texto escrito en el área de texto de envío.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el slice activo está configurado en modo CW, CWL o CWU, y que AetherSDR está conectado a la radio.
- **Presionar Enter no hace nada** — Haga clic primero en el área de texto de envío para darle el foco y, luego, presione Enter.
- **Las teclas de función activan macros en lugar de aparecer como texto escrito** — F1–F12 son atajos globales de la aplicación cuando hay un slice en modo CW activo. Escriba texto usando solo teclas de letras y números; las teclas de función están reservadas para las macros.

## Relacionado

- [Descripción general de CWX](overview.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Activar el QSK de ruptura completa](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosigns](look-up-the-prosign-character-shortcuts.md)
