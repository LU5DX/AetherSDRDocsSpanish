# Asignar un cable USB como CAT, BCD, bit o PTT

La pestaña USB Cables en Radio Setup permite asignar adaptadores seriales USB físicos conectados al FLEX-8600 a roles de control específicos: CAT, BCD, bit o PTT. Use esta página cuando desee que un dispositivo externo o un controlador de amplificador se comunique con la radio mediante un cable serial USB.

## Antes de comenzar

- Conecte el adaptador serial USB al FLEX-8600 antes de abrir el diálogo. La radio debe detectar el cable para que aparezca en la lista.
- AetherSDR debe estar conectado a la radio.

## Pasos

1. Abra `Settings > USB Cables...`.
   El diálogo Radio Setup se abre con la pestaña **USB Cables** ya seleccionada.
   Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Localice su cable en el indicador **Cables list / Status**. Cada cable detectado aparece en la lista con su tipo y un estado **Plugged** o **Unplugged**.
3. Seleccione el cable que desea configurar haciendo clic en él en la lista.
4. Establezca el rol del cable y los parámetros seriales mediante los controles que aparecen para el cable seleccionado:
   - **Name:** — identifica el cable.
   - **Enabled** — habilita o deshabilita esta asignación de cable.
   - **Speed** — velocidad en baudios del puerto serial.
   - **Data Bits** — número de bits de datos.
   - **Parity** — configuración de paridad.
   - **Stop Bits** — número de bits de parada.
   - **Flow** — método de control de flujo.
   - **Source** — la fuente de la radio que este cable monitorea.
   - **Auto Report** — controla el reporte automático de estado.
   - **BCD Type** — se aplica cuando el tipo de cable es BCD; establece la variante de codificación BCD.
   - **Polarity** — polaridad de la señal (normal o invertida).
   - **Bit Configuration (0-7)** — se aplica cuando el tipo de cable es bit; asigna funciones individuales a cada bit.
5. Cierre el diálogo al terminar. Los ajustes se aplican a la radio de inmediato a medida que realiza cambios.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Cables list / Status** | Lista de solo lectura de los cables USB detectados y su estado actual **Plugged** o **Unplugged**. |
| **Name:** | Etiqueta que identifica el cable. |
| **Enabled** | Activa o desactiva la asignación de este cable en la radio. |
| **Speed** | Velocidad en baudios del puerto serial para el cable. |
| **Data Bits** | Longitud de palabra para el enlace serial. |
| **Parity** | Modo de verificación de paridad para el enlace serial. |
| **Stop Bits** | Número de bits de parada para el enlace serial. |
| **Flow** | Selección de control de flujo por hardware o software. |
| **Source** | Qué slice de la radio o fuente de señal reporta este cable. |
| **Auto Report** | Si la radio envía automáticamente actualizaciones de estado por este cable. |
| **BCD Type** | Variante de codificación BCD; activo solo para cables de tipo BCD. |
| **Polarity** | Establece la polaridad lógica de la señal de salida. |
| **Bit Configuration (0-7)** | Asigna una función a cada una de las ocho salidas de bit; activo solo para cables de tipo bit. |

## Solución de problemas

- **El cable no aparece en la lista** — La radio enumera los cables en el momento de la conexión. Desconecte y vuelva a conectar el adaptador USB, luego cierre y vuelva a abrir `Settings > USB Cables...` para actualizar la lista. Confirme que el adaptador esté conectado al puerto USB de la radio y no a la PC anfitriona.
- **El estado muestra Unplugged** — El cable está configurado pero actualmente no está físicamente presente. Vuelva a conectar el adaptador a la radio.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serial de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
