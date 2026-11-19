# Propuesta para Comercial Aurora

## Why

Comercial Aurora atiende a 300 clientes activos y procesa cerca de 1.200 pedidos al mes. El prototipo permitirá probar un flujo común para registrar las solicitudes, asignar responsables y detectar demoras que afectan la confiabilidad de la atención y la recompra.

## What Changes

- Radicar solicitudes de mensajería, correo electrónico y llamadas. Buscar al cliente por NIT, seleccionar el tipo de solicitud y registrar el número de pedido cuando corresponda.
- Generar tickets únicos con formato `AUR-YYYYMM-XXXX`, iniciar cada solicitud en estado **Nuevo** y repartir los casos por rotación entre cuatro agentes.
- Alternar entre los cuatro perfiles de agente y el perfil de coordinador. Cada agente podrá consultar sus casos, agregar comentarios y actualizar estados. El coordinador podrá consultar todos los casos y filtrar por responsable, estado o tramo de plazo.
- Registrar la radicación y los cambios de estado con fecha, perfil y comentario. Los estados serán **Nuevo**, **En proceso**, **Pendiente logística**, **Pendiente ventas**, **Resuelto** y **Cerrado**.
- Mostrar alertas visuales a las 24 y 36 horas corridas. Marcar las solicitudes abiertas como vencidas cuando superen las 48 horas. Al resolver un caso, registrar el tiempo transcurrido y si cumplió el plazo.
- Importar el directorio de clientes en JSON. Exportar y restaurar clientes, solicitudes, historial y secuencias en JSON. Si un archivo es inválido, informar el error y conservar los datos en memoria.
- Entregar `aurora.html` con CSS y JavaScript integrados, un directorio de clientes ficticios en JSON y las especificaciones OpenSpec. El HTML se podrá abrir con doble clic y usar sin conexión.

## Capabilities

### New Capabilities

- `radicacion-de-solicitudes` — Captura, validación, generación de tickets y asignación por rotación.
- `seguimiento-de-solicitudes` — Bandejas por perfil, estados, historial y control del plazo de atención.
- `intercambio-de-datos-json` — Importación del directorio y respaldo y restauración de la sesión.

### Modified Capabilities

## Impact

La interfaz será adaptable y se ejecutará en el navegador. Los datos se mantendrán en objetos y arreglos de JavaScript durante el uso. La autenticación real, el acceso simultáneo, el almacenamiento centralizado, las notificaciones externas y las integraciones con ERP, correo y mensajería quedan fuera de alcance.

## Validación prevista

- Abrir el HTML con doble clic y completar el flujo desde el registro hasta la resolución sin conexión.
- Importar un directorio JSON, buscar un cliente por NIT y confirmar que una solicitud incompleta se rechaza sin alterar la bandeja.
- Radicar cinco solicitudes consecutivas y verificar que los identificadores son únicos y que la quinta se asigna al primer agente.
- Confirmar que cada agente ve sus solicitudes y que el coordinador ve todas.
- Comprobar las alertas a las 24 y 36 horas, el cumplimiento al resolver a las 48 horas exactas y el vencimiento al superar ese umbral con el caso abierto.
- Exportar un respaldo, cerrar y reabrir el HTML, restaurar el respaldo y comprobar que el siguiente caso continúa la numeración y la rotación.
