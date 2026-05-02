# Supervisar el recorte de la salida con el medidor de nivel en el editor

El editor flotante de Tube incluye un medidor de nivel de salida en tiempo real que muestra el nivel de pico posterior a la saturación. Úselo para confirmar que los ajustes de Drive y Output no están recortando la señal procesada antes de que salga de la etapa de tubo.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea supervisar (TX o RX). Consulte [Omitir el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md) si la etapa aún no está activa.
- El editor flotante debe estar abierto. El medidor de nivel no es visible en el panel del applet acoplado.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor flotante. El editor de TX tiene el título "Aetherial Tube — TX"; el editor de RX tiene el título "Aetherial Tube — RX".
2. Localice el medidor "OUT" en el extremo derecho del editor. Muestra el nivel de pico posterior a la saturación con una dinámica de ataque rápido y caída lenta.
3. Pase audio por la etapa — transmita o reciba señal según corresponda — y observe el medidor mientras ajusta Drive y Output.
4. Mantenga el medidor fuera de la zona roja. Las bandas de color indican los siguientes niveles:

   | Color | Rango |
   |-------|-------|
   | Verde | −60 a −12 dB |
   | Lima  | −12 a −6 dB  |
   | Ámbar | −6 a −3 dB   |
   | Rojo  | Por encima de −3 dB |

5. Si el medidor marca consistentemente en rojo, reduzca el potenciómetro Output (rango −24.0 a 12.0 dB, valor predeterminado 0.00 dB, persistido como `ClientTubeTxOutputDb` o `ClientTubeRxOutputDb`) o reduzca el potenciómetro Drive (rango 0.0 a 24.0 dB, valor predeterminado 0.00 dB, persistido como `ClientTubeTxDriveDb` o `ClientTubeRxDriveDb`) hasta que el medidor permanezca en la banda ámbar o inferior bajo condiciones de señal típicas.

## Consejos

- El medidor refleja la señal después de la etapa de tubo. Reducir Drive afecta tanto el carácter armónico como el nivel; reducir Output recorta únicamente el nivel sin modificar la curva de saturación.
- El potenciómetro Dry/Wet (persistido como `ClientTubeTxDryWet` o `ClientTubeRxDryWet`) mezcla de nuevo la señal seca. Con valores por debajo del 100 %, el medidor leerá un nivel más bajo porque la señal sin procesar se mezcla con la salida saturada, lo que puede enmascarar cuánto se está forzando el tubo en sí.
- Los cambios realizados en el editor flotante se reflejan en los potenciómetros del panel del applet acoplado en aproximadamente 33 ms a través del temporizador de sincronización, y viceversa.

## Relacionados

- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Mezcla en paralelo de la saturación con Dry/Wet](parallel-blend-saturation-with-dry-wet.md)
- [Omitir el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md)
