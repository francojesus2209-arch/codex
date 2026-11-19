# Seguimiento de solicitudes

## Purpose

Dar a cada agente una bandeja de sus solicitudes y al coordinador una vista general que permita detectar atrasos y revisar el historial de cada caso.

## ADDED Requirements

### Requirement: Bandejas por perfil
La aplicación SHALL ofrecer un selector con cuatro perfiles simulados de agente y uno de coordinador. Un agente ve sus solicitudes asignadas y el coordinador ve todas.

#### Scenario: Cambio entre agentes
- **WHEN** se cambia del perfil del agente 1 al del agente 2
- **THEN** la bandeja muestra solamente las solicitudes asignadas al agente 2

#### Scenario: Consulta del coordinador
- **WHEN** se selecciona el perfil de coordinador
- **THEN** la bandeja muestra las solicitudes de los cuatro agentes y permite filtrarlas por responsable, estado y tramo de plazo

### Requirement: Actualización de estado e historial
La aplicación SHALL permitir al agente asignado cambiar el estado y agregar comentarios. El historial SHALL conservar la radicación, los cambios de estado y los comentarios registrados, con su fecha, hora y perfil.

#### Scenario: Cambio de estado
- **WHEN** el agente asignado actualiza una solicitud a **En proceso**, **Pendiente logística**, **Pendiente ventas**, **Resuelto** o **Cerrado**
- **THEN** la bandeja refleja el estado y el historial incorpora el estado anterior, el nuevo estado, el perfil, la fecha y hora y el comentario si lo hay

#### Scenario: Comentario sin cambio de estado
- **WHEN** el agente asignado agrega un comentario a su solicitud
- **THEN** el comentario aparece en el historial con el perfil y la fecha y hora, y el estado se conserva

### Requirement: Alertas de plazo
La aplicación SHALL calcular las horas corridas desde la recepción de las solicitudes abiertas y mostrar su tramo al coordinador durante el uso.

#### Scenario: Antes de la primera alerta
- **WHEN** el coordinador consulta una solicitud abierta con menos de 24 horas corridas
- **THEN** la aplicación la muestra sin alerta de plazo

#### Scenario: Alerta a las 24 horas
- **WHEN** una solicitud abierta alcanza 24 horas corridas y aún no llega a 36
- **THEN** la aplicación muestra la primera alerta visual

#### Scenario: Alerta a las 36 horas
- **WHEN** una solicitud abierta alcanza 36 horas corridas y aún no supera las 48
- **THEN** la aplicación muestra la segunda alerta visual

#### Scenario: Solicitud vencida
- **WHEN** una solicitud abierta supera las 48 horas corridas
- **THEN** la aplicación la muestra como vencida

### Requirement: Medición al resolver
La aplicación SHALL registrar la fecha y hora de resolución, el tiempo transcurrido en horas corridas y el cumplimiento del plazo cuando el agente pase el caso a **Resuelto**.

#### Scenario: Resolución en el límite
- **WHEN** el agente resuelve una solicitud exactamente 48 horas después de su recepción
- **THEN** el caso registra 48 horas de atención y queda marcado como cumplido

#### Scenario: Resolución tardía
- **WHEN** el agente resuelve una solicitud después de 48 horas corridas
- **THEN** el caso registra el tiempo real de atención y queda marcado como fuera de plazo

#### Scenario: Consulta de casos terminados
- **WHEN** el coordinador consulta un caso **Resuelto** o **Cerrado**
- **THEN** el caso queda fuera de las alertas de solicitudes abiertas y su resultado de plazo permanece visible si ya fue calculado
