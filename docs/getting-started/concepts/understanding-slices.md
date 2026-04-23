# Entender los slices y los VFO

Un slice (canal de recepción independiente) es un canal de recepción —y opcionalmente de transmisión— que opera dentro de un único panadapter en el FLEX-8600. Comprender cómo los slices se corresponden con los VFO le ayudará a navegar por los controles de AetherSDR y a trabajar varias señales simultáneamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los controles de slice no están disponibles sin conexión.
- Familiarícese con el Panel de Applets en la barra lateral derecha. El applet RX Controls (que se activa con el botón RX del panel lateral) es donde se encuentran los ajustes por slice.

## Cómo funcionan los slices y los VFO

El FLEX-8600 admite hasta ocho slices simultáneos, etiquetados de A a H. Cada slice es un receptor independiente con su propio:

- **Frecuencia de VFO** — mostrada en la etiqueta Frequency del applet RX Controls, con formato de grupos MHz separados por puntos (por ejemplo, `14.225.000`).
- **Modo** — USB, LSB, CW, AM, FM y otros, seleccionables desde el combo Mode.
- **Pasabanda del filtro** — un par de valores bajo/alto que puede configurar mediante presets de ancho de filtro o arrastrando los bordes del widget Filter passband.
- **Asignación de antena** — selectores de antena RX y TX independientes.
- **Controles de audio** — ganancia AF, panorama L/R, squelch, AGC, RIT y XIT, todos independientes por slice.

Un slice a la vez es el **TX slice** — el que transmite cuando activa la clave. El botón TX del applet RX Controls identifica y establece el TX slice.

Los slices aparecen como marcadores superpuestos en el espectro/waterfall del panadapter. Cada slice tiene un código de color; el indicador Slice (A, B, C…) en el applet RX Controls usa el mismo color que el marcador correspondiente en el panadapter.

## Cambiar entre slices

El applet RX Controls muestra una fila de **pestañas Slice (A..H)** en la parte superior cuando existe más de un slice. Haga clic en una pestaña para vincular el applet a ese slice. Todos los controles debajo de la fila de pestañas —frecuencia, modo, filtro, AGC, RIT/XIT, etc.— se aplican entonces al slice seleccionado.

La fila se oculta cuando solo hay un slice activo.

## El TX slice

Solo un slice transmite a la vez. Haga clic en el botón **TX (badge)** del applet RX Controls correspondiente al slice desde el que desea transmitir. El indicador TX se ilumina para indicar que ese slice está activo para transmisión. Cambiar el TX slice no afecta la frecuencia de recepción ni los ajustes de ningún otro slice.

## La frecuencia y el indicador de VFO

La **etiqueta Frequency** muestra la frecuencia de VFO actual del slice. Haga clic en ella para entrar en modo de edición; escriba un valor en MHz y presione Enter para sintonizar y centrar el panadapter en esa frecuencia. El campo acepta valores de 0.001 a 54.000 MHz (hasta 450.000 MHz cuando el slice está en una antena de transverter).

El spinbox **STEP** controla cuánto se desplaza la frecuencia por cada clic de la rueda de desplazamiento o por cada clic de las flechas `<` / `>`. El paso predeterminado es 100 Hz. Los pasos disponibles dependen del modo activo — por ejemplo, SSB ofrece pasos de 1, 10, 50, 100, 500, 1000, 2000 y 3000 Hz.

## RIT y XIT

Dos desplazamientos incrementales permiten ajustar la recepción o la transmisión de forma independiente sin modificar el VFO principal:

- **RIT** (Sintonía Incremental de Recepción) — desplaza únicamente la frecuencia de recepción. Actívelo con el botón de alternancia RIT; ajústelo con el spinbox de desplazamiento RIT en pasos de 10 Hz; llévelo a cero con RIT 0.
- **XIT** (Sintonía Incremental de Transmisión) — desplaza únicamente la frecuencia de transmisión. Actívelo con el botón de alternancia XIT; ajústelo con el spinbox de desplazamiento XIT en pasos de 10 Hz; llévelo a cero con XIT 0.

Ambos tienen un valor predeterminado de +0 Hz.

## Bloquear un slice

El botón de alternancia 🔓 / 🔒 bloquea el slice contra cambios de frecuencia. Cuando está bloqueado (🔒), el slice ignora cualquier entrada de sintonía — útil cuando desea monitorear una frecuencia fija mientras trabaja en otro slice. Haga clic de nuevo para desbloquear (🔓).

## Relación con el panadapter

Cada panadapter muestra el espectro alrededor de uno o más slices. El indicador **Slice title** en la parte superior de cada panel de panadapter muestra a qué slice está vinculado (por ejemplo, `Slice A`). En modo multislice, puede hacer clic en el área de espectro/waterfall para activar un panadapter diferente. La opción **Pan Follows VFO** (`View > Pan Follows VFO`, activada por defecto) mantiene visible el marcador de VFO del slice activo mientras sintoniza.

## Relacionados

- [Cambiar entre varios slices usando la fila de pestañas A..H](../../features/rx/switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Bloquear el slice para evitar una resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Usar RIT para desplazar la frecuencia de recepción de una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislice)](../../features/panadapter/click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general de RX Controls](../../features/rx/overview.md)
- [Descripción general del panadapter](../../features/panadapter/overview.md)
- [Realizar su primer QSO con AetherSDR](../tutorials/first-qso.md)
