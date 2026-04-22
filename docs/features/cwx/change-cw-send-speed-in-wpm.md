# Cambiar la velocidad de envío CW en PPM

Ajuste la velocidad de envío de CWX para que la radio transmita a la cantidad de palabras por minuto que desee. El ajuste de velocidad surte efecto de inmediato y se guarda entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. CWX requiere una conexión de radio activa.
- El slice activo debe estar en modo CW, CWL o CWU, o el panel CWX debe estar ya abierto.

## Pasos

1. Ubique el panel CWX en el área central de la ventana principal.
2. Encuentre el cuadro de valores **Speed:** en la barra inferior del panel CWX.
3. Haga clic en el cuadro de valores y escriba un número, o use las flechas arriba/abajo para ajustar la velocidad.
4. La nueva velocidad surte efecto de inmediato. No se requiere ningún paso de confirmación.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de ajuste |
|---------|-------------|----------------------|--------------|-----------------|
| **Speed:** | Velocidad de envío CW en palabras por minuto. | 20 WPM | 5–100 WPM | `CwxSpeedWpm` |

## Consejos

- El cuadro de valores **Speed:** siempre es visible en la barra inferior, independientemente de la vista activa (Send, Live o Setup). No es necesario cambiar de vista para modificar la velocidad.
- Los cambios de velocidad se aplican tanto a los búferes de texto escrito como a las macros de teclas F.

## Relacionado

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
