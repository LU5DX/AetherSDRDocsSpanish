# Descripción general del sintonizador

El applet del sintonizador proporciona control y monitoreo para el sintonizador de antena externo 4O3A Tuner Genius XL.

## Requisitos previos

- Debe haber un 4O3A Tuner Genius XL presente en su red.
- El TGXL debe ser detectado automáticamente por AetherSDR o configurado manualmente.

## Acceso al applet del sintonizador

Haga clic en el botón **TUN** en la barra lateral derecha para abrir o cerrar el applet del sintonizador. El applet permanece oculto hasta que se detecta un TGXL.

## Disposición del applet

El applet del sintonizador contiene:

- **Medidor de potencia directa** (Fwd Pwr) — muestra la potencia directa en vatios
- **Medidor de ROE** — muestra la relación de ROE (1.0–3.0)
- **Barras de relés** (C1, L, C2) — muestran las posiciones actuales del banco de relés
- **Botón TUNE** — inicia un ciclo de autosintonía
- **Botón OPERATE/BYPASS/STANDBY** — alterna el modo del sintonizador
- **Botones ANT 1/2/3** — selección del puerto de antena (solo visible cuando la conexión directa al TGXL está activa)

## Conexiones de red

El Tuner Genius XL puede conectarse a AetherSDR mediante dos vías:

1. **Vía del firmware de la radio** — El TGXL se comunica a través de la conexión de red del FlexRadio. Esta es la opción predeterminada.
2. **Conexión directa (puerto 9010)** — AetherSDR se conecta directamente al TGXL. Esto permite:
   - Ajuste con la rueda del ratón de los relés C1/L/C2
   - Selección del conmutador de antena ANT 1/2/3
   - Omitir la vía del firmware de la radio para los comandos de autosintonía

Configure la conexión en **Radio Setup → Tuner**.

## Páginas relacionadas

