# Activar QSK (Full Break-in)

QSK (full break-in) permite que el radio alterne entre transmisión y recepción entre los elementos individuales de CW, de modo que usted puede escuchar señales en los espacios entre sus propios puntos y rayas. Esta página muestra cómo activar o desactivar QSK en el panel CWX.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel CWX requiere una conexión de radio activa.
- El slice activo debe estar en modo CW, CWL o CWU para que el panel CWX sea visible.

## Pasos

1. Abra el panel CWX en el área central de MainWindow.
2. Haga clic en **Setup** en la parte inferior del panel. La vista Setup muestra los editores de macros, el control giratorio **Delay:** y el botón **QSK**.
3. Haga clic en **QSK** para activar el full break-in. El botón aparece resaltado cuando está habilitado.
4. Para desactivar QSK, haga clic en **QSK** nuevamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **QSK** | Activa o desactiva QSK (full break-in). Botón de alternancia; resaltado cuando está activo. | — | On / Off | `CwxQsk` |
| **Delay:** | Establece el retardo entre macros en milisegundos. | 5 | 0–2000 ms | `CwxDelay` |

## Relacionado

- [Descripción general de CWX](overview.md)
- [Enviar un búfer de CW escrito en tiempo real](send-a-typed-cw-buffer-live.md)
- [Cambiar la velocidad de envío de CW en WPM](change-cw-send-speed-in-wpm.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
