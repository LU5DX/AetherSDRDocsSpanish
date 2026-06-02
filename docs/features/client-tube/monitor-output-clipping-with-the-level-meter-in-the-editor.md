# Monitoreo de recorte en la salida con el medidor de nivel en el editor

El editor flotante de Tube incluye un medidor de nivel de salida en vivo que muestra el pico posterior a la saturación. Úselo para confirmar que los ajustes de Drive y Output no están recortando la señal procesada antes de que salga de la etapa de tubo.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea monitorear (TX o RX). Consulte [Omitir el tubo de cualquiera de las cadenas](bypass-the-tube-from-either-chain.md) si la etapa aún no está activa.
- El editor flotante debe estar abierto. El medidor de nivel no es visible en el mosaico de applet acoplado.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor flotante. El editor de TX tiene el título "Aetherial Tube — TX"; el editor de RX tiene el título "Aetherial Tube — RX".
2. Localice el medidor "OUT" en el extremo derecho del editor. Muestra el pico posterior a la saturación con balística de ataque rápido y liberación lenta.
3. Pase audio a través de la etapa — transmita o reciba señal según corresponda — y observe el medidor mientras ajusta Drive y Output.
4. Mantenga el medidor fuera de la zona roja. Las bandas de color indican los siguientes niveles:

| Color | Rango          | Notas                                                                                                         |
|-------|----------------|---------------------------------------------------------------------------------------------------------------|
| Verde | −60 a −12 dB   |                                                                                                               |
| Lima  | −12 a −6 dB    |                                                                                                               |
| Ámbar | −6 a −3 dB     |                                                                                                               |
| Rojo  | Por encima de −3 dB |                                                                                                               |

5. Si el medidor marca consistentemente en rojo, reduzca la perilla Output (rango −24.0 a 12.0 dB, predeterminado 0.00 dB, persistido como `ClientTubeTxOutputDb` o `ClientTubeRxOutputDb`) o reduzca la perilla Drive (rango 0.0 a 24.0 dB, predeterminado 0.00 dB, persistido como `ClientTubeTxDriveDb` o `ClientTubeRxDriveDb`) hasta que el medidor se mantenga en las bandas ámbar o inferiores en condiciones de señal típicas.

## Consejos

- El medidor refleja la señal después de la etapa de tubo. Reducir Drive afecta tanto el carácter armónico como el nivel; reducir Output solo recorta el nivel sin cambiar la curva de saturación.
- La perilla Dry/Wet (persistida como `ClientTubeTxDryWet` o `ClientTubeRxDryWet`) mezcla la señal seca nuevamente. En valores inferiores al 100 %, el medidor marcará más bajo porque la señal no procesada se mezcla con la salida saturada, lo que puede enmascarar qué tan fuerte se está excitando el tubo.
- Los cambios realizados en el editor flotante se reflejan en las perillas del mosaico de applet acoplado en aproximadamente 33 ms a través del temporizador de sincronización, y viceversa.
- Cuando la etapa Tube está omitida, todo el mosaico de applet acoplado se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Este atenuado visual coincide con el comportamiento del mosaico de la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. La opacidad vuelve al 100 % tan pronto como se vuelve a habilitar la etapa.
- Los valores de las perillas se pueden editar directamente haciendo clic en el texto del valor. Esto abre una superposición de editor de texto en línea. Escriba el valor deseado y presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido para esa perilla. Presione Escape para cancelar la edición y volver al valor anterior.

## Relacionado

- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ajustar Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Mezcla en paralelo de saturación con Dry/Wet](parallel-blend-saturation-with-dry-wet.md)
- [Omitir el tubo de cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
