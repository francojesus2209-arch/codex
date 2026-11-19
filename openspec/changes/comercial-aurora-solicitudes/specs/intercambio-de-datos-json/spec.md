# Intercambio de datos JSON

## Purpose

Permitir que Comercial Aurora cargue su directorio local de clientes y conserve el trabajo entre sesiones mediante archivos JSON.

## ADDED Requirements

### Requirement: Importación del directorio
La aplicación SHALL importar un directorio desde un archivo JSON válido con NIT y razón social por cliente y ofrecer esos datos en la búsqueda de radicación.

#### Scenario: Directorio válido
- **WHEN** se importa el archivo JSON de clientes ficticios incluido en la entrega
- **THEN** la aplicación informa que se cargó el directorio y permite localizar a los clientes por NIT

### Requirement: Exportación del respaldo
La aplicación SHALL permitir descargar un archivo JSON con el directorio, las solicitudes, su historial y la información necesaria para continuar los consecutivos y la rotación.

#### Scenario: Descarga de la sesión
- **WHEN** se exportan los datos después de registrar y actualizar solicitudes
- **THEN** el navegador descarga un JSON que contiene los clientes, las solicitudes, sus eventos y la información de secuencia

### Requirement: Restauración del respaldo
La aplicación SHALL permitir cargar un respaldo JSON válido para recuperar la sesión respaldada y continuar el trabajo.

#### Scenario: Recuperación al volver a abrir
- **WHEN** se cierra la aplicación, se vuelve a abrir y se carga el respaldo
- **THEN** se recuperan el directorio, los tickets, responsables, estados e historiales exportados
- **AND** la siguiente radicación usa el consecutivo que corresponda a su mes y continúa la rotación desde el agente siguiente

### Requirement: Rechazo de archivos inválidos
La aplicación SHALL validar por completo un archivo antes de aplicar una importación de directorio o una restauración de respaldo.

#### Scenario: JSON incorrecto
- **WHEN** se carga un archivo que no contiene JSON válido o que carece de los datos esperados para la operación
- **THEN** la aplicación muestra un error y conserva los clientes, solicitudes, historial y secuencias de la sesión

### Requirement: Ejecución local
La aplicación SHALL funcionar en un navegador de escritorio o móvil a partir de un único archivo `aurora.html`, con CSS y JavaScript integrados y sin conexión a internet.

#### Scenario: Apertura directa sin conexión
- **WHEN** una persona abre `aurora.html` desde el sistema de archivos con el navegador desconectado
- **THEN** puede importar clientes, radicar solicitudes, consultar la bandeja y el historial, resolver casos y exportar el respaldo sin iniciar un servidor
