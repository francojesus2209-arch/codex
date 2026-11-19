# Radicación de solicitudes

## Purpose

Permitir que Comercial Aurora registre las solicitudes recibidas por distintos canales y asigne un responsable desde el momento de la radicación.

## ADDED Requirements

### Requirement: Captura y validación de la solicitud
La aplicación SHALL permitir al agente radicar solicitudes para clientes del directorio e indicar el canal, el tipo, la descripción y, opcionalmente, el identificador de pedido.

#### Scenario: Consulta de cliente por NIT
- **WHEN** el agente busca el NIT de un cliente del directorio
- **THEN** la aplicación muestra su razón social para asociarla con la solicitud

#### Scenario: Registro con datos válidos
- **WHEN** el agente selecciona un cliente y un canal de mensajería, correo electrónico o llamada telefónica, clasifica la solicitud y escribe una descripción de al menos diez caracteres
- **THEN** la aplicación guarda la solicitud con el NIT y la razón social del cliente, el canal, el tipo, la descripción y el pedido si fue indicado
- **AND** acepta como tipos consulta de stock, estado del pedido, inconformidad de envío, facturación o cobro y devolución

#### Scenario: Datos faltantes o inválidos
- **WHEN** el agente intenta guardar con un canal o tipo inválido o ausente, un NIT que no corresponde a un cliente del directorio o una descripción de menos de diez caracteres tras quitar espacios exteriores
- **THEN** la aplicación indica qué debe corregir y conserva la bandeja sin cambios
- **AND** el intento no consume un consecutivo ni avanza la rotación

### Requirement: Identificación y estado inicial
La aplicación SHALL generar un ticket único e inmutable con formato `AUR-YYYYMM-XXXX` y registrar la fecha y hora de recepción y el estado inicial **Nuevo**.

#### Scenario: Primera radicación del mes
- **WHEN** el agente guarda la primera solicitud válida de un mes sin tickets previos
- **THEN** la aplicación asigna el consecutivo `0001` del año y mes de recepción, registra la fecha y hora del dispositivo y muestra el estado **Nuevo**

#### Scenario: Radicaciones sucesivas
- **WHEN** el agente guarda otra solicitud válida en el mismo mes
- **THEN** la aplicación asigna el siguiente consecutivo libre del mes y conserva los identificadores anteriores

#### Scenario: Consecutivos mensuales agotados
- **WHEN** el consecutivo mensual ya llegó a `9999` y el agente intenta registrar otro caso de ese mes
- **THEN** la aplicación informa que se agotaron los consecutivos y conserva las solicitudes y la rotación existentes

### Requirement: Asignación por rotación
La aplicación SHALL asignar las solicitudes nuevas a los cuatro agentes en orden circular y avanzar la rotación únicamente al guardar una solicitud válida.

#### Scenario: Cinco solicitudes consecutivas
- **WHEN** se guardan cinco solicitudes válidas desde una sesión nueva
- **THEN** las primeras cuatro se asignan a los agentes 1, 2, 3 y 4 respectivamente, y la quinta se asigna al agente 1
