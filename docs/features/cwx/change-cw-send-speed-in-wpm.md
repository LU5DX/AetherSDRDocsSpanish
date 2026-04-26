# Cambiar la velocidad de envío CW en PPM

Ajuste la velocidad de manipulación CW para que el radio transmita a la tasa de palabras por minuto (PPM/WPM) que necesita. El ajuste de velocidad está disponible en todo momento desde la barra inferior del panel CWX.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El panel CWX requiere una conexión de radio activa.
- Abra el panel CWX. Aparece en el área de la ventana principal cuando el slice activo está en modo CW, CWL o CWU.

## Pasos

1. Localice el spinbox **Speed:** en la barra inferior del panel CWX.
2. Haga clic en el spinbox y escriba un valor, o use las flechas arriba/abajo para ajustar la velocidad.
3. La nueva velocidad surte efecto de inmediato. El valor se guarda como `CwxSpeedWpm`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| **Speed:** | 20 | 5–100 WPM | `CwxSpeedWpm` | Establece la velocidad de manipulación CW en palabras por minuto. |

## Consejos

- El spinbox **Speed:** es visible en las tres vistas (Send, Live y Setup). No es necesario cambiar de vista para modificar la velocidad.
- Presione Escape en cualquier momento para cancelar una transmisión en curso sin modificar el ajuste de velocidad.

## Relacionados

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en directo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Habilitar QSK de ruptura completa](enable-qsk-full-break-in.md)
