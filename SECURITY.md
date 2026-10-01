# Seguridad

Este repositorio contiene un prototipo público. No debe utilizarse para publicar datos productivos ni secretos.

## Reglas del repositorio

No subir:

- usuarios o contraseñas;
- tokens, claves API o certificados;
- cadenas de conexión SQL Server;
- archivos `.env`;
- exportaciones reales de clientes, cuentas, facturas o ventas;
- RUT, correos, teléfonos u otros datos personales reales;
- nombres de servidores, IP internas o rutas de red;
- archivos de respaldo de bases de datos.

## Arquitectura productiva esperada

La interfaz del vendedor no debe conectarse directamente al sistema legado ni a SQL Server.

El acceso esperado es:

```text
Navegador del vendedor
        ↓ HTTPS
Backend Django
        ↓ permisos / reglas de negocio
SQL Server
        ↓ proceso de integración controlado
Sistema fuente
```

El backend debe aplicar, como mínimo:

- autenticación;
- autorización por usuario y código de vendedor;
- mínimo privilegio;
- validación de entradas;
- registro de accesos y errores;
- protección de secretos fuera del código fuente;
- cifrado en tránsito;
- consultas parametrizadas;
- límites y controles sobre procesos de sincronización.

## Datos públicos de demostración

Los datos incluidos en el prototipo deben mantenerse ficticios o anonimizados. Antes de cada publicación debe verificarse que no existan datos operacionales reales.

## Reporte de vulnerabilidades

No publicar credenciales, datos personales ni información de infraestructura sensible en un issue público. Los detalles sensibles deben tratarse mediante un canal privado definido por el propietario del repositorio.