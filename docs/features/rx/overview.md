# Descripción general de los controles RX

El applet RX Controls le ofrece control por slice sobre todos los parámetros de recepción: modo, frecuencia, selección de antena, ancho de filtro, CAG, audio, squelch, RIT/XIT y configuración del repetidor FM. Ábralo siempre que necesite configurar cómo un slice recibe o transmite.

## Cómo funciona

El applet RX siempre está presente en el panel de applets (barra lateral derecha). Alterne su visibilidad con el botón RX del panel. Cuando el equipo admite más de un slice, aparece una fila de pestañas de slice (A hasta H) en la parte superior; al hacer clic en una pestaña, el applet queda vinculado a ese slice. Todos los controles que se encuentran debajo de la fila de pestañas afectan únicamente al slice seleccionado en ese momento.

Los preajustes de ancho de filtro son la única configuración que persiste entre sesiones, almacenada bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo del equipo y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del slice

| Control | Predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Selecciona qué slice controla el applet. La fila de pestañas se oculta cuando el equipo tiene un solo slice. Los bordes de los botones y los fondos activos siguen el color por slice definido en SliceColorManager. Al desconectarse, `clearSliceButtons()` elimina todos los botones de pestaña generados y restaura la insignia de slice estática. Las conexiones de clic de los botones de slice están protegidas contra manejadores de señal duplicados entre reconexiones (v0.9.5.1, #2254). |
| Insignia de slice | A | Muestra la letra del slice activo. El color lo gestiona SliceColorManager; los colores personalizados por slice persisten entre sesiones y se reflejan aquí, en los botones de pestaña de slice, los widgets VFO y las tiras de medidores. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia provenientes del panadapter y de otras fuentes. |
| TX (insignia) | — | Haga clic para designar este slice como el slice de TX. |

### Frecuencia y modo

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Selector de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, NT, RTTY (+ RADE si el indicador de compilación HAVE_RADE está activado) | Establece el modo del slice. Al cambiar el modo, los preajustes de filtro y paso se reconfiguran automáticamente. |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para entrar al modo de edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 450.000 MHz con XVTR) | Introduzca una frecuencia en MHz y presione Enter para sintonizar y recentrar. Presione Escape para cancelar y restaurar la frecuencia anterior. |
| STEP | 100 Hz | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones triangulares izquierdo/derecho o use la rueda del ratón para ciclar entre los tamaños de paso. Los pasos disponibles cambian con el modo. |

### Selección de antena

| Control | Predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú con las antenas disponibles de la lista de antenas del equipo. Seleccione una para establecer la antena RX de este slice. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú con las antenas habilitadas para TX. Los puertos solo de recepción (cuyos nombres comienzan con `RX`) quedan excluidos. La etiqueta es roja. |

### Filtro

