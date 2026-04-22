# Cambiar el puerto TCP base

El applet CAT Control enlaza cuatro servidores TCP compatibles con rigctld en puertos consecutivos a partir del puerto base. Cambie el puerto base cuando el valor predeterminado entre en conflicto con otra aplicación o cuando su programa de registro requiera un número de puerto específico.

## Antes de comenzar

- El applet CAT Control debe estar visible. Si no lo está, haga clic en el botón **CAT** de la bandeja en la barra lateral derecha para mostrarlo.
- Se requiere una conexión de radio.

## Pasos

1. En el campo **Base**, seleccione el valor actual y escriba el número de puerto deseado. Rango válido: 1024–65535. Valor predeterminado: `4532`.
2. Presione Enter o haga clic en otro lugar para confirmar. Si el valor está fuera del rango válido, vuelve automáticamente a `4532`.
3. El nuevo valor se guarda inmediatamente en `CatTcpPort`.
4. Si **Enable TCP** está activo en ese momento, los cuatro servidores se detienen y se reinician automáticamente en los nuevos puertos (base, base+1, base+2, base+3). No se requiere ninguna acción adicional.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| **Base** | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. Los canales A, B, C y D se enlazan a base, base+1, base+2 y base+3 respectivamente. Los valores fuera de rango vuelven automáticamente a `4532`. Si los servidores TCP están en ejecución, se reinician con el nuevo puerto de inmediato. |
| **Enable TCP** | Botón de alternancia | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP rigctld. También guarda el puerto base actual en `CatTcpPort` al alternarse. |
| Filas de canales A/B/C/D | Indicador | `(stopped)` | — | — | Muestra el estado TCP y el número de puerto de cada canal una vez que los servidores están en ejecución. |

## Consejos

- Los canales siempre ocupan cuatro puertos consecutivos. Si su puerto base es `4532`, los cuatro servidores escuchan en `4532`, `4533`, `4534` y `4535`. Asegúrese de que los cuatro puertos estén libres antes de iniciar.
- El cambio de puerto se escribe en `CatTcpPort` tanto al terminar de editar el campo **Base** como al alternar **Enable TCP**. No es necesario desactivar y reactivar los servidores para guardar el valor.

## Solución de problemas

- **El servidor no se reinicia después de cambiar el puerto** — Confirme que el nuevo valor fue aceptado verificando que las filas de canales muestren los números de puerto actualizados. Si el campo volvió a `4532`, el valor ingresado estaba fuera del rango 1024–65535.
- **La fila del canal sigue mostrando el puerto anterior después de editar** — Los servidores solo se reinician automáticamente si **Enable TCP** ya estaba activado cuando presionó Enter. Si TCP estaba desactivado, el nuevo puerto base entrará en efecto la próxima vez que active TCP.

## Relacionado

- [Activar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
