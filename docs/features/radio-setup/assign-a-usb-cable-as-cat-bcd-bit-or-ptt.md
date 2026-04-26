# Asignar un cable USB como CAT, BCD, bit o PTT

La pestaña USB Cables en Radio Setup permite asignar adaptadores seriales USB físicos conectados al FLEX-8600 a funciones específicas: control CAT, datos de banda BCD, salidas de bit individuales o PTT. Use esta página para configurar qué función cumple cada cable y establecer sus parámetros seriales.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña USB Cables no es accesible sin una conexión activa al radio.
- El adaptador serial USB debe estar físicamente conectado al FLEX-8600 antes de abrir la pestaña. Los cables desconectados aparecen con el estado Unplugged.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña **USB Cables**. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Localice su cable en la lista **Cables list**. Cada adaptador detectado aparece en la lista con su **Status** actual mostrado como Plugged o Unplugged.
3. Seleccione la entrada del cable que desea configurar.
4. Establezca **Name:** con una etiqueta descriptiva para el cable.
5. Establezca el tipo de cable usando el campo correspondiente. Los tipos disponibles son CAT, BCD, bit y PTT. Seleccione el tipo que corresponda a su uso previsto.
6. Active **Enabled** para habilitar el cable una vez completada la configuración.
7. Para cables CAT y BCD, configure los parámetros de línea serial: **Speed**, **Data Bits**, **Parity**, **Stop Bits** y **Flow**.
8. Establezca **Source** para seleccionar qué señal controla la salida del cable.
9. Para cables CAT, configure **Auto Report** según sea necesario.
10. Para cables BCD, configure **BCD Type** y **Polarity**.
11. Para cables de bit, configure **Bit Configuration (0–7)** y **Polarity** para cada posición de bit.
12. Cierre el diálogo. Los ajustes se aplican al radio de inmediato cada vez que se modifica un control.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Cables list / Status** | Lista todos los cables USB detectados y muestra Plugged o Unplugged para cada uno. |
| **Name:** | Etiqueta asignada por el usuario al cable. |
| **Enabled** | Activa o desactiva el cable. |
| **Speed** | Velocidad en baudios del cable. |
| **Data Bits** | Número de bits de datos por trama serial. |
| **Parity** | Configuración de paridad para la conexión serial. |
| **Stop Bits** | Número de bits de parada por trama serial. |
| **Flow** | Modo de control de flujo. |
| **Source** | Selecciona la señal o fuente de datos que controla la salida de este cable. |
| **Auto Report** | Controla si el radio envía actualizaciones automáticamente a través del cable CAT. |
| **BCD Type** | Selecciona el formato de codificación BCD (solo cables BCD). |
| **Polarity** | Establece la polaridad activa-alta o activa-baja para cables BCD y de bit. |
| **Bit Configuration (0–7)** | Asigna una función a cada una de las ocho salidas de bit (solo cables de bit). |

## Consejos

- Si un cable que espera ver no aparece en la lista, verifique que esté físicamente conectado al radio y que el firmware del radio lo reconozca. Puede ser necesario volver a abrir la pestaña USB Cables después de conectar el cable para actualizar la lista.
- Configurar un cable como PTT no requiere parámetros seriales: solo aplican **Enabled**, **Source** y **Polarity**.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serial de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
