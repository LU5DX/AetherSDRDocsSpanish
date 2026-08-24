# Sintonice el amplificador SPE Expert

Ejecute un ciclo de sintonización ATU en su amplificador lineal SPE Expert (1.3K-FA, 1.5K-FA, 2K-FA) directamente desde AetherSDR, sin tocar el panel frontal del amplificador.

## Antes de comenzar

- Conéctese a su radio FLEX-8600 (el applet SPE requiere una conexión de radio activa).
- Asegúrese de que el amplificador SPE Expert esté conectado mediante puerto serie o ser2net TCP y aparezca en el panel Applet.
- Abra el applet SPE: **Applet panel > SPE tile**.

## Pasos

1. Haga clic en **ON** para encender el amplificador si aún no está encendido.
2. Haga clic en **OPER** para cambiar el amplificador del modo STANDBY al modo OPERATE. La píldora de estado debe indicar **OPR · RX**.
3. Si es necesario, presione **PWR** para seleccionar el nivel de potencia deseado (LOW, MID o HIGH). La etiqueta del botón muestra el nivel actual.
4. Haga clic en **TUNE** para iniciar el ciclo de sintonización ATU. El amplificador activa TX y ejecuta su rutina de sintonización con excitación de RF.

El ciclo de sintonización se completa automáticamente. Observe el indicador **ATU SWR** estabilizarse para confirmar la adaptación.

## Función de cada control

| Control | Comportamiento |
| --- | --- |
| **ON** | Enciende el amplificador pulsando las líneas de control serie. A través de la red, esto requiere un puerto ser2net habilitado con rfc2217. |
| **OPER** | Alterna entre STANDBY y OPERATE (refleja la tecla OPERATE del panel frontal). |
| **PWR** | Cicla el nivel de potencia de salida LOW → MID → HIGH. La etiqueta del botón muestra el nivel actual. |
| **TUNE** | Inicia la sintonización ATU (refleja la tecla TUNE del panel frontal). Activa TX durante el ciclo. |
| **OFF** | Apaga el amplificador. Use **ON** para volver a encenderlo. |
| **INPUT** | Alterna entre los puertos de entrada 1 y 2. |
| **ANT** | Cicla la antena de TX para la banda actual. |
| **▼ / ▲** | Reduce o aumenta la potencia de excitación que el amplificador solicita a la radio a través de CAT. |

## Consejos

- El indicador **ATU SWR** muestra la ROE antes del ATU; el indicador **SWR** muestra la ROE del lado de la antena. Después de sintonizar, ambos deberían bajar hacia 1:1.
- El botón **TUNE** está marcado como un control de activación de TX — asegúrese de que la potencia de sintonía de su banda esté configurada adecuadamente en **Settings > TX Band Settings...** antes de sintonizar.
- El amplificador sigue la banda de su radio automáticamente; no hay teclas de banda en el applet.

## Solución de problemas

- **TUNE está deshabilitado (atenuado)** — El amplificador puede estar en STANDBY u OFF. Haga clic en **OPER** o **ON** primero. Algunas teclas se deshabilitan mientras el amplificador está en silencio.
- **ON / OFF no hacen nada a través de la red** — Estos requieren un puerto ser2net habilitado con rfc2217. Verifique la configuración de su conexión serie en **Settings > Radio Setup...**.

## Relacionados

- [Descripción general del amplificador SPE Expert](overview.md)
- [Ponga el amplificador SPE Expert en Operate o Standby](put-the-spe-expert-amplifier-in-operate-or-standby.md)
- [Cicle el nivel de potencia del SPE Expert (Low, Mid, High)](cycle-the-spe-expert-power-level-low-mid-high.md)
- [Monitoree la potencia directa y la ROE en el amplificador SPE Expert](monitor-forward-power-and-swr-on-the-spe-expert-amplifier.md)
