# Resumen de CWX

CWX es la interfaz de manipulador telegráfico integrada de AetherSDR. Permite enviar texto escrito o macros predefinidas a través del manipulador de la FLEX-8600, controlar la velocidad de transmisión, configurar el retardo entre macros y activar QSK de trabajo en plena ruptura, todo sin salir de la aplicación.

## Antes de empezar

- Conéctese a una radio FLEX-8600. CWX requiere una conexión activa con la radio.
- Configure la franja activa en modo CW, CWL o CWU. El panel CWX aparece en el área central de la ventana principal cuando hay una franja en modo CW activa.

## Cómo funciona

CWX presenta tres vistas, seleccionables mediante los botones en la parte inferior del panel: Enviar, En vivo y Configuración. El cuadro giratorio Velocidad: y los botones de selección de vista están siempre visibles, independientemente de la vista activa.

**Vista Enviar** — Muestra un historial desplazable de búferes enviados previamente como burbujas de chat, con un área de ingreso de texto en la parte inferior. Escriba su mensaje y presione Enter para enviarlo. Los caracteres se resaltan en el historial a medida que se transmiten. Si En vivo está activo, al hacer clic en Enviar primero se desactiva el envío en vivo sin retransmitir ningún texto que ya se haya manipulado carácter por carácter. Si En vivo ya está desactivado, al hacer clic en Enviar se envía el búfer inmediatamente.

**Vista En vivo** — Alterna el envío carácter por carácter en vivo entre activado y desactivado. Cuando En vivo está habilitado, cada carácter que escribe se transmite de inmediato en lugar de esperar hasta que presione Enter. Hacer clic en Configuración o Enviar mientras En vivo está activo desactiva automáticamente el envío en vivo antes de cambiar de vista.

**Vista Configuración** — Muestra los 12 editores de macros para las teclas F, el control Retardo: y el conmutador QSK. Edite aquí el texto de las macros y configure las opciones de temporización del manipulador. Al abrir la vista Configuración siempre se desactiva el envío en vivo.

**Atajos F1–F12** — Cuando la franja activa está en modo CW o CWL, presionar F1 a F12 en el teclado envía la macro correspondiente de inmediato, independientemente de la vista que se muestre en ese momento.

**Escape** — Presionar Escape anula la transmisión CW actual y limpia el búfer de envío. Esto funciona en toda la aplicación mientras CWX esté activo.

## Función de cada control

| Control | Descripción | Ajuste persistente |
|---|---|---|
| Enviar | Envía el búfer escrito si En vivo está desactivado. Si En vivo está activo, desactiva el envío en vivo y cambia a la vista de envío sin retransmitir los caracteres ya manipulados. | — |
| En vivo | Botón de alternancia. Activa el envío carácter por carácter en vivo cuando está activado; lo desactiva cuando está desactivado. El estado del botón se mantiene sincronizado con el modelo de radio. | — |
| Configuración | Cambia al editor de macros y a la vista de configuración QSK. Desactiva el envío en vivo si está activo. | — |
| Velocidad: | Velocidad de transmisión CW en WPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Desplazamiento del historial de envío | Pantalla desplazable de búferes de envío anteriores con resaltado por carácter. Solo lectura. | — |
| Área de texto de envío | Campo de ingreso de texto. Presione Enter para enviar el búfer escrito. | — |
| F1 … F12 (botones de macro) | Envía la macro almacenada para esa tecla de función. Activo mediante atajo de teclado cuando la franja está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macros F1 … F12 | Campos de texto en la vista Configuración para escribir o editar cada cadena de macro. | `CwxMacro_F1` – `CwxMacro_F12` |
| Retardo: | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Activa QSK de trabajo en plena ruptura cuando está marcado. | `CwxQsk` |
| Leyenda de prosignos | Referencia de solo lectura que muestra los atajos de caracteres para prosignos CW comunes (=, +, (, &, $). | — |

## Consejos

- Presionar Escape durante una transmisión de macro limpia el búfer de inmediato. Dado que el estado del manipulador alterna rápidamente entre puntos y rayas, Escape se activa incondicionalmente sin esperar un estado de transmisión específico, por lo que detiene la transmisión de forma confiable.
- Los atajos de teclado F1–F12 solo se activan cuando la franja activa está en modo CW o CWL. Cambiar la franja a un modo que no sea CW los desactiva automáticamente.
- Si cambia a la vista Configuración o hace clic en Enviar mientras En vivo está activo, el envío en vivo se desactiva automáticamente. No retransmitirá accidentalmente caracteres que el manipulador ya haya enviado.
- El estado del botón En vivo refleja directamente el modelo de radio. Si el modelo informa que el envío en vivo está activo cuando el panel se carga por primera vez, el botón En vivo ya aparecerá presionado.

## Relacionados

- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de transmisión CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar QSK de trabajo en plena ruptura](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres para prosignos](look-up-the-prosign-character-shortcuts.md)