- [Ponga el sintonizador en OPERATE, BYPASS o STANDBY](#)
- [Monitoree la potencia directa y la ROE en el applet del sintonizador](#)
- [Ejecute una autosintonía en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Lea la ROE inmediatamente después de una sintonía](read-swr-immediately-after-a-tune.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)

---

# Ponga el sintonizador en OPERATE, BYPASS o STANDBY

Use el botón OPERATE en el applet del sintonizador para alternar el 4O3A Tuner Genius XL entre sus tres estados de relé: OPERATE, BYPASS y STANDBY.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet del sintonizador permanece oculto hasta que se detecta un Tuner Genius XL.
- El botón de bandeja TUN debe estar disponible en la barra lateral derecha, lo que indica que el TGXL ha sido detectado.

## Pasos

1. Haga clic en el botón de bandeja TUN en la barra lateral derecha para abrir el applet del sintonizador.
2. Localice el botón OPERATE en el área inferior derecha del applet.
3. Haga clic en OPERATE para avanzar al siguiente estado. Cada clic avanza un paso:
   - OPERATE → BYPASS
   - BYPASS → STANDBY
   - STANDBY → OPERATE

## Qué hace cada control

| Botón | Color cuando está activo | Significado |
|---|---|---|
| OPERATE | Verde | Los relés del sintonizador están en el circuito y activos. |
| BYPASS | Naranja | El sintonizador está energizado pero la red de adaptación está omitida. |
| STANDBY | Predeterminado (depende del tema) | El sintonizador no está operando. |

La etiqueta y el color del botón se actualizan inmediatamente cuando el TGXL confirma el cambio de estado.

## Consejos

- El botón siempre muestra el estado **actual**, no el siguiente. Una etiqueta OPERATE en verde significa que el sintonizador ya está en OPERATE.
- Un solo clic desde STANDBY devuelve el sintonizador a OPERATE y restaura el color verde. No es necesario pasar por BYPASS para volver a OPERATE.

## Solución de problemas

- **El botón de bandeja TUN no es visible** — El applet del sintonizador permanece oculto hasta que se detecta un Tuner Genius XL en la red. Verifique que el TGXL esté encendido y conectado. Consulte [Descripción general del sintonizador](overview.md).
- **La etiqueta del botón no cambia después de hacer clic** — La etiqueta se actualiza solo cuando el TGXL confirma el nuevo estado. Si la etiqueta permanece igual, verifique la conexión entre AetherSDR y el TGXL.

## Relacionado

- [Descripción general del sintonizador](overview.md)
- [Ejecute una autosintonía en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Lea la ROE inmediatamente después de una sintonía](read-swr-immediately-after-a-tune.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)

---

# Monitoree la potencia directa y la ROE en el applet del sintonizador

El applet del sintonizador muestra los medidores de potencia directa y ROE reportados por el 4O3A Tuner Genius XL.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio y el TGXL debe ser detectado en la red.

## Pasos

1. Haga clic en el botón de bandeja TUN en la barra lateral derecha para abrir el applet del sintonizador.
2. Localice el medidor **Fwd Pwr** en la parte superior del applet. Muestra la potencia directa en vatios.
3. Localice el medidor **SWR** debajo de este. Muestra la relación de ROE.

## Escala de los medidores

La escala del medidor de potencia directa depende de su configuración de hardware:

| Configuración | Rango de escala |
|---|---|
| Sin amplificador | 0–200 W |
| Amplificador Aurora | 0–600 W |
| Amplificador PGXL | 0–2000 W |

El medidor de ROE varía de 1.0 a 3.0. Los valores superiores a 2.5 se muestran en rojo para indicar una condición de ROE alta.

## Mejoras de rendimiento de los medidores en v26.8.4

La escala del medidor de potencia directa ahora solo se actualiza cuando la configuración de hardware cambia realmente (por ejemplo, al conectar o desconectar un PGXL). Anteriormente, la escala del medidor se reaplicaba en cada actualización de estado de la radio, lo que podía causar repintados innecesarios de la pantalla y un parpadeo visible. Este cambio mejora la capacidad de respuesta de la interfaz, especialmente durante actualizaciones rápidas de estado mientras se transmite.

## Cambios de comportamiento importantes en v26.6.3

- **El medidor de ROE ahora se restablece a 1.0 cuando la potencia directa es inferior a 5 W.** El TGXL reporta una ROE de 99.9 en reposo cuando no hay señal incidente. Para evitar que esto sature el medidor, la barra de ROE se restablece a 1.0 siempre que la potencia directa cae por debajo de 5 W. Esto coincide con el umbral utilizado para la visualización de la etiqueta de ROE.
- **Nombres accesibles agregados** para soporte de lectores de pantalla: "Forward power", "SWR", "Tuner capacitor C1", "Tuner inductor L", "Tuner capacitor C2".

## Solución de problemas

- **El medidor de ROE muestra 1.0 incluso al transmitir** — Verifique que la potencia directa supere los 5 W. El medidor de ROE solo muestra el valor medido cuando la potencia directa es de al menos 5 W.
- **El medidor de potencia directa parpadea durante las actualizaciones de estado** — Si está ejecutando una versión anterior a v26.8.4, actualice a v26.8.4 o posterior. La escala del medidor ahora solo se recalcula cuando cambia su configuración de hardware.

## Relacionado

- [Ponga el sintonizador en OPERATE, BYPASS o STANDBY](#)
- [Ejecute una autosintonía en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)

---

# Ejecute una autosintonía en el TGXL externo

Use el botón TUNE en el applet del sintonizador para iniciar un ciclo de sintonización automática en el 4O3A Tuner Genius XL.

## Antes de comenzar

- El applet del sintonizador debe estar abierto. El TGXL debe ser detectado en la red.
- Asegúrese de que su radio esté transmitiendo a un nivel de potencia adecuado para la sintonía (típicamente 5–100 W).
- El sintonizador debe estar en modo OPERATE. El botón TUNE no responderá en modo BYPASS o STANDBY.

## Pasos

1. Haga clic en el botón **TUNE** en el applet del sintonizador.
2. La etiqueta del botón cambia a **TUNING...** y se pone roja mientras el ciclo de sintonía está en curso.
3. Cuando la sintonía se completa, la etiqueta del botón parpadea mostrando **SWR x.xx** durante aproximadamente 2.5 segundos, mostrando la ROE posterior a la sintonía.
4. Después del parpadeo, el botón vuelve a su etiqueta **TUNE** predeterminada.

## Comportamiento de la conexión directa (v0.9.2.1 y posteriores)

Cuando se configura una conexión directa al TGXL (puerto 9010) en Radio Setup → Tuner, el comando de autosintonía se envía directamente al TGXL, omitiendo la vía del firmware de la radio. Esto resuelve los problemas de sintonía que algunos usuarios experimentaron con el firmware 4.2 de FlexRadio.

Cuando no se configura una conexión directa, el comando de autosintonía se enruta a través de la vía del firmware de la radio.

Configure la conexión directa en **Radio Setup → Tuner**.

## Consejos

- El botón TUNE no responderá si el sintonizador está en modo BYPASS o STANDBY. Configure el sintonizador en OPERATE primero.
- El parpadeo de ROE posterior a la sintonía le permite leer la ROE final inmediatamente después de sintonizar sin tener que observar un medidor separado.

## Solución de problemas

- **El botón TUNE permanece rojo y no vuelve a TUNE** — El ciclo de sintonía puede haberse interrumpido. Haga clic en TUNE nuevamente o verifique la conexión al TGXL.
- **TUNE está atenuado o no responde** — Verifique que el sintonizador esté en modo OPERATE y que el TGXL esté detectado.
- **La sintonía falla o es lenta** — Si está ejecutando el firmware 4.2 y experimenta problemas de sintonía con la vía del firmware de la radio, configure una conexión directa al TGXL (puerto 9010) en Radio Setup → Tuner. Esto omite la vía del firmware de la radio para el comando de autosintonía.

## Relacionado

- [Lea la ROE inmediatamente después de una sintonía](read-swr-immediately-after-a-tune.md)
- [Ponga el sintonizador en OPERATE, BYPASS o STANDBY](#)

---

# Ajuste fino de los relés C1/L/C2 con la rueda del ratón

Ajuste las posiciones individuales de los bancos de relés en el 4O3A Tuner Genius XL usando la rueda del ratón sobre las barras de relés C1, L y C2.

## Antes de comenzar

- Debe estar activa una conexión directa al TGXL (puerto 9010). Las barras de relés solo se pueden ajustar cuando AetherSDR tiene una conexión directa al TGXL.
- El applet del sintonizador debe estar abierto.

## Pasos

1. Coloque el cursor del ratón sobre la barra de relé **C1**, **L** o **C2** en el applet del sintonizador.
2. Desplace la rueda del ratón hacia arriba para aumentar la posición del relé, o hacia abajo para disminuirla.
3. La barra de relé se actualiza inmediatamente para mostrar la nueva posición.

## Rangos de los relés

| Relé | Rango | Descripción |
|---|---|---|
| C1 | 0–255 | Banco de capacitores 1 |
| L | 0–255 | Banco de inductores |
| C2 | 0–255 | Banco de capacitores 2 |

## Cuando el desplazamiento está deshabilitado

El desplazamiento con la rueda del ratón solo está habilitado cuando una conexión directa al TGXL está activa. Si está utilizando la vía del firmware de la radio para comunicarse con el sintonizador, las barras de relés muestran los valores actuales pero no se pueden ajustar con la rueda del ratón.

## Consejos

- El ajuste fino de los relés es útil para optimizar una adaptación después de una autosintonía, o para ajustar manualmente el sintonizador a una impedancia específica.
- Los valores de los relés se envían inmediatamente al TGXL en cada evento de desplazamiento.

## Relacionado

- [Descripción general del sintonizador](overview.md)
- [Ejecute una autosintonía en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)

---

# Seleccione una antena con el conmutador ANT 1/2/3

Cuando una conexión directa al TGXL está activa, el applet del sintonizador muestra un conmutador de antena 3x1. Use los botones ANT 1, ANT 2 y ANT 3 para seleccionar qué puerto de antena usa el TGXL para enrutar la RF.

## Antes de comenzar

- Debe estar activa una conexión directa al TGXL (puerto 9010). La fila del conmutador de antena solo es visible cuando AetherSDR tiene una conexión directa al TGXL.
- El applet del sintonizador debe estar abierto.

## Pasos

1. Haga clic en el botón **ANT 1**, **ANT 2** o **ANT 3** en el applet del sintonizador.
2. El botón seleccionado se resalta para indicar que está activo.
3. El TGXL enruta inmediatamente la señal de RF al puerto de antena seleccionado.

## Cuando el conmutador de antena está oculto

Los botones ANT 1/2/3 solo son visibles cuando una conexión directa al TGXL está activa. Si está utilizando la vía del firmware de la radio para comunicarse con el sintonizador, la fila del conmutador de antena está oculta.

## Consejos

- Use el conmutador de antena para cambiar rápidamente entre antenas sin salir del applet del sintonizador.
- La selección de antena actual se muestra mediante el botón resaltado.

## Relacionado

- [Descripción general del sintonizador](overview.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
