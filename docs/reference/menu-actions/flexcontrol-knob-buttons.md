# Perilla y Botones FlexControl

Abre la configuración de la Perilla de Sintonización FlexControl dentro de la página Serial & Controllers de Radio Setup, para que pueda ajustar el comportamiento de la perilla y los botones sin tener que abrir primero AetherControl.

## Antes de comenzar

- Una radio FLEX-8600 con el hardware FlexControl conectado mediante USB.
- AetherSDR compilado con soporte de puerto serie (de lo contrario, el elemento de menú está oculto).

## Pasos

1. Haga clic en **Settings > FlexControl Knob & Buttons...**.
2. El cuadro de diálogo Radio Setup se abre en la página **Serial & Controllers**, con el grupo **FlexControl Tuning Knob** en foco.
3. Ajuste la perilla y la configuración de los botones según sea necesario.
4. Haga clic en **Close** (o el equivalente del cuadro de diálogo) para aplicar los cambios.

## Consejos

- Este elemento de menú es un acceso directo: la misma configuración se puede alcanzar desde **Settings > AetherControl...** seguido del botón de configuración del controlador.
- Si el FlexControl no se detecta, revise el cable USB y confirme que el dispositivo aparece en la página Serial & Controllers antes de ajustar la configuración.

## Solución de problemas

- **El elemento de menú está atenuado o no aparece** — AetherSDR fue compilado sin soporte de puerto serie (compuerta de compilación `HAVE_SERIALPORT`). Recompile con soporte de puerto serie o use la ventana AetherControl si está disponible.

## Relacionado

- [Configuring AetherSDR Controls](configuring-aethersdr-controls.md)
- [USB Cables](usb-cables.md)
- [Getting Started](getting-started.md)
