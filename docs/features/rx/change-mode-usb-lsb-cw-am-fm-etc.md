# Cambiar el modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo cambiar el modo de demodulación de un slice (receptor parcial) mediante el applet RX Controls. Al cambiar el modo, los preajustes de filtro y la lista de pasos de sintonía se adaptan automáticamente al nuevo modo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls no funciona sin una conexión de radio activa.
- Identifique qué slice desea cambiar. Si tiene más de un slice activo, selecciónelo primero usando las pestañas (A..H) en la parte superior del applet RX Controls.

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.
2. Si hay varios slices en uso, haga clic en la pestaña con la letra del slice (A hasta H) que desea cambiar.
3. Localice el cuadro **Mode combo** en el applet. Su valor actual se muestra allí (valor predeterminado: **USB**).
4. Haga clic en el **Mode combo** para abrir la lista de modos.
5. Seleccione el modo deseado: **USB**, **LSB**, **CW**, **AM**, **SAM**, **FM**, **NFM**, **DFM**, **DIGU**, **DIGL** o **RTTY**.
6. El slice cambia al modo seleccionado. Los botones de preajuste de filtro y la lista de pasos de sintonía se actualizan automáticamente para coincidir con el nuevo modo.

## Qué hace cada control

| Control | Valor predeterminado | Opciones válidas | Notas |
|---|---|---|---|
| Mode combo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY | Cambiar el modo adapta los preajustes de filtro y los tamaños de paso. |
| Preajustes de ancho de filtro | (depende del modo) | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz | Los botones se ocultan en los modos FM, NFM y DFM. Los preajustes se almacenan en `FilterPresets`. Haga clic derecho en un botón de preajuste para guardar el ancho actual en ese preajuste. |
| STEP | 100 Hz (índice 2) | USB/LSB: 1/10/50/100/500/1000/2000/3000 Hz; CW: 1/5/10/50/100/200/400 Hz; familia FM: 50/250/500/2500/3000/5000/10000/12500 Hz | La lista de pasos es por modo y se actualiza automáticamente al cambiar de modo. |

## Consejos

- Los modos FM, NFM y DFM no muestran botones de preajuste de ancho de filtro. Use el widget de banda pasante del filtro para arrastrar los bordes inferior/superior si necesita ajustar la banda pasante directamente.
- Tras cambiar a FM o NFM, aparecen controles adicionales: **Tone mode**, **CTCSS tone value**, **Offset**, **−**, **Simplex**, **+** y **REV** para operación de repetidor.
- Hacer clic derecho en un botón de preajuste de filtro guarda el ancho de filtro actual en ese preajuste, el cual se almacena de forma persistente en `FilterPresets`.

## Solución de problemas

- **El Mode combo no responde** — El applet requiere una conexión de radio activa. Verifique que AetherSDR esté conectado mediante `Settings > Connect to Radio...`.
- **El modo RADE no aparece en la lista** — RADE requiere una compilación de AetherSDR con la opción RADE habilitada. Las compilaciones estándar no lo incluyen.

## Temas relacionados

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Operar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre varios slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Descripción general de RX Controls](overview.md)
