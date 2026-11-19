## Context

El prototipo funciona desde un archivo HTML abierto directamente. Los perfiles simulan el flujo de atención local.

## Decisions

- Mantener clientes, solicitudes, eventos, consecutivos mensuales y próxima asignación en un estado en memoria. Guardar las fechas en ISO y mostrar horas de Colombia.
- Separar las operaciones de directorio y respaldo. Validar el archivo completo antes de sustituir datos. El respaldo incluye una versión de formato.
- Usar el reloj del dispositivo para el SLA. Actualizar la bandeja mientras está abierta y conservar el resultado al cerrar un caso resuelto.
- Mostrar una bandeja filtrable, un formulario de radicación y un detalle con historial. El coordinador consulta los casos y cada agente edita los propios.
- Entregar un directorio JSON ficticio. Probar el flujo en Chromium desde el sistema de archivos.
