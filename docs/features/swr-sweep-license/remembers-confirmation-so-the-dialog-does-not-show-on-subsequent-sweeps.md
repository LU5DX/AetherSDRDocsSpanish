# Confirmación de "Recordar mi respuesta" para que el cuadro de diálogo no se muestre en barridos posteriores

Después de confirmar el descargo de responsabilidad del operador y marcar "Recordar mi respuesta", AetherSDR persiste esa confirmación para que el cuadro de diálogo "Antenna SWR Sweep – License Confirmation" se omita en todos los barridos futuros para la estación actual.

## Antes de comenzar

- Debe haber iniciado un barrido de ROE de antena al menos una vez (consulte [Confirmar la responsabilidad del operador antes de ejecutar el barrido de ROE de antena](confirm-operator-responsibility-before-running-the-antenna-swr-sweep.md)).
- La configuración persistida es por estación (se almacena bajo el nombre de la estación actual en el archivo de configuración).

## Pasos

1. Cuando aparezca el cuadro de diálogo "Antenna SWR Sweep — License Confirmation", lea el descargo de responsabilidad del operador.
2. Marque la casilla **Remember my answer**.
3. Haga clic en **I am licensed to use this feature**.

El cuadro de diálogo establece la clave `SwrSweepLicenseConfirmed` en `True` en AppSettings. En barridos posteriores, el asistente `.confirm()` lee esta clave y devuelve `true` inmediatamente sin mostrar el cuadro de diálogo.

## Función de cada control

| Control | Valor predeterminado | Clave persistida | Comportamiento |
|---|---|---|---|
| Casilla **Remember my answer** | Sin marcar | `SwrSweepLicenseConfirmed` | Cuando está marcada, persiste la confirmación en AppSettings para que el cuadro de diálogo se omita en barridos posteriores. |
| Botón **I am licensed to use this feature** | — | — | Acepta el descargo de responsabilidad y procede al barrido de ROE. Botón predeterminado (resaltado con un borde azul). |
| Botón **Cancel** | — | — | Rechaza el descargo de responsabilidad y aborta el barrido. El barrido no se iniciará. |

## Consejos

- El cuadro de diálogo también se omite si tiene un archivo de configuración guardado de una sesión anterior donde ya marcó **Remember my answer** — la clave persiste entre reinicios de la aplicación.
- Para que el cuadro de diálogo vuelva a aparecer, elimine o edite manualmente la línea `SwrSweepLicenseConfirmed` en su archivo de configuración de AetherSDR (`~/.config/AetherSDR/AetherSDR.settings` en Linux/macOS).

## Relacionados

- [Resumen de "Antenna SWR Sweep — License Confirmation"](overview.md)
- [Confirmar la responsabilidad del operador antes de ejecutar el barrido de ROE de antena](confirm-operator-responsibility-before-running-the-antenna-swr-sweep.md)
