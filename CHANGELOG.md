# Changelog

Todos los cambios relevantes de la Plataforma Comercial para Vendedores se documentarán en este archivo.

El proyecto utiliza una evolución compatible con Semantic Versioning durante la etapa de prototipo.

## [0.2.0] - 2026-10-26

### Añadido
- `prototypes/app-vendedor-v112.html`: prototipo completo de la App del Vendedor (versión pública con datos ficticios).
- Estado de cuentas: filtro por región y comuna a partir del maestro de clientes (para todos los usuarios).
- Módulo «Estado de situación» (ficha del cliente) con «Control de crédito» en un cuadro superpuesto.
- Módulo «Historial» (cartola de movimientos) con encabezado fijo, filtros por tipo, exportación a Excel, subida de facturas en PDF (guardadas solo en el navegador) y enlace preparado para la API de DBNET.
- Acceso de demostración sin clave (`AUTH_DEV_MODE`).

### Corregido
- Importación del informe «Deudas por vendedor»: se aceptan filas cuya columna EMP. es un dígito y cabeceras de vendedor con un solo espacio.

### Seguridad y privacidad
- Usuarios, correos, teléfonos y claves reemplazados por valores de demostración.
- Cliente de ejemplo anonimizado (COMERCIAL DEMO S.A., RUT ficticio).

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