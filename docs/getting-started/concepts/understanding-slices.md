# Comprender los slices y los VFOs

Un slice es un canal de recepción (y, opcionalmente, de transmisión) independiente dentro de un único panadapter. Comprender cómo se corresponden los slices con los VFOs es la base para usar AetherSDR de manera eficaz, ya sea que esté monitoreando una sola frecuencia o realizando operación en split a través de varias bandas simultáneamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los slices son creados y administrados por el firmware de la radio; no existen sin una conexión activa.
- El applet RX Controls (botón RX en la bandeja de la barra lateral derecha) debe estar visible para interactuar con los controles de slice.

## Qué es un slice

El FLEX-8600 admite hasta ocho slices simultáneos, etiquetados de la A a la H. Cada slice es un canal de recepción sintonizable de forma independiente, con su propio:

- Frecuencia de VFO (mostrada en la **Frequency label** del applet RX Controls)
- Modo (USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY)
- Pasabanda del filtro
- Configuración de AGC, ganancia de AF, silenciador, RIT y XIT
- Asignación de antenas de RX y TX

Cada slice está vinculado a un panadapter. El indicador **Slice title** del panadapter (por ejemplo, "Slice A") muestra qué slice controla esa pantalla.

## Qué es el VFO

En AetherSDR, el término VFO hace referencia a la frecuencia sintonizada de un slice. No existe el concepto separado de VFO A / VFO B a nivel de aplicación; en cambio, cada slice con su letra correspondiente lleva su propia frecuencia. Trabajar en "split" significa designar un slice como el slice de TX (mediante el botón **TX (badge)**) mientras se recibe en otro.

La frecuencia actual del slice activo se muestra en la **Frequency label** del applet RX Controls. Haga clic en la etiqueta para entrar al modo de edición (**Frequency edit**), escriba una frecuencia en MHz y presione Enter para sintonizar.

## Cambiar entre slices

Cuando la radio tiene más de un slice activo, aparece una fila de pestañas etiquetadas **A**, **B**, **C**, y así sucesivamente en la parte superior del applet RX Controls. Haga clic en una pestaña para vincular el applet a ese slice. El **Slice badge** (letra de color en el applet) confirma qué slice se muestra en ese momento.

En el panadapter, cada slice aparece como su propia superposición sobre el espectro. El **Slice title** en la barra de título de cada panadapter identifica el slice asociado. En distribuciones con múltiples panadapters, puede hacer clic en el área **Spectrum / waterfall** de un panadapter para activarlo.

## Designar el slice de TX

Solo un slice transmite a la vez. Haga clic en el botón **TX (badge)** del applet RX Controls correspondiente al slice en el que desea transmitir. Esto establece ese slice como el slice de TX. Para trabajar en split, sintonice un slice a la frecuencia de transmisión y haga clic en su **TX (badge)**; luego regrese al slice de recepción usando la fila de pestañas.

## Bloquear un slice

Para evitar que un slice sea resintonizado accidentalmente, haga clic en el botón de alternancia **🔓 / 🔒** del applet RX Controls. El ícono cambia a un candado cerrado cuando el bloqueo de sintonía está activo. Un slice bloqueado ignora todas las solicitudes de cambio de frecuencia.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido |
|---|---|---|---|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX Controls. | — | 1–8 pestañas, limitado por el hardware |
| Slice badge | Muestra la letra del slice activo en ese momento. | A | A–H |
| 🔓 / 🔒 | Activa o desactiva el bloqueo de sintonía; el slice bloqueado ignora los cambios de frecuencia. | 🔓 (desbloqueado) | — |
| Frequency label | Muestra la frecuencia de VFO actual con agrupación por puntos. | 0.000.000 | — |
| Frequency edit | Escriba una frecuencia en MHz y presione Enter para sintonizar. | — | 0.001–54.000 MHz (hasta 450.000 MHz en XVTR) |
| TX (badge) | Establece este slice como el slice de TX. | — | — |
| Slice title (panadapter) | Muestra qué slice está vinculado al panadapter. | Slice A | Slice A–Slice H |

## Consejos

- La fila de pestañas de slice se oculta cuando solo hay un slice activo (número máximo de slices ≤ 1).
- Haga doble clic en el deslizador **L / R pan** para restablecerlo al centro (50) en cualquier slice.
- Los desplazamientos de RIT y XIT son por slice. Póngalos a cero con **RIT 0** y **XIT 0** antes de cambiar de tarea operativa.

## Relacionados

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Bloquear el slice para evitar una resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Usar RIT para desplazar la frecuencia de recepción ante una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la RX](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Realizar su primer QSO con AetherSDR](../tutorials/first-qso.md)
- [Comprender el panel de applets de AetherSDR](understanding-applets.md)
