# Identificar qué antenas no pueden transmitir en la banda actual (ámbar o apagadas)

El applet Antenna Genius asigna un color a cada botón de antena para indicar si esa antena puede transmitir en la banda actual. Verificar los colores de los botones antes de transmitir le indica de inmediato cuáles antenas son aptas para TX y cuáles son solo de recepción o no tienen permiso alguno en esa banda.

## Antes de comenzar

- El applet Antenna Genius debe estar abierto y conectado. La etiqueta de estado debe mostrar "Connected — \<name\> v\<version\>".
- El radio debe estar sintonizado en la banda que desea verificar; los colores de los botones se actualizan automáticamente cuando cambia la banda.

## Pasos

1. Haga clic en el botón "AG" de la barra lateral derecha para abrir el applet Antenna Genius.
2. Observe los botones de antena en la cuadrícula de Port A (y Port B, si está visible).
3. Lea el color de cada botón:
   - **Azul** — la antena tiene permiso de TX y RX en la banda actual.
   - **Ámbar** — la antena tiene permiso solo de RX en la banda actual; no está permitido transmitir con esta antena.
   - **Apagado (sin iluminar)** — la antena no tiene ningún permiso en la banda actual.
4. Seleccione un botón azul para la operación normal de TX+RX. Evite los botones ámbar y apagados si tiene intención de transmitir.

## Qué hace cada control

| Control | Color / estado | Significado |
|---|---|---|
| Botones de antena de Port A | Azul (marcado) | Seleccionado; TX y RX permitidos en la banda actual |
| Botones de antena de Port A | Ámbar (marcado) | Seleccionado; solo RX en la banda actual |
| Botones de antena de Port A | Apagado | No seleccionado o sin permiso en la banda actual |
| Botones de antena de Port B | Los mismos tres estados | El mismo significado para Port B |
| Etiquetas de banda de Port A / Port B | Nombre de banda o "—" | Muestra la banda contra la cual AetherSDR está evaluando los permisos actualmente |

## Sugerencias

- Los colores de los botones se actualizan en tiempo real cada vez que el radio cambia de banda, por lo que no es necesario volver a abrir el applet después de sintonizar.
- Si Port B está oculto, el Antenna Genius conectado reporta solo un puerto de radio; todos los botones de antena se encuentran en Port A.
- Un botón de antena que aparece apagado porque ya está seleccionado en el otro puerto es una condición de bloqueo independiente. Consulte [Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto están bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md) para obtener más detalles.

## Solución de problemas

- **Todos los botones aparecen apagados y la etiqueta de banda muestra "—"** — AetherSDR no puede determinar la banda actual. Confirme que el radio esté conectado y sintonizado en una banda de radioaficionado reconocida.
- **Los colores no cambian después de sintonizar** — Verifique que la etiqueta de estado siga mostrando "Connected — \<name\> v\<version\>". Si la conexión se interrumpió, haga clic en "Disconnect" y luego en "Connect" para restablecerla.

## Relacionados

- [Descripción general de Antenna Genius](overview.md)
- [Seleccionar una antena para Port A o Port B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Intercambiar radios que comparten el AG (las antenas en uso por el otro puerto están bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
