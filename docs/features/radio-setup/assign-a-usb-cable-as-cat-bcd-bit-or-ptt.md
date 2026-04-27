# Asignar un cable USB como CAT, BCD, bit o PTT

Use esta página para configurar los adaptadores seriales USB conectados a su FLEX-8600 y asignar a cada uno una función: control CAT, datos de banda BCD, salida de bit individual o PTT, junto con sus parámetros seriales y opciones de comportamiento.

## Antes de comenzar

- Conecte el o los adaptadores seriales USB a la computadora que ejecuta AetherSDR antes de abrir el diálogo.
- AetherSDR debe estar conectado a la radio. La pestaña USB Cables no está disponible sin una conexión activa con la radio.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña USB Cables. También puede abrir `Settings > Radio Setup...` y hacer clic en la pestaña **USB Cables**.
2. Localice la lista de cables en el lado izquierdo de la pestaña. Cada cable USB detectado aparece con su nombre y un indicador de estado **Plugged** (conectado) o **Unplugged** (desconectado).
3. Seleccione el cable que desea configurar haciendo clic en él en la lista.
4. Establezca el tipo de cable mediante el campo **Name:** y el selector de tipo asociado. Elija entre CAT, BCD, bit o PTT según la función que deba cumplir el cable.
5. Active **Enabled** para habilitar el cable. El cable no funcionará hasta que esté habilitado.
6. Configure los parámetros seriales del cable:
   - **Speed** — velocidad en baudios de la conexión serial.
   - **Data Bits** — número de bits de datos.
   - **Parity** — configuración de paridad.
   - **Stop Bits** — número de bits de parada.
   - **Flow** — método de control de flujo.
7. Configure las opciones de comportamiento correspondientes al tipo de cable:
   - **Source** — selecciona qué señal de la radio controla la salida del cable.
   - **Auto Report** — controla si los cambios de estado se reportan automáticamente.
   - **BCD Type** — selecciona el formato de codificación BCD (solo para cables BCD).
   - **Polarity** — establece lógica activa en alto o activa en bajo.
   - **Bit Configuration (0–7)** — asigna funciones a los bits de salida individuales (solo para cables de tipo bit).
8. Repita los pasos 3–7 para los cables adicionales que sea necesario.
9. Haga clic en **Close** para cerrar el diálogo. Los ajustes surten efecto de inmediato cuando se habilita cada cable; no se requiere un paso de aplicación por separado.

## Descripción de cada control

| Control | Descripción |
|---|---|
| **Cables list / Status** | Muestra todos los adaptadores seriales USB detectados con su estado **Plugged** o **Unplugged**. Seleccione un cable aquí para editar su configuración. |
| **Name:** | Etiqueta visible para el usuario que identifica el cable. |
| **Enabled** | Activa el cable. El cable permanece inactivo hasta que se habilita. |
| **Speed** | Velocidad en baudios del puerto serial. |
| **Data Bits** | Número de bits de datos seriales. |
| **Parity** | Paridad serial: None, Even, Odd, etc. |
| **Stop Bits** | Número de bits de parada. |
| **Flow** | Método de control de flujo (None, Hardware, Software). |
| **Source** | Selecciona la señal de la radio que controla la salida del cable. |
| **Auto Report** | Cuando está activo, la radio reporta automáticamente los cambios de estado al cable. |
| **BCD Type** | Selecciona el formato de codificación de datos de banda BCD. Se aplica únicamente a cables de tipo BCD. |
| **Polarity** | Establece si la lógica de salida es activa en alto o activa en bajo. |
| **Bit Configuration (0–7)** | Asigna los pines de salida individuales a funciones específicas. Se aplica únicamente a cables de tipo bit. |

## Consejos

- Si un cable muestra **Unplugged**, verifique la conexión física del USB y vuelva a abrir el diálogo. La lista refleja el estado en el momento en que se construyó la pestaña.
- Asigne únicamente un cable PTT a la vez si desea un comportamiento predecible en la activación de transmisión.
- Los cables BCD y de tipo bit comparten muchos de los mismos parámetros seriales; configure **Speed**, **Data Bits**, **Parity**, **Stop Bits** y **Flow** para que coincidan con los requisitos del dispositivo externo que recibe los datos.

## Solución de problemas

- **El cable muestra Unplugged aunque está conectado** — Es posible que el adaptador USB no estuviera presente cuando se cargó la pestaña. Cierre Radio Setup, asegúrese de que el adaptador sea reconocido por el sistema operativo y vuelva a abrir `Settings > USB Cables...`.
- **El interruptor Enabled no tiene efecto** — Confirme que la radio está conectada. La pestaña USB Cables requiere una conexión activa con la radio; los controles no envían comandos sin ella.
- **Las salidas BCD o de bit están invertidas** — Verifique la configuración de **Polarity** del cable y cámbiela para que coincida con los niveles lógicos de su dispositivo externo.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serial de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
