# Cambiar perfiles de TX (p. ej., SSB, Digital)

Use el applet TX Controls para cambiar entre perfiles de transmisión almacenados en el radio, como perfiles configurados para SSB, modos digitales u otros estilos de operación. Los perfiles se crean y administran en el radio y se cargan en AetherSDR automáticamente al momento de la conexión.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls no está activo sin una conexión al radio.
- Debe existir al menos un perfil de TX en el radio. Use `Profiles > Profile Manager...` para ver los perfiles disponibles, o créelos en SmartSDR.
- El applet TX Controls debe estar visible. Si no se muestra, haga clic en el botón TX tray en la barra lateral derecha.

## Pasos

1. Localice el menú desplegable **TX Profile** en el applet TX Controls. Aparece directamente debajo de los controles deslizantes **RF Power** y **Tune Pwr**.
2. Haga clic en el menú desplegable **TX Profile** para expandirlo. La lista se completa con los perfiles almacenados en el radio.
3. Haga clic en el perfil que desea cargar (por ejemplo, "SSB" o "Digital").

El radio carga el perfil seleccionado de inmediato. No se requiere ningún paso de confirmación.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado | Valores válidos |
|---|---|---|---|---|
| TX Profile | Menú desplegable | Selecciona y carga un perfil de transmisión desde el radio. Al enviar una nueva selección, ese perfil se carga en el radio de inmediato. | Se completa desde el radio al conectar | Perfiles devueltos por el radio |

## Consejos

- Los nombres de los perfiles se definen en el radio. Si falta un perfil que espera encontrar, verifique que exista en `Profiles > Profile Manager...`.
- También puede cargar un perfil desde la barra de menú sin abrir el applet TX Controls: `Profiles` muestra todos los perfiles disponibles debajo de un separador. Haga clic en el nombre de un perfil para cargarlo directamente.
- No se recomienda cambiar perfiles durante una transmisión. Realice los cambios mientras está en recepción.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Ajustar la potencia del portador de sintonía](set-tune-carrier-power.md)
- [Realice su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
