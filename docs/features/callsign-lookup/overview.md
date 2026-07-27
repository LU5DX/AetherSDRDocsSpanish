# Resumen de la consulta de indicativos

La función de consulta de indicativos busca en bases de datos de radioaficionados en línea —principalmente QRZ.com— para mostrar detalles del operador, como nombre, ubicación, cuadrícula, entidad DXCC, clase de licencia, bandera del país y biografía para cualquier indicativo que ingrese.

Los resultados aparecen en una tarjeta de indicativo que muestra los detalles del operador y un mapa cuando está disponible. Esto es útil para identificar indicativos escuchados al aire, planificar QSOs o investigar estaciones de DX.

## Cómo funciona

1. Abra el diálogo de Consulta de indicativos usando cualquiera de estos métodos:
   - **Tools > Callsign Lookup...**
   - Haga clic derecho en una señal en el panadapter y elija **Lookup**
2. Escriba un indicativo en el campo **Callsign field**.
3. Presione Enter o haga clic en el botón **Lookup** para enviar la consulta.
4. La **Callsign card** aparece con el resultado de la consulta, mostrando nombre, ubicación, cuadrícula, entidad DXCC, bandera del país, clase de licencia y una biografía cuando está disponible.

Para datos completos (dirección, cuadrícula, biografía), la función requiere una suscripción XML válida a QRZ.com. Sin una suscripción, los resultados pueden limitarse a datos básicos del indicativo.

## Función de cada control

| Control | Tipo | Comportamiento | Notas |
|---------|------|----------------|-------|
| **Callsign field** | Campo de texto | Escriba un indicativo y presione Enter o haga clic en Lookup para iniciar la consulta. | Sin valor predeterminado; sin configuración persistente. |
| **Lookup button** | Botón pulsador | Envía la consulta a QRZ.com y otras bases de datos configuradas. | Se requiere suscripción XML a QRZ para datos completos. |
| **Callsign card** | Indicador | Muestra el resultado: nombre, ubicación, cuadrícula, entidad DXCC, bandera del país, clase de licencia y biografía. | La apariencia depende de la respuesta de la base de datos. |

## Consejos

- Se recomienda encarecidamente una suscripción XML a QRZ.com para obtener los resultados más útiles. Sin ella, es posible que solo vea datos básicos del indicativo y la cuadrícula.
- Puede iniciar una consulta directamente desde una señal en el panadapter haciendo clic derecho en la etiqueta de la señal y eligiendo **Lookup** — no es necesario escribir el indicativo manualmente.

## Relacionados

- [Consulte un indicativo en QRZ.com](look-up-a-callsign-on-qrz-com.md)
- [Vea el nombre, ubicación y entidad DXCC del operador](see-operator-name-location-and-dxcc-entity.md)
- [Vea la tarjeta de indicativo con bandera y detalles](view-the-callsign-card-with-flag-and-details.md)
