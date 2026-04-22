# Asignar un cable USB como CAT, BCD, bit o PTT

Use esta página para configurar un adaptador serie USB conectado a su FLEX-8600 como cable de control CAT, salida de decodificador de banda BCD, salida de bit individual o línea PTT. Cada adaptador conectado aparece en la pestaña USB Cables, donde se define su tipo y parámetros serie.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña USB Cables solo está disponible mientras haya conexión activa.
- El adaptador serie USB debe estar físicamente conectado al puerto USB del radio antes de abrir el diálogo, para que el radio pueda detectarlo.

## Pasos

1. Abra `Settings > USB Cables...`. El diálogo Radio Setup se abre directamente en la pestaña **USB Cables**. También puede abrir `Settings > Radio Setup...` y hacer clic en la pestaña **USB Cables**.
2. Localice su cable en la lista **Cables list**. Cada adaptador detectado aparece en la lista con su **Status** actual, que indica Plugged o Unplugged.
3. Seleccione la entrada del cable que desea configurar.
4. Establezca **Name:** con una etiqueta descriptiva para el cable.
5. Establezca **Enabled** según el estado deseado para este cable.
6. Configure **Speed**, **Data Bits**, **Parity**, **Stop Bits** y **Flow** para que coincidan con los parámetros serie requeridos por el dispositivo conectado.
7. Configure **Source** para definir qué señal maneja la salida del cable.
8. Si el tipo de cable es BCD, configure **BCD Type** y **Polarity** según los requisitos de su decodificador de banda.
9. Si el tipo de cable es bit, use **Bit Configuration (0-7)** para asignar la función de cada bit de salida.
10. Si el tipo de cable es PTT, confirme que **Polarity** coincida con la entrada de su amplificador o accesorio.
11. Active **Auto Report** si el dispositivo conectado espera que el radio envíe actualizaciones de forma automática.

## Función de cada control

| Control | Descripción |
|---|---|
| Cables list / Status | Muestra todos los adaptadores USB detectados por el radio. Status indica Plugged o Unplugged para cada entrada. |
| Name: | Etiqueta asignada por el usuario para esta entrada de cable. |
| Enabled | Activa o desactiva la asignación del cable. |
| Speed | Velocidad de baudios serie para este cable. |
| Data Bits | Número de bits de datos por trama serie. |
| Parity | Configuración de paridad para la conexión serie. |
| Stop Bits | Número de bits de parada por trama serie. |
| Flow | Modo de control de flujo. |
| Source | Selecciona qué evento o dato del radio maneja la salida de este cable. |
| Auto Report | Cuando está activo, el radio envía actualizaciones al cable de forma automática, sin necesidad de solicitud. |
| BCD Type | Selecciona el esquema de codificación BCD (aplica al tipo de cable BCD). |
| Polarity | Invierte el nivel lógico activo en la salida (aplica a los tipos de cable BCD y PTT). |
| Bit Configuration (0-7) | Asigna una función a cada uno de los ocho bits de salida (aplica al tipo de cable bit). |

## Consejos

- También puede acceder a la pestaña USB Cables desde `Settings > Radio Setup...` y seleccionando **USB Cables** en la barra de pestañas.
- Si un cable aparece como Unplugged, conéctelo al puerto USB del radio y vuelva a abrir el diálogo, o espere a que el estado se actualice.
- Los cables CAT permiten que software externo de registro y de concurso controle el VFO y el modo del radio a través de una conexión serie virtual.

## Solución de problemas

- **El cable no aparece en la Cables list** — El adaptador debe estar conectado al hardware del radio, no a la PC. Confirme que el adaptador esté conectado al puerto USB del FLEX-8600 y luego vuelva a abrir el diálogo.
- **Status muestra Unplugged aunque el cable esté conectado** — Vuelva a conectar el adaptador USB al radio y espere un momento para que el firmware del radio lo detecte antes de reabrir el diálogo.
- **Las salidas BCD o bit están invertidas** — Cambie el valor de **Polarity** para esa entrada de cable.

## Temas relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serie de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
