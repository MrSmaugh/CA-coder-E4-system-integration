# Checkpoint 4 — Sincronización del Cerebro Agéntico con Ecosistemas de Negocio

## Descripción

Este checkpoint extiende el sistema multi-agente desarrollado en los módulos anteriores para incorporar **integraciones externas reales** y controles preventivos de seguridad dentro de n8n.

El proyecto corresponde a una **tienda de libros**, cuyo sistema ya cuenta con sub-workflows orientados a:

*  Consultas sobre el catálogo.
*  Gestión y consulta de información de libros.

Sobre esta arquitectura existente se incorporan las integraciones y controles requeridos para este checkpoint.

## Integraciones

Se integran tres herramientas externas mediante **OAuth2**:

* **CRM:** HubSpot / Salesforce.
* **Gmail:** casilla de soporte.
* **Slack:** canal del equipo de operaciones.

Los permisos se configuran siguiendo el principio de **Mínimo Privilegio**, limitando el acceso a las operaciones y datos necesarios.

## Controles implementados

El workflow incorpora los siguientes controles no-code:

1. **IF anti auto-reply**
   Detecta correos automáticos (`Auto-reply`, `Out of office`, `Undeliverable`, `no-reply@`, etc.) y evita ciclos de respuestas.

2. **Lookup antes de Create**
   Busca previamente el contacto en el CRM para evitar registros duplicados y errores `409`.

3. **Set / limpieza de payload**
   Reduce y valida la información enviada a los sistemas externos, evitando payloads innecesariamente grandes o inválidos.

4. **Create Draft / Human-in-the-loop**
   La respuesta generada por el sistema se almacena como borrador en Gmail. El envío definitivo requiere intervención humana.


Slack se utiliza como canal de comunicación operacional, aplicando previamente filtros y limpieza del payload cuando corresponde.

## Validación

Antes de la entrega se realizan pruebas manuales mediante **Test Step / Execute Workflow**, verificando:

* Autenticación correcta de los conectores.
* Filtrado de correos automáticos.
* Búsqueda previa de contactos.
* Prevención de duplicados.
* Limpieza y validación del payload.
* Creación de borradores en Gmail.
* Correcta comunicación con Slack.
