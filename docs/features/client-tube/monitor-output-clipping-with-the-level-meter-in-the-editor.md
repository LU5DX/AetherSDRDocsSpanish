# Monitoreo de recorte en la salida con el medidor de nivel en el editor

El editor flotante de Tube incluye un medidor de nivel de salida en vivo que muestra el nivel máximo posterior a la saturación. Úselo para confirmar que los ajustes de Drive y Output no están recortando la señal procesada antes de que salga de la etapa de tubo.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea monitorear (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md) si la etapa aún no está activa.
- El editor flotante debe estar abierto. El medidor de nivel no es visible en el mosaico acoplado del applet.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor flotante. El editor de TX se titula "Aetherial Tube — TX"; el editor de RX se titula "Aetherial Tube — RX".
2. Localice el medidor "OUT" en el extremo derecho del editor. Muestra el nivel máximo posterior a la saturación con balística de ataque rápido y liberación lenta.
3. Pase audio a través de la etapa — transmita o reciba señal según corresponda — y observe el medidor mientras ajusta Drive y Output.
4. Mantenga el medidor fuera de la zona roja. Las bandas de color indican los siguientes niveles:

   | Color  | Rango          |
   |--------|----------------|
   | Verde  | −60 a −12 dB   |
   | Lima   | −12 a −6 dB    |
   | Ámbar  | −6 a −3 dB     |
   | Rojo   | Por encima de −3 dB |

5. Si el medidor marca consistentemente en rojo, reduzca la perilla Output (rango −24.0 a 12.0 dB, valor predeterminado 0.00 dB, almacenado como `ClientTubeTxOutputDb` o `ClientTubeRxOutputDb`) o reduzca la perilla Drive (rango 0.0 a 24.0 dB, valor predeterminado 0.00 dB, almacenado como `ClientTubeTxDriveDb` o `ClientTubeRxDriveDb`) hasta que el medidor permanezca en las bandas ámbar o inferiores en condiciones típicas de señal.

## Consejos

- El medidor refleja la señal después de la etapa de tubo. Reducir Drive afecta tanto el carácter armónico como el nivel; reducir Output solo recorta el nivel sin cambiar la curva de saturación.
- La perilla Dry/Wet (almacenada como `ClientTubeTxDryWet` o `ClientTubeRxDryWet`) mezcla la señal seca nuevamente. Con valores por debajo del 100 %, el medidor marcará más bajo porque la señal no procesada se mezcla con la salida saturada, lo que puede enmascarar qué tan fuerte se está excitando el tubo en sí.
- Los cambios realizados en el editor flotante se reflejan en las perillas del mosaico acoplado del applet en aproximadamente 33 ms mediante el temporizador de sincronización, y viceversa.
- Cuando la etapa Tube está en bypass, todo el mosaico acoplado del applet se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esta atenuación visual coincide con el comportamiento del mosaico de la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. La opacidad vuelve al 100 % tan pronto como la etapa se reactiva.

## Relacionados

- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-dry-wet.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
