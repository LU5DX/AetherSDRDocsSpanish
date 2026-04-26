# Descripción general del Ecualizador Paramétrico Aetherial (TX / RX)

El Ecualizador Paramétrico Aetherial es un ecualizador paramétrico del lado del cliente que procesa el audio de forma independiente en las rutas de transmisión y recepción. Úselo para dar forma a su señal transmitida o a su audio recibido sin modificar ningún ajuste de DSP del equipo de radio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un equipo de radio para la configuración, pero el analizador FFT en tiempo real solo muestra señal cuando hay audio circulando.
- Los paneles del EQ ("Aetherial TX EQ" y "Aetherial RX EQ") permanecen ocultos hasta que la etapa de EQ correspondiente se habilite desde el widget CHAIN o desde el editor flotante. Habilite primero la etapa de EQ si no ve los paneles.

## Cómo funciona

AetherSDR instancia dos copias independientes del EQ: una vinculada permanentemente a la ruta TX ("Aetherial TX EQ") y otra vinculada permanentemente a la ruta RX ("Aetherial RX EQ"). Cada una reside dentro del contenedor padre Aetherial Audio (TXDSP). No existe un selector dentro del panel para cambiar entre rutas — cada panel queda bloqueado a su lado desde el momento de su creación.

**Paneles applet (vista acoplada)**

Cada panel contiene un único área de analizador y curva de solo lectura. El panel muestra la respuesta de EQ combinada de su ruta y una superposición del analizador FFT en tiempo real. No es posible editar bandas directamente en el panel; toda la edición de bandas se realiza en el editor flotante.

**Editor flotante**

Al hacer doble clic en la etapa de EQ en el widget CHAIN se abre el editor flotante sin marco, titulado "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX" según el lado que haya abierto. Se reutiliza una única ventana de editor para ambos lados; su título se actualiza para reflejar la ruta activa.

El editor flotante contiene:

- Una barra de ayuda de interacción en la parte superior que describe los gestos de arrastre.
- Un selector de familia de filtros (véase la tabla a continuación).
- Una fila de iconos, un lienzo editable y una fila de parámetros para agregar, eliminar y ajustar bandas.
- Un fader de salida a la derecha con un medidor de nivel y lectura en dB.

El analizador FFT del editor se ejecuta a 25 Hz mientras el editor está visible y se detiene cuando se cierra.

**Bypass**

El bypass de una etapa de EQ se realiza desde el widget CHAIN, no desde el interior del panel ni desde el editor flotante.

## Qué hace cada control

### Controles del panel applet

| Control | Descripción | Ajuste persistido |
|---|---|---|
| Área de analizador / curva | Visualización de solo lectura, 110 px de alto. Muestra la curva de respuesta de EQ combinada y una superposición del analizador FFT en tiempo real para la ruta de este panel. | — |

### Controles del editor flotante

| Control | Valor predeterminado | Valores válidos | Ajuste persistido |
|---|---|---|---|
| Familia de filtros | Butterworth | Butterworth, Chebyshev, Bessel, Elliptic | `ClientEqTxBands` / `ClientEqRxBands` (guardado junto con los datos de banda) |
| Fader de salida | — | Ganancia lineal, mostrada en dB | `ClientEqTxBands` / `ClientEqRxBands` |
| EQ RX habilitado | — | Activo / en bypass | `ClientEqRxEnabled` |
| EQ TX habilitado | — | Activo / en bypass | `ClientEqTxEnabled` |
| Definiciones de banda (RX) | — | Agregadas/eliminadas de forma interactiva en el lienzo | `ClientEqRxBands` |
| Definiciones de banda (TX) | — | Agregadas/eliminadas de forma interactiva en el lienzo | `ClientEqTxBands` |

**Opciones de familia de filtros**

| Opción | Comportamiento |
|---|---|
| Butterworth | Banda de paso máximamente plana |
| Chebyshev | Transición más pronunciada, rizado de 1 dB en la banda de paso |
| Bessel | Fase lineal, caída más suave |
| Elliptic | Transición más pronunciada, rizado en ambas bandas |

El selector de familia de filtros se aplica al cálculo en cascada de HP/LP. Los filtros de shelving y peak utilizan su topología nativa de segundo orden independientemente de este ajuste.

**Indicador de respuesta de EQ combinada**

Muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas para la ruta del panel. Se muestra plana cuando no hay bandas activas o cuando todas las bandas tienen una ganancia de 0 dB, y con forma cuando las bandas contribuyen a la respuesta.

**Superposición del analizador en tiempo real**

Muestra una FFT en tiempo real del audio que circula por la ruta del panel. Inactivo cuando no hay audio circulando; activo cuando hay audio presente.

## Consejos

- Haga clic derecho en la barra de título del subcontenedor "Aetherial TX EQ" o "Aetherial RX EQ" para flotar, extraer u ocultar el panel.
- En el lienzo del editor flotante: arrastre una banda peak o de shelving para ajustar la frecuencia y la ganancia; mantenga presionada la tecla Shift mientras arrastra para ajustar el Q. Arrastre una banda HP o LP para ajustar la frecuencia y el Q. Haga clic en el ícono de una banda para ciclar entre los tipos de filtro.
- El fader de salida del editor flotante controla la ganancia maestra de esa ruta de EQ después de que todas las bandas se han combinado.

## Solución de problemas

- **El panel "Aetherial TX EQ" o "Aetherial RX EQ" no es visible** — El panel permanece oculto hasta que la etapa de EQ correspondiente esté habilitada. Habilite la etapa desde el widget CHAIN o desde el editor flotante.
- **El analizador FFT en tiempo real no muestra nada** — El audio debe estar circulando por la ruta para que el analizador muestre señal. Confirme que el equipo de radio esté conectado y que el enrutamiento de audio esté activo para esa ruta.
- **El título del editor flotante no corresponde al lado que desea editar** — El editor es compartido entre ambas rutas. Abra el editor haciendo doble clic en la etapa de EQ correcta (TX o RX) en el widget CHAIN para cambiarlo a ese lado.

## Relacionados

- [Bypass de la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Inspeccionar la curva de EQ TX y el espectro en tiempo real](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ RX y el espectro en tiempo real](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Abrir el editor sin marco para agregar, eliminar y ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Verificar que la curva combinada coincida con su objetivo](verify-the-summed-curve-matches-your-mental-target.md)