| Control | Predeterminado / rango | Clave de configuración | Comportamiento |
|---|---|---|---|
| Preajustes de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como preajuste. Los botones se ocultan en los modos FM, NFM y DFM. Los preajustes se almacenan como un valor de ancho simple o como un par de paso de banda `lo:hi`; ambos formatos se leen y escriben correctamente (v0.9.5.1, #2259). |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda de filtro actual. Se actualiza al aplicar un preajuste o al arrastrar el paso de banda. Solo lectura. |
| Widget de paso de banda del filtro | — | — | Arrastre el borde inferior o superior para establecer un paso de banda de filtro personalizado. |

### CAG (AGC)

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de CAG | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta de la CAG. Se oculta en los modos de la familia FM. |
| Umbral de CAG | 65 | 0–100 | Establece el umbral de la CAG. Cuando el modo de CAG está en Off, ajusta el nivel CAG-desactivada en su lugar. |

### Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (con audio) | — | Silencia o reactiva la salida de audio del slice. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. |
| Paneo L / R | 50 | 0–100 | Panea el audio entre el canal izquierdo (0) y el derecho (100). Haga doble clic para restablecer al centro (50). |
| SQL | — | — | Activa el squelch al nivel establecido por el control deslizante de squelch. Deshabilitado y forzado a apagado en los modos DIGU, DIGL, NT, CW y CWL. |
| Nivel de squelch | 20 | 0–100 | Establece el umbral de squelch. Solo tiene efecto cuando SQL está activado. |

### RIT y XIT

| Control | Predeterminado | Comportamiento |
|---|---|---|
| RIT | apagado | Activa o desactiva la sintonía incremental de recepción (RIT). |
| RIT 0 | — | Pone a cero el desplazamiento RIT de inmediato. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | apagado | Activa o desactiva la sintonía incremental de transmisión (XIT). |
| XIT 0 | — | Pone a cero el desplazamiento XIT de inmediato. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Reducción de ruido y botones de filtro DSP

Los siguientes botones de filtro DSP son visibles en los modos que no son FM. La disponibilidad de los botones depende de la serie del equipo.

| Botón | Disponibilidad | Comportamiento |
|---|---|---|
| NR | Todas las series | Activa la reducción de ruido. Se oculta en los modos de la familia FM. |
| NR2 | Todas las series | Activa la reducción de ruido modo 2. Se oculta en los modos de la familia FM. |
| NB | Todas las series | Activa el blanqueador de ruido. Se oculta en los modos de la familia FM. |
| NRL | Todas las series (incluida la serie 6000) | Activa la reducción de ruido (algoritmo NRL). Se oculta en los modos de la familia FM. Disponible en equipos de la serie 6000 a partir de V0.9.4; anteriormente requería firmware de la serie 8000. |
| NRS | Solo serie 8000 | Activa la reducción de ruido NRS. Se oculta en los modos de la familia FM. |
| RNN | Solo serie 8000 | Activa la reducción de ruido RNN. Se oculta en los modos CW y de la familia FM. |
| NRF | Solo serie 8000 | Activa la reducción de ruido NRF. Se oculta en los modos de la familia FM. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando el CW full break-in está activo. Se controla desde el applet CW; solo lectura aquí. |

### Controles de repetidor FM

Estos controles son visibles únicamente cuando el modo del slice es FM, NFM o DFM.

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | Selecciona si se envía un tono CTCSS durante la transmisión. |
| Valor del tono CTCSS | — | 67.0–254.1 Hz (41 tonos estándar EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Solo está activo cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento hacia abajo) | — | — | Establece la frecuencia TX por debajo de la frecuencia RX según la cantidad de desplazamiento. |
| Simplex | marcado | — | Establece TX y RX en la misma frecuencia (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | Establece la frecuencia TX por encima de la frecuencia RX según la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar un par de repetidor invertido. |

## Pestaña Peripherals — conexión IP manual

La pestaña Peripherals del cuadro de diálogo Radio Setup permite conectarse manualmente a dispositivos externos mediante dirección IP. Las siguientes filas están disponibles.

### Antenna Genius (AG) — fila 3

Conecta a un dispositivo Antenna Genius en la IP y puerto especificados. El estado "Connected" se muestra únicamente cuando el dispositivo conectado es un Antenna Genius propiamente dicho. Si la conexión es en realidad a un ShackSwitch, la fila AG aparece como desconectada y la fila ShackSwitch aparece como conectada en su lugar.

### ShackSwitch — fila 4 (agregado en V0.9.4)

| Control | Clave de configuración | Predeterminado | Comportamiento |
|---|---|---|---|
| Campo de dirección IP | `SS_ManualIp` | — | Introduzca la dirección IP del ShackSwitch. |
| Campo de puerto | `SS_ControlPort` | 9007 | Puerto utilizado para el protocolo de control AG. Siempre se conecta en el puerto 9007 independientemente del valor introducido. |
| Botón Connect | — | — | Conecta al ShackSwitch en la IP especificada por el puerto 9007 usando el protocolo de control AG. |
| Botón Disconnect | — | — | Desconecta del ShackSwitch. |
| Estado Connected | — | — | Muestra "Connected" únicamente cuando la conexión activa es a un dispositivo ShackSwitch. |
| Botón ⚙ Web UI | `SS_ManualIp`, `SS_WebPort` | puerto 5000 | Abre la interfaz web del ShackSwitch en su navegador. Usa la dirección del par activo si hay un ShackSwitch conectado en ese momento. Usa `SS_WebPort` de la configuración si está definido y es mayor que 1024; de lo contrario, recurre al `webPort` anunciado por el dispositivo si es válido (>1024) y, finalmente, usa por defecto el puerto 5000. No realiza ninguna acción si no se puede determinar ninguna dirección IP. |

Tanto la fila AG como la fila ShackSwitch comparten la conexión subyacente de `AntennaGeniusModel`. Conectarse a uno se reflejará como desconectado en el otro.

## Accesores del AppletPanel y métodos de visibilidad

Los siguientes métodos de acceso y ayudantes de visibilidad están disponibles en `AppletPanel`. Se usan internamente y en el código que coordina la presencia de dispositivos con el estado de los applets.

### Accesores de applets

| Método | Devuelve | Descripción |
|---|---|---|
| `tciApplet()` | `TciApplet*` | Devuelve la instancia del applet TCI. |
| `daxIqApplet()` | `DaxIqApplet*` | Devuelve la instancia del applet DAX IQ. |
| `agApplet()` | `AntennaGeniusApplet*` | Devuelve la instancia del applet Antenna Genius. |
| `ssApplet()` | `ShackSwitchApplet*` | Devuelve la instancia del applet ShackSwitch. Agregado en V0.9.4. |
| `meterApplet()` | `MeterApplet*` | Devuelve la instancia del applet de medidores. |
| `mqttApplet()` | `MqttApplet*` | Devuelve la instancia del applet MQTT. Disponible únicamente en compilaciones HAVE_MQTT. |

### Ayudantes de visibilidad
