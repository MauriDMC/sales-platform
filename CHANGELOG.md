# Changelog

Todos los cambios relevantes de la Plataforma Comercial para Vendedores se documentarán en este archivo.

El proyecto utiliza una evolución compatible con Semantic Versioning durante la etapa de prototipo.

## [0.1.0] - 2026-10-01

### Añadido
- Inicialización formal del repositorio `sales-platform`.
- Documentación del objetivo, arquitectura y roadmap.
- Prototipo de interfaz comercial como base de trabajo.
- Módulos de clientes, rutas, estado de cuentas, herramientas, ficha comercial y configuración.
- Diseño de conectores desacoplados para clientes, vendedores y cuentas.

### Seguridad y privacidad
- Datos demostrativos públicos anonimizados.
- Exclusión explícita de credenciales, archivos productivos y cadenas de conexión.

### Arquitectura objetivo documentada
- Sistema legado como fuente.
- Extracción automática aproximada cada 5 minutos.
- SQL Server como capa de datos.
- Django como backend y capa de autorización.
- Interfaz comercial desacoplada del sistema fuente.

### Pendiente
- Implementación productiva de SQL Server/Django.
- Autenticación real y autorización por vendedor.
- Integración automática con el sistema fuente.
- Incorporación de `Conector_Ficha_Comercial.html` cuando exista una versión aprobada.
- Validaciones de seguridad, rendimiento y observabilidad.