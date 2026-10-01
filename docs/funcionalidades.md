# Funcionalidades

Este documento distingue entre funcionalidades presentes en el prototipo y capacidades planificadas para la versión integrada.

## Funcionalidades presentes en el prototipo

### Clientes

- Visualización de clientes.
- Búsqueda y edición local.
- Carga de base mediante Excel/CSV.
- Filtrado por código de vendedor configurado.
- Datos comerciales básicos y de contacto.

### Rutas de clientes

- Selección de clientes para visita.
- Ordenamiento y planificación visual.
- Uso de ubicación del navegador cuando el usuario la habilita.
- Configuración de minutos estimados por visita.
- Apertura de ubicaciones en mapas.

### Estado de cuentas

- Carga manual de información.
- Visualización de clientes y facturas.
- Saldos pendientes.
- Fechas de emisión y vencimiento.
- Estados de cobranza.
- Selección de facturas.
- Generación de vista imprimible.
- Exportación de vencimientos seleccionados a calendario `.ics`.

### Configuración comercial

- Perfil de usuario local.
- Código de vendedor.
- Código/identificador Anzio.
- Preferencias visuales.
- Almacenamiento local del prototipo.

### Ficha Comercial

La interfaz contempla un módulo desacoplado mediante `Conector_Ficha_Comercial.html`. El archivo conector no forma parte de esta versión hasta contar con una versión aprobada.

### Otros módulos del prototipo

- Inicio.
- Base de conocimientos.
- Colas.
- Chats.
- Herramientas del vendedor.
- Configuración de cuenta.

## Capacidades objetivo con backend

Cuando exista integración con SQL Server y Django, la plataforma debe evolucionar hacia:

- autenticación real;
- autorización por vendedor;
- actualización automática aproximadamente cada 5 minutos;
- cartera de clientes sincronizada;
- cuentas por cobrar casi en tiempo real;
- estadísticas de ventas;
- cumplimiento de metas;
- evolución por período;
- ranking/top de clientes;
- indicadores comerciales por vendedor;
- trazabilidad de sincronizaciones;
- registro de errores y accesos;
- API interna para los módulos del frontend.

## Regla de acceso

Un vendedor no debe obtener información de otro vendedor únicamente modificando parámetros en el frontend. El filtro por código comercial debe aplicarse y validarse en el backend.

El filtrado actual en JavaScript es únicamente una simulación de experiencia y no constituye un mecanismo de seguridad productivo.

## Fuentes de datos

El prototipo contempla tres dominios principales de integración:

- clientes;
- vendedores;
- cuentas por cobrar.

Estos conectores se reemplazarán progresivamente desde carga manual/Excel hacia servicios backend y SQL Server sin rediseñar la experiencia principal.