# Asignar un cable USB como CAT, BCD, bit o PTT

La pestaña USB Cables permite asignar un adaptador serie USB físico conectado a su FLEX-8600 a uno de cuatro tipos de cable: CAT, BCD, bit o PTT. Úsela para controlar equipos externos como amplificadores, conmutadores de antena o software de registro mediante los puertos USB del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña USB Cables requiere una conexión activa con el radio.
- El adaptador serie USB debe estar físicamente conectado al FLEX-8600 antes de abrir este diálogo. Los cables aparecen en la lista solo cuando el radio los detecta.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña **USB Cables**. Como alternativa, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Localice su cable en la lista **Cables list**. La columna **Status** muestra **Plugged** o **Unplugged** para cada cable detectado.
3. Seleccione el cable que desea configurar haciendo clic en su fila de la lista.
4. Establezca **Name:** con una etiqueta que identifique este cable en su estación.
5. Establezca **Enabled** en el estado activo para poner el cable en servicio.
6. Configure **Speed**, **Data Bits**, **Parity**, **Stop Bits** y **Flow** para que coincidan con la velocidad en baudios y el encuadre que espera el equipo conectado.
7. Establezca **Source** en el slice o fuente de radio que controla la salida del cable.
8. Si el tipo de cable es BCD, configure **BCD Type** y **Auto Report** según lo requiera su equipo.
9. Si el tipo de cable es bit, configure **Bit Configuration (0-7)** y **Polarity** para cada línea de bit.
10. Si el tipo de cable es PTT, establezca **Polarity** para que coincida con el requisito de nivel activo alto o activo bajo del dispositivo conectado.
11. Cierre el diálogo. Los ajustes se aplican al radio de inmediato al cambiar cada control.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Cables list / Status** | Lista todos los adaptadores serie USB que el radio ha detectado, con estado **Plugged** o **Unplugged** para cada uno. |
| **Name:** | Etiqueta asignada por el usuario para esta entrada de cable. |
| **Enabled** | Activa el cable. El cable no lleva señal mientras está desactivado. |
| **Speed** | Velocidad en baudios serie para el cable. |
| **Data Bits** | Número de bits de datos por carácter. |
| **Parity** | Esquema de paridad (None, Even, Odd, etc.). |
| **Stop Bits** | Número de bits de parada. |
| **Flow** | Selección de control de flujo por hardware o software. |
| **Source** | El slice de radio o fuente de señal enrutada a este cable. |
| **Auto Report** | Cuando está activado, el radio envía cambios de estado al cable sin necesidad de consulta. |
| **BCD Type** | Selecciona el formato de codificación BCD. Se aplica solo a los cables de tipo BCD. |
| **Polarity** | Invierte el estado activo de la línea de salida. Se aplica a los tipos de cable bit y PTT. |
| **Bit Configuration (0-7)** | Asigna una función a cada una de las ocho líneas de bit del cable. Se aplica solo a los cables de tipo bit. |

## Solución de problemas

- **El cable no aparece en la lista** — El radio no ha detectado el adaptador USB. Verifique que el adaptador esté conectado al FLEX-8600 (no al PC host) y que la columna **Status** muestre **Plugged**. Si el estado permanece en **Unplugged**, intente desconectar y volver a insertar el adaptador, luego cierre y vuelva a abrir el diálogo.
- **El cable aparece en la lista pero no produce salida** — Confirme que **Enabled** esté activo para ese cable. Verifique también que **Speed**, **Parity** y **Stop Bits** coincidan con los requisitos del equipo conectado.
- **La línea PTT permanece activada o nunca se activa** — Revise el ajuste de **Polarity**. Cambiar **Polarity** invierte el nivel activo.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serie de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
- [Establecer la potencia TX máxima por banda y el modo de ajuste](set-per-band-tx-max-power-and-tune-mode.md)
