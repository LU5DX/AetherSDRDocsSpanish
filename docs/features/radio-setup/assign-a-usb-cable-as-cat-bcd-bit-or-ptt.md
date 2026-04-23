# Asignar un cable USB como CAT, BCD, bit o PTT

La pestaña USB Cables permite asignar adaptadores serie USB físicos conectados al radio Flex a un tipo de cable específico — CAT, BCD, bit o PTT — y configurar los parámetros serie por cable. Utilice esta función cuando necesite que el radio controle equipos externos, como amplificadores, decodificadores de banda o software de registro, a través de un puerto serie USB.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña USB Cables solo está disponible mientras hay una conexión de radio activa.
- El cable USB debe estar físicamente conectado al puerto USB del radio Flex. Los cables que no se detectan aparecen con el estado "Unplugged" en la lista.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña USB Cables. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Revise el indicador **Cables list / Status**. Cada cable USB detectado aparece en la lista con su tipo y un estado Plugged o Unplugged.
3. Seleccione el cable que desea configurar de la lista.
4. En **Name:**, introduzca una etiqueta descriptiva para el cable.
5. Active **Enabled** para habilitar el cable.
6. Configure **Speed**, **Data Bits**, **Parity**, **Stop Bits** y **Flow** para que coincidan con los parámetros serie requeridos por su equipo externo.
7. En **Source**, seleccione la fuente de señal que seguirá este cable.
8. Para cables BCD, configure **BCD Type** y ajuste **Polarity** según sea necesario.
9. Para cables bit, configure **Bit Configuration (0-7)** y **Polarity**.
10. Para cables CAT, configure **Auto Report** para controlar si el radio envía actualizaciones de frecuencia de forma automática.
11. Para cables PTT, configure **Polarity** para que coincida con el sentido de activación de su equipo.
12. Cierre el diálogo. Los ajustes se aplican al radio de inmediato.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Cables list / Status** | Muestra todos los cables USB detectados por tipo. Indica Plugged o Unplugged para cada uno. |
| **Name:** | Etiqueta asignada por el usuario para el cable. |
| **Enabled** | Activa el cable. |
| **Speed** | Velocidad de baudios serie para este cable. |
| **Data Bits** | Número de bits de datos por trama. |
| **Parity** | Configuración de paridad para el enlace serie. |
| **Stop Bits** | Número de bits de parada por trama. |
| **Flow** | Selección de control de flujo por hardware o software. |
| **Source** | Selecciona qué señal de radio o slice controla la salida de este cable. |
| **Auto Report** | Cuando está activo, el radio envía actualizaciones de frecuencia y modo de forma automática (cables CAT). |
| **BCD Type** | Selecciona el formato de codificación BCD (solo cables BCD). |
| **Polarity** | Invierte el nivel lógico activo en la salida del cable. |
| **Bit Configuration (0-7)** | Asigna bits de salida individuales a estados del radio (solo cables bit). |

## Consejos

- Puede acceder a la misma pestaña desde `Settings > Radio Setup...` y luego haciendo clic en **USB Cables**, si necesita cambiar a otra pestaña (como TX o Peripherals) durante la misma sesión sin volver a abrir el diálogo.
- El estado Plugged o Unplugged en **Cables list / Status** se actualiza de forma dinámica. Si un cable no aparece en la lista, compruebe la conexión USB física al radio y vuelva a abrir la pestaña.

## Temas relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serie de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
- [Conectar TGXL, PGXL o Antenna Genius por IP](../../getting-started/setup/connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
