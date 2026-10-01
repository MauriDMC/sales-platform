# Roadmap

## v0.1 — Base del prototipo

**Estado:** actual

- Repositorio formal.
- Interfaz comercial base.
- Clientes.
- Rutas.
- Estado de cuentas.
- Herramientas y configuración.
- Documentación de arquitectura.
- Datos públicos anonimizados.

## v0.2 — Normalización del frontend

- Separar HTML, CSS y JavaScript en archivos mantenibles.
- Eliminar dependencias temporales no utilizadas.
- Consolidar nombres de módulos y estados.
- Definir contratos de datos del frontend.
- Incorporar pruebas básicas de interfaz.

## v0.3 — Modelo SQL Server

- Definir tablas maestras y transaccionales.
- Claves primarias y foráneas.
- Índices para consultas comerciales.
- Tablas de control de sincronización.
- Estrategia incremental de extracción.
- Validación de calidad de datos.

## v0.4 — Backend Django

- Proyecto Django.
- Autenticación.
- Modelo de usuario/vendedor.
- Autorización por registro.
- API para clientes.
- API para cuentas por cobrar.
- API para ventas e indicadores.
- Gestión de errores y logging.

## v0.5 — Integración sistema fuente

- Conector de lectura aprobado por TI.
- Sincronización programada.
- Objetivo inicial: aproximadamente 5 minutos.
- Registro de última sincronización.
- Manejo de fallos y reintentos.
- Validación de carga sobre el sistema origen.

## v0.6 — Inteligencia comercial

- Ventas por período.
- Cumplimiento de metas.
- Tendencias.
- Top clientes.
- Evolución por cliente/producto cuando los datos lo permitan.
- Indicadores de cobranza.

## v0.7 — Operación y endurecimiento

- Pruebas de permisos.
- Auditoría de accesos.
- Gestión de secretos.
- HTTPS.
- Monitoreo.
- Backups.
- Pruebas de rendimiento.
- Validación con usuarios comerciales.

## v1.0 — Primera versión integrada

Criterios propuestos:

- frontend estable;
- backend Django desplegado;
- SQL Server integrado;
- sincronización automática validada;
- autorización por vendedor probada;
- datos productivos no expuestos en cliente ni repositorio;
- indicadores principales validados por negocio;
- documentación técnica y operativa disponible.